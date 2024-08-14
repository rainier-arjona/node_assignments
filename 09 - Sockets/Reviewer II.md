# Assignment: Group Chat Application

In this assignment, you'll build a group chat application using Express.js with TypeScript, Sequelize for database management, JWT for authentication, and Socket.io for real-time communication. The application will allow users to log in, create and manage chat rooms, and communicate in real-time.

![Wireframe](../10%20-%20Assets/ChatRoomwithbe.png)

**Estimated Time to Completion:** 3-4 hours

**Level of Complexity:** High

## Instructions

1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

## Evaluation Criteria & Learning Objectives

- Implement authentication with JWT
- Set up CRUD operations for chat rooms
- Use Sequelize to manage database interactions
- Implement real-time chat functionality with Socket.io

## Directions

### 1. User Authentication

**MVP Requirements:**

- Implement user authentication using JWT.
- Create login and registration endpoints.
- Ensure users are able to authenticate and receive a JWT for subsequent requests.

### 2. Chat Room Management

**MVP Requirements:**

- Rooms: Users should be able to create, read, update, and delete chat rooms.
- Messages: Implement real-time messaging within rooms.
- Room Management: Users should be able to join and leave rooms dynamically.

### 3. CRUD Operations

**MVP Requirements:**

- Chat Rooms: Implement CRUD operations for chat rooms.
- Messages: Ensure that messages are stored and retrieved properly for each room.

### 4. Real-Time Chat

**MVP Requirements:**

- Implement real-time chat functionality using Socket.io.
- Ensure that messages sent in a chat room are broadcasted to all users in that room.
- Implement user connection and disconnection events.

**Stretch Requirements:**

- Allow users to update their profile information.
- Add functionality for users to create their own rooms and manage them.
- Implement JWT refresh tokens for maintaining user sessions.

## Expected Outputs

- A functioning group chat application where users can log in, create and manage chat rooms, and send real-time messages.
- Proper handling of JWT authentication and CRUD operations for chat rooms and messages.

## Additional Notes

- Ensure your code is well-documented and follows best practices for authentication, database operations, and real-time communication.
- Test your application thoroughly to ensure all features work as expected and handle edge cases gracefully.
