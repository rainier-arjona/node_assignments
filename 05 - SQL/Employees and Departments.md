### Assignment: Employees Queries II

Let's focused on performing JOIN operations between two tables, along with UPDATE and DELETE operations.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**
1. Read through the directions below. 
2. Complete the necessary elements as outlined. 
3. Zip the project and submit to [xxxxx] by the due date.

**Evaluation Criteria & Learning Objectives**
- Perform SELECT queries using INNER JOINs between two tables
- Perform UPDATE queries involving two tables
- Perform DELETE queries involving two tables

**Directions**
The following challenges will require you to create the appropriate JOIN queries that will fetch, update, and manipulate data from the `employees` and `departments` tables.

**Setup: Creating the Necessary Tables and Inserting Data**
Use the management_db from the previous exercise.

1. Create the `departments` table and insert data:

    ```sql
        CREATE TABLE IF NOT EXISTS departments (
            id INT AUTO_INCREMENT PRIMARY KEY,
            name VARCHAR(100) NOT NULL
        );

        INSERT INTO departments (name) VALUES
        ('Sales'),
        ('Engineering'),
        ('Human Resources'),
        ('Marketing');
    ```

**MVP Requirements: Basic Queries**
Create a new SQL file and perform the following challenges:
1. Perform an INNER JOIN:
    - Write a query to retrieve all employees along with their department names.
2. Perform an INNER JOIN with a WHERE clause:
    - Write a query to retrieve all employees in the 'Engineering' department.
3. Perform an INNER JOIN with ordering:
    - Write a query to retrieve all employees along with their department names, ordered by department name.
4. Update using INNER JOIN:
    - Write a query to update the phone number of all employees in the 'Sales' department to '9999999999'.
5. Update using INNER JOIN with a condition:
    - Write a query to update the email address of 'Michael Johnson' to 'michael.j@engineering.com'.
6. Delete using INNER JOIN:
    - Write a query to delete all employees who are in the 'Marketing' department.
7. Delete using INNER JOIN with a condition:
    - Write a query to delete the employee 'Patricia Wilson'.
