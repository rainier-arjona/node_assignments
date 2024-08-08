### server.ts
```ts
import express, { Request, Response } from 'express';
import http from 'http';
import { Server as SocketIOServer, Socket } from 'socket.io';
import path from 'path';

const app = express();
const server = http.createServer(app);
const io = new SocketIOServer(server);

const port = 3000;

/**
 * Interface representing a chat message.
 * @typedef {Object} ChatMessage
 * @property {string} username - The username of the message sender.
 * @property {string} message - The content of the message.
 */
interface ChatMessage {
    username: string;
    message: string;
}

/**
 * Interface representing a user activity log entry.
 * @typedef {Object} UserActivity
 * @property {string} username - The username of the user.
 * @property {string} activityType - The type of activity (e.g., "joined" or "left").
 * @property {number} timestamp - The timestamp of the activity.
 */
interface UserActivity {
    username: string;
    activityType: string;
    timestamp: number;
}

/**
 * Interface representing user information associated with a socket.
 * @typedef {Object} UserSocketInfo
 * @property {string} username - The username of the user.
 * @property {string} room - The name of the room the user is in.
 */
interface UserSocketInfo {
    username: string;
    room: string;
}

// Maps to store room-specific data
const chatHistory: { [room: string]: ChatMessage[] } = {};
const userActivity: { [room: string]: UserActivity[] } = {};
const userSocketMap: Map<string, UserSocketInfo> = new Map(); // Map to store socket ID to user info

app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, '..', 'src', 'views'));
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));

/**
 * Renders the homepage.
 * @param {Request} req - The request object.
 * @param {Response} res - The response object.
 */
app.get('/', (req: Request, res: Response) => {
    res.render('index');
});

/**
 * Renders a chat room page.
 * @param {Request} req - The request object.
 * @param {Response} res - The response object.
 */
app.get('/room/:roomName', (req: Request, res: Response) => {
    res.render('room');
});

io.on('connection', (socket: Socket) => {
    let username: string | null = null;
    let roomName: string | null = null;

    /**
     * Handles a user joining a room.
     * @param {Object} data - The data containing username and room.
     * @param {string} data.username - The username of the user.
     * @param {string} data.room - The room the user is joining.
     */
    socket.on('join room', (data: { username: string, room: string }) => {
        username = data.username;
        roomName = data.room;
        userSocketMap.set(socket.id, { username: data.username, room: data.room });
        socket.join(data.room);

        // Initialize room-specific data if it doesn't exist
        if (!chatHistory[data.room]) chatHistory[data.room] = [];
        if (!userActivity[data.room]) userActivity[data.room] = [];

        const now = Date.now();
        userActivity[data.room].push({ username: data.username, activityType: 'joined', timestamp: now });

        const activeUsers = Array.from(userSocketMap.values())
            .filter(user => user.room === data.room)
            .map(user => user.username);

        io.to(data.room).emit('user activity', userActivity[data.room]);
        io.to(data.room).emit('chat history', chatHistory[data.room]);
        io.to(data.room).emit('user list', activeUsers);
        io.to(data.room).emit('user count', activeUsers.length); // Emit user count
    });

    /**
     * Handles a user disconnecting from a room.
     */
    socket.on('disconnect', () => {
        if (username && roomName) {
            const now = Date.now();
            userActivity[roomName].push({ username: username, activityType: 'left', timestamp: now });
            userSocketMap.delete(socket.id);

            // Emit updated user list and count
            const updatedUsers = Array.from(userSocketMap.values())
                .filter(user => user.room === roomName)
                .map(user => user.username);

            io.to(roomName).emit('user activity', userActivity[roomName]);
            io.to(roomName).emit('user list', updatedUsers);
            io.to(roomName).emit('user count', updatedUsers.length);
        }
    });

    /**
     * Handles incoming chat messages.
     * @param {Object} data - The chat message data.
     * @param {string} data.room - The room where the message is sent.
     * @param {string} data.message - The message content.
     */
    socket.on('chat message', (data: { room: string, message: string }) => {
        if (!chatHistory[data.room]) chatHistory[data.room] = [];
        chatHistory[data.room].push({ username: username || 'Anonymous', message: data.message });
        io.to(data.room).emit('chat message', { username: username || 'Anonymous', message: data.message });
    });

    /**
     * Returns the number of users in each room.
     * @param {Request} req - The request object.
     * @param {Response} res - The response object.
     */
    app.get('/room-counts', (req: Request, res: Response) => {
        const roomCounts: { [key: string]: number } = {};

        io.sockets.adapter?.rooms.forEach((room, roomName) => {
            roomCounts[roomName] = room.size;
        });

        res.json(roomCounts);
    });

});

server.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});
```

