### Assignment: Student Info II

In this assignment, you will build a simple web application using Node.js, Express, and Sequelize to handle student records. The application will allow users to create new student records and delete existing ones via a web interface.

![../10%20-%20Assets/StudentInfoII.png](../10%20-%20Assets/StudentInfoII.png)

**Estimated Time to Completion:** 2-3 hours

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Learn how to create new records.
- Learn how to delete existing records.

---

**Directions**

1. Project Setup
    - Initialize a new Node.js project and install required dependencies (express, sequelize, and a suitable database adapter like mysql2).

2. Database Configuration
    - Configure Sequelize:
    - Set up Sequelize to connect to your database and test the connection to ensure it is working properly.

3. Model Definition
    - Define a Model:
        - We will be using the data from our first assignment `Student Info I` with the `students_db` schema.

4. Build API Endpoints
    - Create API Endpoints:
        - *POST /students:* Create a new student record based on the data submitted through a form.
        - *DELETE /students/:id:* Delete a student record by ID.

5. Web Interface
    - Create Forms:
        - *Student Creation Form:* Design a form to allow users to create a new student. The form should include fields for `first_name`, `last_name`, `email`, and `age`.
        - Implement a button next to each student record in the table that allows users to delete the student. This button should submit a form to the `/students/delete/:id` endpoint.

6. Validation and Testing
    - Validate Functionality:
        - Ensure that the forms correctly create and delete student records.
        - Test the application using a web browser to ensure the API endpoints and forms work as expected.

**MVP Requirements: Student Management System**

- **Student Creation Form:** Implement a form that allows users to create a new student record.
- **Student Deletion Form:** Implement a form that allows users to delete a student record by ID.
- **API Endpoints:** Implement the necessary endpoints to handle form submissions.

**Expected Outputs**

- **Web Interface:** Functional forms for creating and deleting student records.
- **Database:** Verify that new student records are created and existing records are deleted in the database.

**Additional Notes**

- Ensure that you handle errors gracefully, both on the server-side and client-side.
- Include any relevant screenshots or exports showing the web application in action.