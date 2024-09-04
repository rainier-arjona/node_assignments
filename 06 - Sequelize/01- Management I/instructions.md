### Assignment: Management I

Learn how to define multiple Sequelize models and synchronize them with a MySQL database to create corresponding tables.

![./assets/management_erd.png](./assets/management_erd.png)

**Estimated Time to Completion:** 120 minutes

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Learn how to synchronize models with the database to create the corresponding tables.

---

**Directions**

Set up a Node.js project and initialize Sequelize with MySQL. Create the management_db database and configure Sequelize to connect. Define Employee, Project, and Task models with the specified fields. Synchronize the models to create tables in the database, and optionally insert sample data for testing.

**MVP Requirements: Database Setup and Model Definition**

- **Configure the Database**
    1. Create a MySQL database named `management_db`.
    2. Configure Sequelize to connect to this database using the provided configuration file.
- **Define the Models**
    - *Employee Model:*
        - `id`: Integer, Primary Key, Auto Increment
        - `firstName`: String, not null
        - `lastName`: String, not null
        - `email`: String, unique, not null
        - `hireDate`: Date, not null
        - `salary`: Decimal, not null
    - *Project Model:*
        - `id`: Integer, Primary Key, Auto Increment
        - `name`: String, not null, unique
        - `description`: String
        - `startDate`: Date
        - `endDate`: Date
    - *Task Model:*
        - `id`: Integer, Primary Key, Auto Increment
        - `title`: String, not null
        - `description`: String
        - `status`: String, not null (e.g., 'Not Started', 'In Progress', 'Completed')
        - `dueDate`: Date
- **Synchronize the Models**
    - Use Sequelize’s sync method to create the `Employee`, `Project`, and `Task` tables in the `management_db` database based on your models.
    - Ensure you are calling the models in your synchronization script to register them with Sequelize.
- **Insert Sample Data (Optional but Recommended)**
    - After synchronizing the models, insert sample data into each table to test the setup.

**Expected Outputs:**

- Tables Created: `Employee`, `Project`, `Task`
- Sample Data: (if added) Inserted into each table

**Additional Notes:**

- Ensure that each table accurately reflects the defined model structure.
- Submit screenshots or exports from MySQL Workbench showing the tables and sample data.