### Assignment: Debugging Express Application (Student Enrollment)

In this assignment, you'll practice debugging by identifying and fixing issues in a provided Express application. The application handles student enrollment data and displays it on a webpage. Your goal is to ensure that the application functions correctly according to the requirements.

**Estimated Time to Completion:** 60 minutes

**Level of Complexity:** Medium

**Instructions**

Below is the provided code with intentional errors. Debug and correct the issues as described.

[Download here.](https://drive.google.com/file/d/1WAMy0bWNr8u7h9kD1HrOZ1MjMmldvPtz/view?usp=sharing)

1. **Review the Provided Code:**
    - The code files you will be working with include `index.ejs`, `edit.ejs`, `server.ts`, and `model/enrollment.ts`.
    - Carefully read through the code to understand its functionality and identify any potential issues.
2. **Identify and Fix Issues:**
    - *In `index.ejs`:*
        - Check the placeholders and syntax for displaying student data within the table. Ensure correct EJS syntax is used for dynamic data rendering.
        - Verify that the form action method and input names match the server-side logic.
    - *In `server.ts`:*
        - Inspect the route handlers for managing enrollment data. Ensure data retrieval and saving to the database are functioning correctly.
        - Validate the session and database configuration to avoid errors when retrieving student information.
        - Check for potential issues in Sequelize model usage, particularly in the `update` and `delete` routes.
    - *In `model/enrollment.ts`:*
        - Review the Sequelize model definition for the `Enrollment` table. Ensure that the model attributes and associations are correctly defined.
        - Check for any syntax errors or misconfigurations in the model that could affect CRUD operations.
3. **Test the Application:**
    - Run the server and test the application by adding, editing, and deleting student records.
    - Ensure data is correctly displayed on the homepage (`/`) and that form submissions work as expected.
4. **Submit Your Work:**
    - Submit your updated code to your GitHub repository.
    - Include a brief description of the issues you identified and the fixes you implemented.

**Evaluation Criteria & Learning Objectives**

- Correctly identify and fix issues related to EJS rendering and form handling.
- Ensure proper CRUD operations using Sequelize models.
- Verify session handling and data retrieval within Express routes.
- Correctly define and configure Sequelize models for database interactions.

**Hints for Debugging**

- EJS Placeholders: Verify that placeholders use the correct `<%= %>` syntax for outputting values and check that the correct property names are being referenced.
- Form Handling: Ensure that form methods (`GET`, `POST`) match the server routes and that the input fields are correctly named.
- Sequelize Issues: Look for potential errors in model handling, such as incorrect attribute names or missing model methods (e.g., `save`, `destroy`).
- Model Definition: Ensure that Sequelize model attributes and data types are correctly defined, and check for any missing associations or validation rules.

Good luck, and happy debugging!