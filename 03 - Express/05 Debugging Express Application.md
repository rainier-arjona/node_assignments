Debugging Assignment
## Milestone: Debugging Assignment

In this assignment, you'll identify and fix errors in a given Express TypeScript application. The goal is to ensure that the application runs correctly after resolving the issues.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

### Instructions

1. Review the provided code, which contains several intentional errors.
2. Identify and fix these errors to make the application run as expected.
3. Submit your GitHub URL with the corrected code by the due date.

### Evaluation Criteria & Learning Objectives

- Correctly identify and fix errors in the Express application
- Ensure proper configuration and functionality of the Express server
- Verify that static files and views are served correctly
- Confirm that session management and routing work as intended

### Directions

Below is the provided code with intentional errors. Debug and correct the issues as described.

**[file]**

#### Application Functionality

Once the errors are fixed, the application should:

- Serve Static Files: Serve CSS and other static assets correctly from the static directory.
- Render Views: Properly render the index.ejs view with the visitor count and message.
- Session Management: Maintain and update the session count on each visit, with functionality to reset or decrement the count as described.
- Routing: Correctly handle routes /, /reset, and /repeat according to the expected behavior.

#### Hints for Debugging

- Static Files: Verify that the path to the static files directory is correct. Ensure the static folder is properly set up in the file structure.
- Session Data Types: Ensure that session data types are consistent throughout the application, and fix any type-related issues.
- EJS Template Path: Check if the path to the EJS templates (views directory) is correctly set up and that the template is rendering as expected.