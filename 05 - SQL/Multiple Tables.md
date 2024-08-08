### Assignment: Employees Queries II

Now let us practice SELECT with JOIN, INSERT, UPDATE, and DELETE queries that involves multiple related tables.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**
1. Read through the directions below. 
2. Complete the necessary elements as outlined. 
3. Zip the project and submit to [xxxxx] by the due date.

**Evaluation Criteria & Learning Objectives**
- Perform SELECT queries using INNER JOINs
- Perform UPDATE queries involving multiple tables
- Perform DELETE queries involving multiple tables

**Directions**
The following challenges will require you to create the appropriate JOIN queries that will fetch, update, and manipulate data from multiple tables: `employees`, `departments`, and `projects`.

**Setup: Creating the Necessary Tables and Inserting Data**
Use the updated management_db file from the previous exercise.

1. Create the `projects` table and insert data:

    ```sql
    CREATE TABLE IF NOT EXISTS projects (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    department_id INT,
    FOREIGN KEY (department_id) REFERENCES departments(id)
    );

    INSERT INTO projects (name, department_id) VALUES
    ('Project A', 1),
    ('Project B', 2),
    ('Project C', 3),
    ('Project D', 4);
    ```
**MVP Requirements: Basic Queries**
Create a new SQL file and perform the following challenges:

1. Perform an INNER JOIN across three tables:
    - Write a query to retrieve all employees along with their department names and project names.
2. Perform an INNER JOIN with a WHERE clause:
    - Write a query to retrieve all employees working on 'Project B' along with their department names.
3. Perform an INNER JOIN with ordering:
    - Write a query to retrieve all employees along with their department names and project names, ordered by department name.
4. Update using INNER JOIN:
    - Write a query to update the email address of all employees in the 'Sales' department to 'sales@company.com'.
5. Update using INNER JOIN with a condition:
    - Write a query to update the phone number of employees working on 'Project A' to '1111111111'.
6. Delete using INNER JOIN with a condition:
    - Write a query to delete all employees who are working on 'Project B'.
7. Complex Update with INNER JOIN:
    - Write a query to update the email addresses of all employees in the 'Human Resources' department to follow the format 'firstname.lastname@hr.com'.
