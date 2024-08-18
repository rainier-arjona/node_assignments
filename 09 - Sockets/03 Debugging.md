# Debugging Assignment: Socket.io Issues

In this debugging assignment, you will identify and fix issues related to Socket.io in a multiplayer game application. The application features real-time chat, player movement, and character management.

**Estimated Time to Completion:** 5 hours

**Level of Complexity:** High

**Instructions**:

Below is the provided code with intentional errors. Debug and correct the issues as described.

[Download here.](https://drive.google.com/file/d/1-Cy0nJocM4pnGxoqnMbNQjxXBYYanKk7/view?usp=sharing)

1. **Setup**: Download the code snippets from the provided links. Install the necessary dependencies using `npm install`.
2. **Application Overview**:
    - The application is a multiplayer game where players control ghost characters and communicate via a chat interface.
    - Players are able to move characters around and send chat messages.
    - Players should see real-time updates for other players' movements, chat messages, and changes in the player list.
3. **Debugging Tasks**:
    - **Fix Broadcasting Issues**: Review and correct the Socket.io `emit` and `broadcast` events in the `socket.ts` file so that the following functionality works as intended:
        - **Movement Updates**: Ensure that when a player moves, all other players see this update, not just the player who moved.
        - **Chat Messages**: Confirm that chat messages are visible to all players, not just the sender.
        - **Player List Updates**: Make sure that updates to the list of players are broadcasted to all connected clients.
        - **Player Disconnections**: Verify that when a player disconnects, all remaining players are informed and updated.
4. **Expected Outputs**:
    - Correct movement and chat functionality where updates are visible to all players.
    - Proper handling of player list updates and disconnections.
5. **Stretch Requirements** (Optional):
    - Implement additional features like private messaging or notifications.
    - Improve the visual representation of player movements or chat messages.

**Evaluation Criteria & Learning Objectives**:

- **Correctness**: Ensure that all debugging tasks are completed and functionalities work as expected.
- **Understanding**: Demonstrate a clear understanding of how Socket.io broadcasting and emitting work.
- **Code Quality**: Maintain clean and well-commented code with good practices.

**Directions**:

1. Begin by examining the provided code in `socket.ts` and `index.js`.
2. Identify where `emit` and `broadcast` calls are incorrect or missing.
3. Apply fixes to ensure that the intended broadcast behavior is achieved.
4. Test the application thoroughly to confirm that the changes resolve the issues.

**Files to Review and Debug**:

- `socket.ts` (for server-side Socket.io code)
- `index.js` (for client-side Socket.io code)
- `index.ejs` (for the HTML structure and inclusion of scripts)
