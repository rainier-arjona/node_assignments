Assignment: Creating and Deleting Student Records
# Assignment: Student Info II

In this assignment, you will build a simple web application using Node.js, Express, and Sequelize to handle student records. The application will allow users to create new student records and delete existing ones via a web interface.

![Wireframe](../assets/Student%20Info%20II.png)

**Estimated Time to Completion:** 2-3 hours

**Level of Complexity:** Medium

## Instructions

1. Read through the directions below. Note: You will be provided with any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Zip the project and submit to [XXXXX] by the due date.

## Evaluation Criteria & Learning Objectives

- Implement basic CRUD operations (Create and Delete) using Sequelize ORM.
- Develop a simple web interface using Express to interact with the database.
- Validate functionality through form submissions and database changes.

## Directions

For this assignment, you will create a web application to manage student records. Follow the steps below to complete the assignment:

### Project Setup

1. Initialize a new Node.js project and install required dependencies (express, sequelize, and a suitable database adapter like mysql2).

### Database Configuration

1. Configure Sequelize:
    - Set up Sequelize to connect to your database and test the connection to ensure it is working properly.

### Model Definition

1. Define a Model:
    - We will be using the data from our first assignment `Student Info I` with `students_db` schema.

### Build API Endpoints

1. Create API Endpoints:
    - POST /students: Create a new student record based on the data submitted through a form.
    - DELETE /students/:id: Delete a student record by ID.

### Web Interface

1. Create Forms:
    - Student Creation Form: Design a form to allow users to create a new student. The form should include fields for first_name, last_name, email, and age.
    - Student Deletion Form: Design a form to delete an existing student. The form should include a field for entering the student ID to be deleted.

### Validation and Testing

1. Validate Functionality:
    - Ensure that the forms correctly create and delete student records.
    - Test the application using a web browser to ensure the API endpoints and forms work as expected.

## MVP Requirements

- Student Creation Form: Implement a form that allows users to create a new student record.
- Student Deletion Form: Implement a form that allows users to delete a student record by ID.
- API Endpoints: Implement the necessary endpoints to handle form submissions.

## Expected Outputs

- Web Interface: Functional forms for creating and deleting student records.
- Database: Verify that new student records are created and existing records are deleted in the database.

## Additional Notes

- Ensure that you handle errors gracefully, both on the server-side and client-side.
- Include any relevant screenshots or exports showing the web application in action.

