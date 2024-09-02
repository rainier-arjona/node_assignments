### Assignment: Real-Time Chatroom

In this assignment, you will create a real-time chatroom application using [Socket.io](http://socket.io/). Users will be able to enter a chatroom, send and receive messages, and see a log of user activity (joining and leaving). Implement real-time updates and manage user connections with [Socket.io](http://socket.io/).

![/10%20-%20Assets/ChatRoom1.png](/10%20-%20Assets/ChatRoom1.png)

**Estimated Time to Completion:** 2 hours

**Level of Complexity:** Medium

**Instructions**

1. **Create the Chatroom Application**
    - **Set Up the Server:** Implement a basic Express server with [Socket.io](http://socket.io/). Install necessary dependencies: `socket.io`, `express`, and `typescript`.
    - **Implement [Socket.io](http://socket.io/):** Set up [Socket.io](http://socket.io/) on the server to handle real-time communication. Create events for handling user connections, disconnections, and message broadcasting.
    - **Create a Simple Frontend:** Create an HTML page with a chat interface where users can enter their name and send messages. Use JavaScript or TypeScript to interact with [Socket.io](http://socket.io/) on the client side.
2. **Implement Socket Commands**
    - **Connect/Disconnect:** Implement functionality to log when a user connects or disconnects from the chatroom. Display messages in the chatroom when users join or leave.
    - **Broadcast Messages:** Allow users to send messages that are broadcasted to all connected users.
    - **Emit and Listen:** Set up `emit` and `on` handlers for sending and receiving messages and user activity logs.
3. **Add Real-Time Data Updates**
    - **Live Chat:** Implement real-time chat functionality so that messages are immediately visible to all users in the chatroom.
    - **User Activity Log:** Display logs of users joining and leaving the chatroom.
4. **Optional: Implement JWT for User Authentication**
    - **JWT Integration:** Optionally, implement JWT to authenticate users before they can enter the chatroom. Ensure that users must log in before accessing the chatroom. If you choose to implement this, use the `jsonwebtoken` package to create and verify JWTs.
5. **Submit Your Work**
    - Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives**

- **Functionality:** Ensure the chatroom operates correctly with real-time updates. Messages should be broadcasted to all users, and user connections and disconnections should be logged in real time.
- **User Experience:** The chat interface should be intuitive and responsive. Users should be able to easily send and receive messages and view a clear log of user activity.
- **Code Quality:** Code should be well-organized, clean, and properly commented. Follow best practices for coding standards and structure.
- **Real-Time Performance:** Demonstrate efficient real-time communication between server and clients. The chatroom should handle multiple users smoothly.
- **Optional Feature:** If implementing JWT, ensure secure user authentication and that users are required to log in before accessing the chatroom.

**Expected Outputs**

- **Functional Chatroom:** A working chatroom application where users can:
    - Connect with a username.
    - Send and receive messages in real time.
    - View a log of user activity (joining and leaving).
- **Real-Time Messaging:** Messages sent by any user should immediately appear to all connected users.
- **User Activity Logging:** Users should see notifications or messages when other users join or leave the chatroom.
- **Optional JWT Integration:** If implemented, users must authenticate with JWT before accessing the chatroom, ensuring a secure login process.