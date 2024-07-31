# Assignment: User Model with Validations

**Objective:**
In this assignment, you will create a User model with validations to ensure data integrity using Sequelize. You will then validate the table schema using MySQL Workbench.

**Estimated Time to Completion:** 60 mins  
**Level of Complexity:** Medium

**Instructions**

**Create the User Model:**

- Define a User model using Sequelize.
- Include attributes such as name, email, and password.
- Apply validations to ensure:
  - name is a non-empty string with a maximum length of 50 characters.
  - email is a valid email address and unique across the table.
  - password is a non-empty string with a minimum length of 8 characters.

**Validate the Model:**

- Ensure that the validation rules are correctly applied by testing various inputs.
- Use Sequelize’s validation methods to verify that the constraints are enforced.

**Verify in MySQL Workbench:**

- Connect to your MySQL database using MySQL Workbench.
- Inspect the User table to ensure that the validations and constraints have been correctly applied.

**Submit Your Work:**

- Share your code repository URL with the implemented User model.
- Provide screenshots of the User table in MySQL Workbench showing the applied validations and constraints.

**Evaluation Criteria & Learning Objectives**

- Define a Sequelize model with appropriate validations.
- Ensure that model validations are applied and enforced correctly.
- Verify the application of constraints and validations in the database schema.

**Directions**

**Define the User Model:**

- Create a Sequelize model for User with attributes: id, name, email, password.
- Apply validations to enforce constraints:
  - name should not be empty and have a maximum length of 50 characters.
  - email should be unique and properly formatted.
  - password should be a non-empty string with a minimum length of 8 characters.

**Test Your Validations:**

- Insert data into the User model and check that invalid data is correctly rejected by Sequelize.

**Verify in MySQL Workbench:**

- Check the User table schema in MySQL Workbench to confirm the applied constraints.

**Submit Your Work:**

- Provide a link to your GitHub repository with the User model code.
- Include screenshots of the User table schema from MySQL Workbench.

**Expected Outputs**

- **Code Repository:** Implementation of the User model with validations.
- **Database Schema:** Screenshot of the User table schema from MySQL Workbench.

**Stretch Requirements:**

- Add additional custom validations.
- Create a test script to automate validation checks.