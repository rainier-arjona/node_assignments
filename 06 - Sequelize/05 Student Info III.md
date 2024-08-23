### Assignment: Updating Student Records

In this assignment, you will enhance your existing web application by adding functionality to update student records. You will use Node.js, Express, and Sequelize to implement the update feature, allowing users to modify existing student records through a web interface. Instead of using PUT or PATCH, you will use POST with a custom action to handle updates.

![../10%20-%20Assets/StudentInfoIII.png](../10%20-%20Assets/StudentInfoIII.png)

**Estimated Time to Completion:** 1-2 hours

**Level of Complexity:** Mediumgit 

**Instructions**

1. Read through the directions below. Note: You will be provided with any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives**

- **Implement an update operation using the POST method with a custom action.**
- **Develop a web interface that allows users to update student records.**
- **Ensure proper validation and error handling for updates.**

**Directions**

**1. Project Setup**

- *Use Existing Project:* Use the existing Node.js project from the previous assignment `Student Info II`.

**2. Model and Database Configuration**

- *Review Configuration:* Ensure Sequelize is properly configured and the Student model is defined as in the previous assignment.

**3. Build API Endpoint**

- *Create or Modify API Endpoint: POST /students/update/:id*
    - Implement an endpoint to handle student record updates using POST with a custom route. This endpoint should handle updating the `first_name`, `last_name`, `email`, and `age` fields based on the data submitted through a form. The endpoint should support partial updates, so only the fields provided in the request body will be updated.

**4. Web Interface**

- *Create or Modify Forms: Student Update Form*
    - Design a form that allows users to update an existing student record. The form should include fields for `first_name`, `last_name`, `email`, and `age`. Ensure that the form pre-fills with the existing data for the student to be updated.

**5. Validation and Testing**

- *Validate Functionality:*
    - Ensure that the update form correctly updates student records in the database.

**MVP Requirements**

- **Student Update Form:** Implement a form that allows users to update an existing student record.
- **API Endpoint:** Implement the POST /students/update/:id endpoint to handle update requests.

**Expected Outputs**

- **Web Interface:** A functional update form for modifying student records.
- **Database:** Verify that student records are updated correctly in the database.

**Additional Notes**

- Handle errors gracefully, both on the server-side and client-side.
- Include any relevant screenshots or exports showing the update functionality in action.