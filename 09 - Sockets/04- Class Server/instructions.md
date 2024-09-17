### Assignment: Class Server

In this assignment, you will create a **Class Server** using Node.js, Express, and [Socket.io](http://socket.io/), which will track and broadcast connections and disconnections of students (clients). Each student will be identified by their unique socket ID, and whenever a student connects to or leaves the class, the server will broadcast this information to all other connected students in real time.

![Server.png](./Server.png)

**Estimated Time to Completion:** 60 minutes

**Level of Complexity:** Beginner

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Set up and configure a Class Server using Express.js and [Socket.io](http://socket.io/).
- Implement real-time tracking of student connections and disconnections using [Socket.io](http://socket.io/) events.
- Broadcast class-wide notifications when students join or leave the class.

---

**Directions**

1. **Complete the Project Setup:**
    - Create a new project directory.
    - Initialize a Node.js project using `npm init -y`.
    - Install required dependencies: Express, Socket.io, and TypeScript (along with necessary TypeScript dependencies like `typescript` and `@types/node`).

2. **Create the Class Server (`server.ts`):**
   - Set up an Express server to act as the Class Server, where students (clients) will connect.
   - Configure the server to optionally serve static files, such as a basic front-end interface for the students to connect to.
   - Set the server to listen on a designated port.

3. **Integrate [Socket.io](http://socket.io/) to Manage Class Connections:**
   - Import [Socket.io](http://socket.io/) into your server code.
   - Create a [Socket.io](http://socket.io/) server instance and attach it to the Express server.

4. **Implement [Socket.io](http://socket.io/) Events to Handle Student Connections and Disconnections (`server.ts`):**
   - **Connection Event:**
     - Listen for the `connection` event when a student joins the class.
     - Log the connected student’s unique socket ID to track who is present.
     - Broadcast a message to all other students in the class, announcing the arrival of a new student with their socket ID.

   - **Disconnection Event:**
     - Listen for the `disconnect` event when a student leaves the class.
     - Log the socket ID of the disconnected student.
     - Broadcast a message to all remaining students, notifying them that a student has left the class, along with their socket ID.

**Example Tasks:**

   1. **Student Connection Handling:**
      - When a new student joins the class, log their socket ID and broadcast a welcome message to the rest of the class, including the new student's socket ID.

   2. **Student Disconnection Handling:**
      - When a student leaves the class, log their socket ID and broadcast a message to the remaining students, notifying them of the student’s departure along with their socket ID.


**MVP Requirements: Real-Time Class Server**

- **Server-Side:**
   - Set up an Express.js server as the Class Server.
   - Integrate [Socket.io](http://socket.io/) to track and manage student connections and disconnections.
   - Log and broadcast connection and disconnection events to all connected students.

- **Client-Side:**
   - The client should display real-time updates when students join or leave the class, showing the corresponding socket IDs.

**Expected Outputs:**

- The Class Server should log all connection and disconnection events of students (clients).
- All connected students should receive real-time updates showing which student (socket ID) has joined or left the class.
