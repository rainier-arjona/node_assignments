**MULTIPLE TABLES SOLUTION**

1. Perform an INNER JOIN across three tables:
    - Write a query to retrieve all employees along with their department names and project names.
        ```sql
        SELECT 
            employees.first_name, 
            employees.last_name, 
            departments.name AS department_name, 
            projects.name AS project_name
        FROM employees
        INNER JOIN departments ON employees.department_id = departments.id
        INNER JOIN projects ON departments.id = projects.department_id;
        ```
2. Perform an INNER JOIN with a WHERE clause:
    - Write a query to retrieve all employees working on 'Project B' along with their department names.
        ```sql
        SELECT 
            employees.first_name, 
            employees.last_name, 
            departments.name AS department_name
        FROM employees
        INNER JOIN departments ON employees.department_id = departments.id
        INNER JOIN projects ON departments.id = projects.department_id
        WHERE projects.name = 'Project B';
        ```
3. Perform an INNER JOIN with ordering:
    - Write a query to retrieve all employees along with their department names and project names, ordered by department name.
        ```sql
        SELECT 
            employees.first_name, 
            employees.last_name, 
            departments.name AS department_name, 
            projects.name AS project_name
        FROM employees
        INNER JOIN departments ON employees.department_id = departments.id
        INNER JOIN projects ON departments.id = projects.department_id
        ORDER BY departments.name;
        ```
4. Update using INNER JOIN:
    - Write a query to update the email address of all employees in the 'Sales' department to 'sales@company.com'.
        ```sql
        UPDATE employees
        INNER JOIN departments ON employees.department_id = departments.id
        SET employees.email = 'sales@company.com'
        WHERE departments.name = 'Sales';
        ```
5. Update using INNER JOIN with a condition:
    - Write a query to update the phone number of employees working on 'Project A' to '1111111111'.
        ```sql
        UPDATE employees
        INNER JOIN departments ON employees.department_id = departments.id
        INNER JOIN projects ON departments.id = projects.department_id
        SET employees.phone_number = '1111111111'
        WHERE projects.name = 'Project A';
        ```
6. Delete using INNER JOIN with a condition:
    - Write a query to delete all employees who are working on 'Project B'.
        ```sql
        DELETE employees
        FROM employees
        INNER JOIN departments ON employees.department_id = departments.id
        INNER JOIN projects ON departments.id = projects.department_id
        WHERE projects.name = 'Project B';
        ```
7. Complex Update with INNER JOIN:
    - Write a query to update the email addresses of all employees in the 'Human Resources' department to follow the format 'firstname.lastname@hr.com'.
        ```sql
        UPDATE employees
        INNER JOIN departments ON employees.department_id = departments.id
        SET employees.email = CONCAT(LOWER(employees.first_name), '.', LOWER(employees.last_name), '@hr.com')
        WHERE departments.name = 'Human Resources';
        ```
