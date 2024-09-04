### Assignment: Counter (Express session)

Create a simple counter application using Express.js, TypeScript, and sessions. The application will have two buttons: one to increase the counter and one to decrease it. Each button will have its own URL route to handle the increase or decrease action. The main page will display the current counter value each time.

![/10%20-%20Assets/Counter.png](/10%20-%20Assets/Counter.png)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Medium

**Instructions:**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives:**

- Adding and implementing Express sessions.

---

**Directions**

Set up your Express.js project. Configure session middleware, create routes to display and update a counter, and implement session logic to manage the counter value. Finally, create an EJS template to show the counter and buttons for increasing or decreasing it.

**MVP Requirements: Counter management with Express and EJS**

- **Create the Express Application**
    1. **Configure Session Middleware:**
        - Configure the session middleware in your Express application to manage session data.
    2. **Create Routes:**
        - Create three routes:
            - A root route (`/`) to display the current counter value.
            - An increase route (`/increase`) to increment the counter.
            - A decrease route (`/decrease`) to decrement the counter.
    3. **Implement Session Logic:**
        - Use sessions to store and update the counter value across requests.
- **Create EJS Templates**
    - **Main Page Template (`index.ejs`):**
        - Create an EJS template to display the current counter value and the two buttons for increasing and decreasing the counter.

**Expected Output:**

- The application should be accessible at `http://localhost:3000`.
- The main page should display the current counter value and two buttons.
- Clicking the "Increase" button should increment the counter and refresh the page to show the updated value.
- Clicking the "Decrease" button should decrement the counter and refresh the page to show the updated value.

**Additional Notes:**

- Ensure your session configuration is secure and suitable for your development environment.
- Test each route thoroughly to confirm that the counter updates correctly and persists across requests.