# Real-time Donation

In this assignment, you’ll create a real-time donation tracker application using [Socket.io](http://socket.io/) and Express.js with TypeScript. Your goal is to establish a live connection between the server and clients, allowing users to see donations as they happen.

---

![Wireframe](https://prod-files-secure.s3.us-west-2.amazonaws.com/19ad07a1-ef67-4a69-a521-ac6460e9edce/c5d223aa-7d83-4af4-a359-4823d4745805/Untitled.png)

**Estimated Time to Completion:** 150 minutes

**Level of Complexity:** Medium

**Instructions**

1. **Read through the Directions:**
    - Understand the concepts of WebSockets and Socket.io.
    - After familiarizing yourself with essential Socket.io events such as `connect`, `disconnect`, `broadcast`, we will not implement `emit`.
2. **Complete the Project Setup:**
    - Initialize a Node.js project and install necessary dependencies (Express, Socket.io, TypeScript, etc.) as covered in the initial setup.
3. **Create the Express Server (server.ts):**
    - Set up an Express application.
    - Integrate Socket.io with the Express server.
    - Configure the server to listen on a specified port.
4. **Implement Socket.io Events (server.ts):**
    - **Connection Event:** On client connection, prompt the user for their name.
        - Emit a `prompt name` event to the client.
        - Store the user's name and manage connections.
    - **Donation Event:** Handle donation events from clients.
        - Emit a `donate` event to all connected clients, including the donor’s name and donation amount.
5. **Develop the Client-Side Application (client.html and client.ts):**
    - **HTML Setup:** Create an HTML file to serve as the client interface.
        - Include Socket.io and client-side script references.
    - **Client-Side Logic (client.ts):**
        - Establish a connection to the Socket.io server.
        - Handle the `prompt name` event to get the user's name and send it to the server.
        - Implement a donation button:
            - Emit a `donate` event when the button is clicked.
        - Listen for donation events from the server and update the UI to display donation information in real-time.
6. **Run the Application:**
    - Compile TypeScript files to JavaScript.
    - Start the Express server.
    - Open the application in multiple browser windows to simulate different users and observe the real-time updates.

**MVP Requirements:**

- **Server-Side:**
    - Set up a basic Express server.
    - Integrate Socket.io to handle real-time events.
    - Implement logic to handle user connections, disconnections, and donations.
- **Client-Side:**
    - Create an interface that allows users to input their name and make donations.
    - Ensure all connected clients see updates for each donation in real-time.

**Expected Outputs:**

- A real-time donation tracker where users can:
    - Connect with a username.
    - Make donations that are broadcast to all connected users.
    - See live updates of donations made by others.