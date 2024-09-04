### Assignment: Real-time Donation

In this assignment, you’ll create a real-time donation tracker application using [Socket.io](http://socket.io/) and Express.js with TypeScript. Your goal is to establish a live connection between the server and clients, allowing users to see donations as they happen.

![../10%20-%20Assets/OnlineDonation.png](../10%20-%20Assets/OnlineDonation.png)

**Estimated Time to Completion:** 150 minutes

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date. 

**Evaluation Criteria & Learning Objectives**

-Install Socket.io dependencies on a new Node/Express project and implement: `emit`.

---

**Directions**

1. **Understand the Concepts:**
    - Review the basics of WebSockets and how [Socket.io](http://socket.io/) facilitates real-time communication.
    - Familiarize yourself with essential [Socket.io](http://socket.io/) events such as `connect`, `disconnect`, `broadcast`, and `emit`.
2. **Complete the Project Setup:**
    - Initialize a Node.js project.
    - Install necessary dependencies:
        
        ```
        npm install express socket.io typescript @types/node @types/express @types/socket.io
        
        ```
        
    - Set up your TypeScript configuration and folder structure.
3. **Create the Express Server (`server.ts`):**
    - Set up an Express application.
    - Integrate [Socket.io](http://socket.io/) with the Express server.
    - Configure the server to listen on a specified port.
4. **Implement [Socket.io](http://socket.io/) Events (`server.ts`):**
    - **Connection Event:**
        - On client connection, emit a `prompt name` event to request the user's name.
        - Store the user's name and manage connections.
    - **Donation Event:**
        - Handle donation events sent by clients.
        - Emit a `donate` event to all connected clients, including the donor’s name and donation amount.
5. **Develop the Client-Side Application (`client.html` and `client.ts`):**
    - **HTML Setup:**
        - Create an HTML file to serve as the client interface.
        - Include [Socket.io](http://socket.io/) and client-side script references.
    - **Client-Side Logic (`client.ts`):**
        - Establish a connection to the [Socket.io](http://socket.io/) server.
        - Handle the `prompt name` event to capture the user's name and send it back to the server.
        - Implement a donation button:
            - Emit a `donate` event when the button is clicked.
        - Listen for donation events from the server and update the UI to display donation information in real-time.
6. **Run the Application:**
    - Compile TypeScript files to JavaScript.
    - Start the Express server:
        
        ```
        npm start
        
        ```
        
    - Open the application in multiple browser windows to simulate different users and observe the real-time updates.


**MVP Requirements: Real-Time Donations System with Express and Socket.io**

- **Server-Side:**
    - Set up a basic Express server.
    - Integrate [Socket.io](http://socket.io/) to handle real-time events.
    - Implement logic to handle user connections, disconnections, and donations.
- **Client-Side:**
    - Create an interface that allows users to input their name and make donations.
    - Ensure all connected clients see updates for each donation in real-time.

**Expected Outputs:**

- A real-time donation tracker where users can:
    - Connect with a username.
    - Make donations that are broadcast to all connected users.
    - See live updates of donations made by others.