### Milestone Assignment: Counter Application with JWT

In this assignment, you will create a simple counter application using Express.js and JWT (JSON Web Tokens) to manage and persist the counter value. The application will have two buttons to increase or decrease the counter, with JWT used to handle state across requests.

![../10%20-%20Assets/Counter.png](../10%20-%20Assets/Counter.png)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Medium

**Instructions**

1. **Set Up the Express Application**
    
    *Note: Basic setup for Express.js and TypeScript is assumed.*
    
2. **Create and Configure JWT Middleware**
    - **Install Dependencies:** Install `jsonwebtoken` and `express`.
    - **Implement JWT Middleware:** Create middleware to verify and decode JWT tokens, managing the counter value.
3. **Define Routes**
    - **Root Route (/):** Display the current counter value.
    - **Increase Route (/increase):** Increment the counter and update the JWT token.
    - **Decrease Route (/decrease):** Decrement the counter and update the JWT token.
4. **Create EJS Template**
    - **Main Page Template (index.ejs):** Design an EJS template to display the current counter value and provide buttons for increasing and decreasing the counter.
5. **Implement JWT Logic**
    - **Initialize JWT:** When a counter action is performed, generate a new JWT with the updated counter value and send it to the client.
    - **Verify JWT:** Ensure that JWT is correctly verified on each request to manage counter state.
6. **Submit Your Work:** Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives**

- **JWT Usage:** JWT should correctly manage and persist the counter value.
- **Route Functionality:** Routes should work as expected to display and modify the counter.
- **EJS Display:** The EJS template should correctly show the counter value and buttons.
- **State Persistence:** The counter value should persist across requests.
- **Code Quality:** Code should be clean and well-organized.

**Directions**

1. **Set Up JWT Middleware:** Implement JWT verification and decoding middleware.
2. **Create Routes:** Implement the routes to handle counter actions and manage JWT.
3. **Design the EJS Template:** Create a template to render the counter value and provide buttons for counter actions.
4. **Test Your Application:** Ensure that the counter updates correctly and persists across requests using JWT.

**Expected Outputs**

- **Functional Application:** The application should correctly display the counter value and update it based on user actions.
- **JWT Management:** JWT should correctly manage and persist the counter state.
- **EJS Template:** The counter value should be dynamically rendered on the main page.

**Stretch Requirements**

- **Implement additional validation or error handling.**
- **Add extra features or functionality if desired.**