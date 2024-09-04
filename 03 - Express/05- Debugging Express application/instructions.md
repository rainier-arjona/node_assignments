## Assignment: Debugging Assignment

In this assignment, you'll identify and fix errors in a given Express TypeScript application. The goal is to ensure that the application runs correctly after resolving the issues.

**Estimated Time to Completion:** 60 minutes

**Level of Complexity:** Medium

**Instructions:**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives:**

- Demonstrate your ability to debug and resolve issues in an Express TypeScript application.
- Confirm that the server is set up and operating correctly.
- Ensure that static assets and EJS templates are correctly served.
- Validate that session management and routing operate as specified.

---

**Directions:**

- **Review and Fix the Provided Code**
    - Below is the code with intentional errors. Debug and correct these issues as described.
    
    [Download here.](https://drive.google.com/file/d/1uEhUEYV7-2JpXN4tJXUtU-FzgK0OeAcR/view?usp=sharing)

**MVP Requirements: Debugging and Enhancing Static Asset Handling, View Rendering, and Session Management**

- **Functionality Requirements**
    - Ensure the application:
        - Serves CSS and other static assets correctly from the static directory.
        - Properly renders the `index.ejs` view with the visitor count and message.
        - Maintains and updates the session count on each visit, with functionality to reset or decrement the count.
        - Correctly handles routes `/`, `/reset`, and `/repeat`.

**Hints for Debugging:**

- **Static Files:** Verify that the path to the static files directory is correct. Ensure the static folder is properly set up in the file structure.
- **Session Data Types:** Ensure that session data types are consistent throughout the application, and fix any type-related issues.
- **EJS Template Path:** Check if the path to the EJS templates (views directory) is correctly set up and that the template is rendering as expected.