### index.js
```js
/**
 * Initializes the page when the DOM content is fully loaded.
 */
document.addEventListener('DOMContentLoaded', () => {
    const socket = io();
    const urlParams = new URLSearchParams(window.location.search);
    const encodedRoomName = window.location.pathname.split('/').pop();
    const roomName = decodeURIComponent(encodedRoomName);
    const username = urlParams.get('username') || 'Anonymous';
    const roomCountElements = {};

    /**
     * Updates the displayed room counts.
     * @param {Object<string, number>} counts - An object where the key is the room name and the value is the count of users in that room.
     */
    function updateRoomCounts(counts) {
        for (const [roomName, count] of Object.entries(counts)) {
            const roomCountElement = roomCountElements[roomName];
            if (roomCountElement) {
                roomCountElement.textContent = count;
            }
        }
    }

    /**
     * Creates a message element for display in the chat.
     * @param {Object} data - The message data.
     * @param {string} data.username - The username of the sender.
     * @param {string} data.message - The message content.
     * @returns {HTMLElement} - The created message element.
     */
    function createMessageElement(data) {
        const messageElement = document.createElement('li');
        messageElement.innerHTML = `<strong>${data.username}:</strong> ${data.message}`;
        return messageElement;
    }

    /**
     * Creates a log entry element for display in the activity log.
     * @param {Object} logEntry - The log entry data.
     * @param {string} logEntry.username - The username of the user.
     * @param {string} logEntry.activityType - The type of activity (e.g., "joined" or "left").
     * @param {number} logEntry.timestamp - The timestamp of the activity.
     * @returns {HTMLElement} - The created log entry element.
     */
    function createLogEntryElement(logEntry) {
        const logItem = document.createElement('li');
        const time = new Date(logEntry.timestamp).toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
        const activityType = logEntry.activityType;

        logItem.classList.add('activity-log-entry', activityType);
        logItem.innerHTML = `<span class="activity-log-time">${time}</span> ${logEntry.username} has ${activityType}.`;
        return logItem;
    }

    /**
     * Creates a user element for display in the user list.
     * @param {string} user - The username to display.
     * @returns {HTMLElement} - The created user element.
     */
    function createUserElement(user) {
        const userItem = document.createElement('li');
        userItem.textContent = user;
        return userItem;
    }

    /**
     * Joins a specified room by redirecting the user to the room page.
     * @param {string} room - The name of the room to join.
     */
    function joinRoom(room) {
        const encodedRoom = encodeURIComponent(room);
        window.location.href = `/room/${encodedRoom}?username=${username}`;
    }

    /**
     * Sends a chat message to the server.
     * @param {string} message - The message to send.
     */
    function sendMessage(message) {
        if (message) {
            socket.emit('chat message', { room: roomName, message });
        }
    }

    /**
     * Handles form submission to send a chat message.
     * @param {Event} e - The form submit event.
     */
    function handleFormSubmit(e) {
        e.preventDefault();
        const messageInput = document.getElementById('message-input');
        const message = messageInput.value;
        sendMessage(message);
        messageInput.value = '';
    }

    /**
     * Initializes event listeners and updates the page content.
     */
    function initialize() {
        fetch('/room-counts')
            .then(response => response.json())
            .then(data => {
                updateRoomCounts(data);
            });

        document.querySelectorAll('.chatroom-room').forEach(room => {
            const roomName = room.querySelector('.chatroom-room-name').textContent;
            const countElement = room.querySelector('.user-count');

            if (countElement) {
                roomCountElements[roomName] = countElement;
            }
        });

        document.querySelectorAll('button[data-room]').forEach(button => {
            button.addEventListener('click', () => {
                const room = button.getAttribute('data-room');
                joinRoom(room);
            });
        });

        document.getElementById('room-name').textContent = roomName;

        socket.emit('join room', { username, room: roomName });

        socket.on('chat message', (data) => {
            const newMessage = createMessageElement(data);
            document.getElementById('message-list').appendChild(newMessage);
        });

        socket.on('chat history', (history) => {
            history.forEach(data => {
                const message = createMessageElement(data);
                document.getElementById('message-list').appendChild(message);
            });
        });

        socket.on('user activity', (activityLog) => {
            const log = document.getElementById('activity-log');
            log.innerHTML = '';
            activityLog.forEach(logEntry => {
                const logItem = createLogEntryElement(logEntry);
                log.appendChild(logItem);
            });
        });

        socket.on('user list', (users) => {
            const userList = document.getElementById('user-list');
            userList.innerHTML = '';
            users.forEach(user => {
                const userItem = createUserElement(user);
                userList.appendChild(userItem);
            });
        });

        socket.on('user count', (count) => {
            document.getElementById('user-count').textContent = count;
        });

        document.getElementById('message-form').addEventListener('submit', handleFormSubmit);
    }

    initialize();
});
```

### index.ejs
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ChatRoom</title>
    <script src="/scripts/index.js" defer></script>
    <script src="/socket.io/socket.io.js"></script>
    <link rel="stylesheet" href="/styles/style.css">
    <script>
        function joinRoom(roomName) {
            const username = prompt('Enter your username:') || 'Anonymous';
            window.location.href = `/room/${roomName}?username=${username}`;
        }
    </script>
</head>

<body>
    <div class="chatroom">
        <h1>Select a Room</h1>
        <section class="chatroom-rooms">
            <article class="chatroom-room">
                <header>
                    <h2 class="chatroom-room-name">Book Club Bliss</h2>
                </header>
                <button onclick="joinRoom('Book Club Bliss')">Join Room</button>
                <p>Users:</p>
                <span class="user-count">0</span> <!-- count of users in the room -->
            </article>
            <article class="chatroom-room">
                <header>
                    <h2 class="chatroom-room-name">Coding Corner</h2>
                </header>
                <button onclick="joinRoom('Coding Corner')">Join Room</button>
                <p>Users:</p>
                <span class="user-count">0</span> <!-- count of users in the room -->
            </article>
        </section>
    </div>
</body>

</html>

```

### room.ejs
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chatroom</title>
    <script src="/scripts/index.js" defer></script>
    <script src="/socket.io/socket.io.js"></script>
    <link rel="stylesheet" href="/styles/style.css">
</head>

<body>
    <main>
        <header>
            <h1 id="room-name"></h1>
        </header>
        <section class="chat-container">
            <section class="activity-log">
                <h2>Activity Log:</h2>
                <ul id="activity-log"></ul>
            </section>
            <section class="chat-messages">
                <ul id="message-list"></ul>
                <form id="message-form">
                    <input type="text" id="message-input" placeholder="Type here..." />
                    <button type="submit">Send</button>
                </form>
            </section>
            <aside class="user-list">
                <h2>Users:</h2>
                <ul id="user-list"></ul>
            </aside>
        </section>
    </main>
</body>

</html>

```
