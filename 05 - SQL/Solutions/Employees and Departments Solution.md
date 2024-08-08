**EMPLOYEES AND DEPARTMENTS SOLUTION**

1. Perform an INNER JOIN:
    - Write a query to retrieve all employees along with their department names.
        ```sql
        SELECT 
            employees.first_name, 
            employees.last_name, 
            employees.email, 
            employees.phone_number, 
            departments.name AS department_name
        FROM employees
        INNER JOIN departments ON employees.department_id = departments.id;
        ```
2. Perform an INNER JOIN with a WHERE clause:
    - Write a query to retrieve all employees in the 'Engineering' department.
        ```sql
        SELECT 
            employees.first_name, 
            employees.last_name, 
            employees.email, 
            employees.phone_number, 
            departments.name AS department_name
        FROM employees
        INNER JOIN departments ON employees.department_id = departments.id
        WHERE departments.name = 'Engineering';
        ```
3. Perform an INNER JOIN with ordering:
    - Write a query to retrieve all employees along with their department names, ordered by department name.
        ```sql
        SELECT 
            employees.first_name, 
            employees.last_name, 
            employees.email, 
            employees.phone_number, 
            departments.name AS department_name
        FROM employees
        INNER JOIN departments ON employees.department_id = departments.id
        ORDER BY departments.name;
        ```
4. Update using INNER JOIN:
    - Write a query to update the phone number of all employees in the 'Sales' department to '9999999999'.
        ```sql
        UPDATE employees
        INNER JOIN departments ON employees.department_id = departments.id
        SET employees.phone_number = '9999999999'
        WHERE departments.name = 'Sales';
        ```
5. Update using INNER JOIN with a condition:
    - Write a query to update the email address of 'Michael Johnson' to 'michael.j@engineering.com'.
        ```sql
        UPDATE employees
        INNER JOIN departments ON employees.department_id = departments.id
        SET employees.email = 'michael.j@engineering.com'
        WHERE employees.first_name = 'Michael' AND employees.last_name = 'Johnson';
        ```
6. Delete using INNER JOIN:
    - Write a query to delete all employees who are in the 'Marketing' department.
        ```sql
        DELETE employees
        FROM employees
        INNER JOIN departments ON employees.department_id = departments.id
        WHERE departments.name = 'Marketing';

        ```
7. Delete using INNER JOIN with a condition:
    - Write a query to delete the employee 'Patricia Wilson'.
        ```sql
        DELETE employees
        FROM employees
        WHERE employees.first_name = 'Patricia' AND employees.last_name = 'Wilson';
        ```