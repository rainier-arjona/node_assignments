### Assignment: Debugging [Socket.io](http://socket.io/) Issues

In this debugging assignment, you will identify and fix issues related to [Socket.io](http://socket.io/) in a multiplayer game application. The application features real-time chat, player movement, and character management.

**Estimated Time to Completion:** 5 hours

**Level of Complexity:** High

**Instructions**

1. **Setup:**
    - Download the code snippets from the provided link: [Download here](https://drive.google.com/file/d/1-Cy0nJocM4pnGxoqnMbNQjxXBYYanKk7/view?usp=sharing).
    - Install the necessary dependencies using:
        
        ```
        npm install
        
        ```
        
2. **Application Overview:**
    - The application is a multiplayer game where players control ghost characters and communicate via a chat interface.
    - Players should be able to move characters around and send chat messages.
    - Players should see real-time updates for other players' movements, chat messages, and changes in the player list.
3. **Debugging Tasks:**
    - **Fix Broadcasting Issues:** Review and correct the [Socket.io](http://socket.io/) `emit` and `broadcast` events in the `socket.ts` file to ensure the following functionalities work as intended:
        - **Movement Updates:** Ensure that when a player moves, all other players see this update, not just the player who moved.
        - **Chat Messages:** Confirm that chat messages are visible to all players, not just the sender.
        - **Player List Updates:** Make sure that updates to the list of players are broadcasted to all connected clients.
        - **Player Disconnections:** Verify that when a player disconnects, all remaining players are informed and updated.
4. **Expected Outputs:**
    - Correct movement and chat functionality where updates are visible to all players.
    - Proper handling of player list updates and disconnections.
5. **Stretch Requirements** (Optional):
    - Implement additional features like private messaging or notifications.
    - Improve the visual representation of player movements or chat messages.
6. **Submission Instructions:**
    - Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives**

- **Technical Accuracy:** Ensure all [Socket.io](http://socket.io/) events (`emit`, `broadcast`) are correctly implemented, providing proper real-time functionality for player movements, chat messages, and player list updates.
- **Comprehensive Debugging:** Demonstrate a strong understanding of [Socket.io](http://socket.io/) by successfully identifying and fixing all real-time communication issues.
- **Clean Code & Best Practices:** The code should be well-structured, clearly commented, and follow best practices for maintainability and extensibility.
- **User Experience:** Ensure the game provides a smooth and responsive real-time experience, with timely updates on movements, chat, and player statuses.
- **Robustness:** Implement proper error handling and ensure the application gracefully manages player connections and disconnections.

**Directions**

1. **Examine the Provided Code:**
    - Review the `socket.ts` and `index.js` files to understand how the server and client interact using [Socket.io](http://socket.io/).
2. **Identify and Correct Issues:**
    - Look for incorrect or missing `emit` and `broadcast` calls.
    - Apply necessary changes to ensure intended broadcast behavior is achieved.
3. **Test the Application:**
    - Thoroughly test the application to confirm that the changes resolve the issues.
    - Ensure movement updates, chat messages, player list updates, and disconnections are properly handled across all connected clients.

**Files to Review and Debug**

- `socket.ts` (server-side [Socket.io](http://socket.io/) code)
- `index.js` (client-side [Socket.io](http://socket.io/) code)
- `index.ejs` (HTML structure and inclusion of scripts)

**Expected Outputs**

- **Real-Time Movement:** Players’ movement updates are broadcasted to and visible by all connected clients.
- **Chat Functionality:** Chat messages are sent and received by all players in real time.
- **Player List Management:** The player list is accurately updated for all players when new players join or existing players disconnect.
- **Disconnection Handling:** Disconnections are properly handled, and remaining players are informed and updated accordingly.