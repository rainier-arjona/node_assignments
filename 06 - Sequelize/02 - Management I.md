# Assignment: Management I

Learn how to define multiple Sequelize models and synchronize them with a MySQL database to create corresponding tables.

![MySQL Workbench](./assets/management_erd.png)

**Estimated Time to Completion:** 120 minutes

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided with any necessary files on which to work.
2. Complete the required elements as outlined.
3. Zip the project and submit it to [XXXXX] by the due date.

**Evaluation Criteria & Learning Objectives**

- Define three Sequelize models.
- Synchronize the models with a MySQL database to create corresponding tables.
- Validate the creation of the tables using MySQL Workbench.
---
**Assignment Details**

You are tasked with creating a basic database schema for a management system. The schema will include tables for storing details related to Employee, Project, and Task.

**Objectives:**

**Setup the Project:**

- Create a new Node.js project.
- Install the necessary dependencies: sequelize, mysql2, and sequelize-cli.
- Initialize Sequelize in your project.

**Database Configuration:**

- Create a MySQL database named `management_db`.
- Configure Sequelize to connect to this database using the provided configuration file.

**Define the Models:**

**Employee Model:**

- `id`: Integer, Primary Key, Auto Increment
- `firstName`: String, not null
- `lastName`: String, not null
- `email`: String, unique, not null
- `hireDate`: Date, not null
- `salary`: Decimal, not null

**Project Model:**

- `id`: Integer, Primary Key, Auto Increment
- `name`: String, not null, unique
- `description`: String
- `startDate`: Date
- `endDate`: Date

**Task Model:**

- `id`: Integer, Primary Key, Auto Increment
- `title`: String, not null
- `description`: String
- `status`: String, not null (e.g., 'Not Started', 'In Progress', 'Completed')
- `dueDate`: Date

**Synchronize the Models:**

- Use Sequelize’s sync method to create the `Employee`, `Project`, and `Task` tables in the `management_db` database based on your models.
- Ensure you are calling the models in your synchronization script to register them with Sequelize.

**Insert Sample Data (Optional but Recommended):**

- After synchronizing the models, insert sample data into each table to test the setup.

**Expected Outputs:**

- Tables Created: `Employee`, `Project`, `Task`
- Sample Data: (if added) Inserted into each table

**Additional Notes:**

- Ensure that each table accurately reflects the defined model structure.
- Submit screenshots or exports from MySQL Workbench showing the tables and sample data.
