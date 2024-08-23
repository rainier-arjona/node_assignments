### Assignment: Sequelize Migrations and Model Updates

Learn how to create and run migrations in Sequelize to manage database schema changes over time. Update existing models and handle schema modifications using migrations.

![./assets/management_erd.png](./assets/management_erd.png)

**Estimated Time to Completion:** 120 minutes

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives**

- **Create and run Sequelize migrations to manage schema updates:** Learn to create and apply migrations to maintain the database schema over time.
- **Update existing Sequelize models and handle schema changes:** Modify models and synchronize them with the database schema.
- **Validate the changes using MySQL Workbench or a similar tool:** Ensure the schema reflects the desired state after migrations.

**Directions**

**1. Review the Schema**

- Based on the provided images, understand the new schema requirements and how they impact your models.

**2. Update the Models**

- **Delete Two Models:**
    - *Delete `Employee`:* Remove the `Employee` model and its corresponding table from your project.
    - *Delete `Project`:* Remove the `Project` model and its corresponding table from your project.
- **Update the Remaining Model:**
    - *Update `Task`:*
        - Modify the `Task` model to reflect the following changes:
            - *Change `dueDate` Property:* Update the `dueDate` field to be non-nullable (i.e., `allowNull: false`).

![./assets/management_II.png](./assets/management_II.png)

**3. Generate Migrations**

- **Create Migration to Delete Models:**
    - Generate a migration file to drop the `employees` and `projects` tables.
- **Create Migration to Update Remaining Model:**
    - Generate a migration file to apply changes to the `tasks` table, including the modification to the `dueDate` field.

**4. Run Migrations**

- Use the Sequelize CLI to run the migrations and apply the changes to the database.

**5. Validate the Changes**

- Use MySQL Workbench or a similar tool to verify that the database schema has been updated correctly. Ensure that:
    - The `employees` and `projects` tables are removed.
    - The `tasks` table reflects the new schema, including the updated `dueDate` field.

![./assets/updated.png](./assets/updated.png)

**MVP Requirements**

- **Model Files:** Update the Sequelize model files according to the new schema requirements.
- **Migration Files:** Generate and apply migration files for schema updates.
- **Database Schema:** Confirm the updated schema in MySQL Workbench or equivalent tool.

**Expected Outputs**

- **Updated Models:** Reflecting the new schema as per the wireframe.
- **Migration Files:** Correctly managing schema changes.
- **Database Schema:** Updated and verified using MySQL Workbench or similar tool.

**Additional Notes**

- Ensure that all migrations are accurately generated and applied without data loss.
- Submit your updated project files, migration scripts, and validation screenshots or exports.