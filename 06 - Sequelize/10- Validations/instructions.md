### Assignment: User Model with Validations

In this assignment, you will create a User model with validations to ensure data integrity using Sequelize. You will then validate the table schema using MySQL Workbench.

![../10%20-%20Assets/UserModelValidation.png](../10%20-%20Assets/UserModelValidation.png)

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Understand how to add validations to models to ensure data integrity.

---

**Directions**

1. Create the User Model:
    - Define a User model using Sequelize.
    - Include attributes such as name, email, and password.
    - Apply validations to ensure:
        - **name** is a non-empty string with a maximum length of 50 characters.    
        - **email** is a valid email address and unique across the table.
        - **password** is a non-empty string with a minimum length of 8 characters.
2. Validate the Model:
    - Ensure that the validation rules are correctly applied by testing various inputs.
    - Use Sequelize’s validation methods to verify that the constraints are enforced.
3. Verify in MySQL Workbench:
    - Connect to your MySQL database using MySQL Workbench.
    - Inspect the User table to ensure that the validations and constraints have been correctly applied.
4. Wireframe:
    - A wireframe is provided to help you visualize the registration form and how the user properties (name, email, password) will be presented. Use this as a reference to ensure your implementation aligns with the provided design.
5. Submit Your Work:
    - Provide screenshots of the User table in MySQL Workbench showing the applied validations and constraints.
    - Include a screenshot of the registration form, as shown in the wireframe, demonstrating that the form is properly handling user input and validation feedback.

**MVP Requirements: Defining and Validating the User Model with Sequelize**

- Define the User Model:
    - Create a Sequelize model for User with attributes: id, name, email, password.
    - Apply validations to enforce constraints:
        - name should not be empty and have a maximum length of 50 characters.
        - email should be unique and properly formatted.
        - password should be a non-empty string with a minimum length of 8 characters.
- Test Your Validations:
    - Insert data into the User model and check that invalid data is correctly rejected by Sequelize.
    - Use the provided wireframe to test the registration form and ensure proper validation feedback.
- Verify in MySQL Workbench:
    - Check the User table schema in MySQL Workbench to confirm the applied constraints.

**Expected Outputs**

- **Code Repository:** Implementation of the User model with validations.
- **Database Schema:** Screenshot of the User table schema from MySQL Workbench.
- **Registration Form:** Screenshot of the registration form from your application, matching the provided wireframe.

**Stretch Requirements:**

- Add additional custom validations.