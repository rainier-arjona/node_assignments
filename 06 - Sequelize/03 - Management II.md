# Employees II (Seuqelize)

Learn how to create and run migrations in Sequelize to manage database schema changes over time. Update existing models and handle schema modifications using migrations.

---

![ERD](./assets/management_erd.png)

**Estimated Time to Completion:** 120 minutes

**Level of Complexity:** Medium

**Instructions**

1. **Read through the directions below. Note: you will be provided any necessary files on which to work.**
2. **Complete the necessary elements as outlined.**
3. **Zip the project and submit to [XXXXX] by the due date.**

**Evaluation Criteria & Learning Objectives**

- Create and run Sequelize migrations to manage schema updates.
- Update existing Sequelize models and handle schema changes.
- Validate the changes using MySQL Workbench or a similar tool.

---

**Directions**

You have previously created a database schema with three models. For this assignment, you will modify the schema as follows:

1. **Review the Provided Wireframe:**
    - You will be given a wireframe of a simple application. Review the wireframe to understand the updated schema requirements.
2. **Update the Models:**
    - **Delete Two Models:**
        - From the previous assignment, remove two of the models (`Employee`, `Project`, or `Task`).
    - **Update the Remaining Model:**
        - Update the remaining model to reflect the changes required by the new schema (e.g., add, remove, or modify fields).
3. **Generate Migrations:**
    - Create a migration file to delete the two models from the database.
    - Create another migration file to apply the changes to the remaining model based on the updated schema.
4. **Run Migrations:**
    - Run the migrations using Sequelize CLI to apply the changes to the database.
5. **Validate the Changes:**
    - Use MySQL Workbench or a similar tool to verify that the changes have been applied correctly to the database schema.
    

**MVP Requirements:**

- **Model Files:**
    - Generate Sequelize model files based on the wireframe, including relationships if applicable.
- **Migration Files:**
    - Create and apply migrations to delete two models and update the remaining model.
    

**Expected Outputs:**

- **Updated Models:** Reflecting the new schema as per the wireframe.
- **Migration Files:** Correctly handling schema changes.
- **Database Schema:** Updated in MySQL Workbench or equivalent tool.

**Additional Notes:**

- Ensure that all migrations are correctly generated and applied without data loss.
- Submit your updated project files, migration scripts, and validation screenshots or exports.
