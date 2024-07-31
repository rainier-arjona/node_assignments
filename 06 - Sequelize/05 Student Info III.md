Assignment: Updating Student Records
## Assignment: Updating Student Records

In this assignment, you will enhance your existing web application by adding functionality to update student records. You will use Node.js, Express, and Sequelize to implement the update feature, allowing users to modify existing student records through a web interface. Instead of using PUT or PATCH, you will use POST with a custom action to handle updates.

![Wireframe](./assets/Student%20Info%20III.png)

**Estimated Time to Completion:** 1-2 hours  
**Level of Complexity:** Medium

### Instructions

1. Read through the directions below. Note: You will be provided with any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Zip the project and submit it to [XXXXX] by the due date.

### Evaluation Criteria & Learning Objectives

- Implement an update operation using the POST method with a custom action.
- Develop a web interface that allows users to update student records.
- Ensure proper validation and error handling for updates.

### Directions

For this assignment, you will extend your web application to include functionality for updating student records. Follow the steps below to complete the assignment:

#### Project Setup

1. Use Existing Project: Use the existing Node.js project from the previous assignment `Student Info II`.

#### Model and Database Configuration

1. Review Configuration: Ensure Sequelize is properly configured and the Student model is defined as in the previous assignment.

#### Build API Endpoint

1. Create or Modify API Endpoint: POST /students/update/
    - Implement an endpoint to handle student record updates using POST with a custom route. This endpoint should handle updating the `first_name`, `last_name`, `email`, and `age` fields based on the data submitted through a form. The endpoint should support partial updates, so only the fields provided in the request body will be updated.

#### Web Interface

1. Create or Modify Forms: Student Update Form
    - Design a form that allows users to update an existing student record. The form should include fields for `first_name`, `last_name`, `email`, and `age`. Ensure that the form pre-fills with the existing data for the student to be updated.

#### Validation and Testing

1. Validate Functionality:
    - Ensure that the update form correctly updates student records in the database.

### MVP Requirements

- Student Update Form: Implement a form that allows users to update an existing student record.
- API Endpoint: Implement the POST /students/update/:id endpoint to handle update requests.

### Expected Outputs

- Web Interface: A functional update form for modifying student records.
- Database: Verify that student records are updated correctly in the database.

### Additional Notes

- Handle errors gracefully, both on the server-side and client-side.
- Include any relevant screenshots or exports showing the update functionality in action.
