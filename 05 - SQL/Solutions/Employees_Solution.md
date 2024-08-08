**EMPLOYEES SOLUTION**
1. **Select all employees:**
    - Write a query to select all columns for all employees.
        ```sql
        SELECT * FROM employees;
        ```
2. **Select specific columns:**
    - Write a query to select only the first name, last name, and email of all employees.
        ```sql
        SELECT first_name, last_name, email FROM employees;
        ```
3. **Insert a new employee:**
    - Insert a new employee named "Robert Lee" with an employee number "11", email "robert.lee@example.com", phone number "123-123-1234", hire date "2024-01-01", job ID 1, salary 65000.00, manager ID 1, and department ID 1.
        ```sql
        INSERT INTO employees (employee_id, first_name, last_name, email, phone_number, hire_date, job_id, salary, manager_id, department_id)
        VALUES (11, 'Robert', 'Lee', 'robert.lee@example.com', '123-123-1234', '2024-01-01', 1, 65000.00, 1, 1);
        ```
4. **Insert multiple employees:**  
    - Insert two new employees: "11", "Alice Green", "alice.green@example.com", "234-234-2345", "2024-02-02", job ID 2, salary 60000.00, manager ID 2, department ID 2.
    "12", "Bob White", "bob.white@example.com", "345-345-3456", "2024-03-03", job ID 3, salary 62000.00, manager ID 3, department ID 3.

        ```sql
        INSERT INTO employees (employee_id, first_name, last_name, email, phone_number, hire_date, job_id, salary, manager_id, department_id) 
        VALUES(11, 'Alice', 'Green', 'alice.green@example.com', '234-234-2345', '2024-02-02', 2, 60000.00, 2, 2),(12, 'Bob', 'White', 'bob.white@example.com', '345-345-3456', '2024-03-03', 3, 62000.00, 3, 3);
        ```
5. **Update an employee's salary:**
    - Update the salary of the employee with the email "john.doe@example.com" to 70000.00.
        ```sql
        UPDATE employees
        SET salary = 70000.00
        WHERE email = 'john.doe@example.com';
        ```
6. **Update an employee's department:**
    - Update the department of the employee with the first name "Laura" to department ID 3.
        ```sql
        UPDATE employees
        SET department_id = 3
        WHERE first_name = 'Laura';
        ```
7. **Delete an employee based on email:**
    - Delete the employee with the email "chris.brown@example.com".
        ```sql
        DELETE FROM employees
        WHERE email = 'chris.brown@example.com';
        ```

8. **Select employees with a specific job ID:**
    - Write a query to select all employees with job ID 1.
        ```sql
        SELECT * FROM employees
        WHERE job_id = 1;
        ```
9. **Select employees with a salary greater than a certain amount:**
    - Write a query to select all employees with a salary greater than 60000.00.
        ```sql
        SELECT * FROM employees
        WHERE salary > 60000.00;
        ```
10. **Update multiple columns for an employee:**
    - Update the email and phone number for the employee named "Emily Davis" to "emily.davis@newexample.com" and "987-654-3210", respectively.
        ```sql
        UPDATE employees
        SET email = 'emily.davis@newexample.com', phone_number = '987-654-3210'
        WHERE first_name = 'Emily' AND last_name = 'Davis';
        ```