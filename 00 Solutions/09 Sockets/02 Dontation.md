### server.ts
```ts
import express, { Request, Response } from 'express';
import http from 'http';
import { Server as SocketIOServer } from 'socket.io';
import path from 'path';

const app = express();
const server = http.createServer(app);
const io = new SocketIOServer(server);

const port = 3000;
const donors: { [key: string]: number } = {}; // Store donors and their donations

// Serve static files
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, '..', 'src', 'views'));
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));

// Express route
app.get('/', (req: Request, res: Response) => {
    res.render('index');
});

// Function to get sorted donors
/**
 * Retrieves the sorted list of donors.
 *
 * @returns {Array<{ name: string, donation: number }>} The sorted list of donors, sorted by donation amount in descending order.
 */
const getSortedDonors = () => {
    return Object.entries(donors)
        .sort(([, donationA], [, donationB]) => donationB - donationA) // Sort by donation amount in descending order
        .map(([name, donation]) => ({ name, donation }));
};

// Socket.io connection handler
io.on('connection', (socket) => {
    console.log('A user connected');

    // Handle new user connection
    socket.on('new_user', (donor_name: string) => {
        console.log(`${donor_name} connected`);
        socket.emit('update_donors', getSortedDonors());
    });

    // Handle donation event
    socket.on('donate', (data: { donor_name: string, amount: number }) => {
        const { donor_name, amount } = data;

        // Increment the donor's donation or set it if they haven't donated yet
        donors[donor_name] = (donors[donor_name] || 0) + amount;

        // Broadcast updated donor list to all clients
        io.emit('update_donors', getSortedDonors());
    });

    socket.on('disconnect', () => {
        console.log('A user disconnected');
    });
});

server.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});

```

### public/scripts/index.js
```js
document.addEventListener('DOMContentLoaded', () => {
    const socket = io();
    const donor_name = prompt("Enter your name:") || "User";

    const donate25 = document.getElementById('donate25');
    const donate50 = document.getElementById('donate50');
    const donate100 = document.getElementById('donate100');
    const donorsList = document.querySelector('.donors_list ul');

    if (donor_name) {
        socket.emit('new_user', donor_name);
    }

    const handleDonateClick = (amount) => {
        socket.emit('donate', { donor_name, amount: Number(amount) });
    };

    donate25.addEventListener('click', () => handleDonateClick(25));
    donate50.addEventListener('click', () => handleDonateClick(50));
    donate100.addEventListener('click', () => handleDonateClick(100));

    socket.on('update_donors', (sortedDonors) => {
        donorsList.innerHTML = '';
        sortedDonors.forEach(({ name, donation }) => {
            const li = document.createElement('li');
            li.textContent = `${name} - $${donation}`;
            donorsList.appendChild(li);
        });
    });
});
```

### views/index.ejs
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Donate.io</title>
    <script src="/socket.io/socket.io.js"></script>
    <script src="/scripts/index.js" defer></script>
    <link rel="stylesheet" href="/styles/style.css">
</head>

<body>
    <section>
        <h1>Donors List</h1>
        <div class="donors_list">
            <ul>
                <!-- Donors list will be populated here -->
            </ul>
        </div>
    </section>
    <section>
        <h2>Support Our Cause</h2>
        <img src="/images/egg.jpg" alt="Support">
        <button type="button" id="donate25">Donate $25</button>
        <button type="button" id="donate50">Donate $50</button>
        <button type="button" id="donate100">Donate $100</button>
    </section>
</body>

</html>
```