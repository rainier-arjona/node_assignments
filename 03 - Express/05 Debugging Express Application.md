## Assignment: Debugging Assignment

In this assignment, you'll identify and fix errors in a given Express TypeScript application. The goal is to ensure that the application runs correctly after resolving the issues.

**Estimated Time to Completion:** 60 minutes

**Level of Complexity:** Medium

**Instructions:**

1. Review the provided code, which contains several intentional errors.
2. Identify and fix these errors to make the application run as expected.
3. Submit your GitHub URL with the corrected code by the due date.

**Evaluation Criteria & Learning Objectives:**

- **Correctly identify and fix errors in the Express application:** Demonstrate your ability to debug and resolve issues in an Express TypeScript application.
- **Ensure proper configuration and functionality of the Express server:** Confirm that the server is set up and operating correctly.
- **Verify that static files and views are served correctly:** Ensure that static assets and EJS templates are correctly served.
- **Confirm that session management and routing work as intended:** Validate that session management and routing operate as specified.

**Directions:**

1. **Review and Fix the Provided Code**
    - Below is the code with intentional errors. Debug and correct these issues as described.
    
    [Download here.](https://drive.google.com/file/d/1uEhUEYV7-2JpXN4tJXUtU-FzgK0OeAcR/view?usp=sharing)
    
2. **Functionality Requirements**
    - Ensure the application:
        - Serves CSS and other static assets correctly from the static directory.
        - Properly renders the `index.ejs` view with the visitor count and message.
        - Maintains and updates the session count on each visit, with functionality to reset or decrement the count.
        - Correctly handles routes `/`, `/reset`, and `/repeat`.

**Hints for Debugging:**

- **Static Files:** Verify that the path to the static files directory is correct. Ensure the static folder is properly set up in the file structure.
- **Session Data Types:** Ensure that session data types are consistent throughout the application, and fix any type-related issues.
- **EJS Template Path:** Check if the path to the EJS templates (views directory) is correctly set up and that the template is rendering as expected.