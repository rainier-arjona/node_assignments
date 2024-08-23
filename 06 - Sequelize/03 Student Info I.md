### Assignment: Student Info I

Learn how to read data from a Sequelize-managed database using various query techniques.

![./assets/Student_Info.png](./assets/Student_Info.png)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives**

- **Perform SELECT queries to read data from the database.**
- **Use Sequelize ORM queries to retrieve data according to specified conditions.**

**Directions**

**1. Dummy Data**

- Create a SQL script to populate the `students_db` schema with the following data:
    
    ```sql
    -- Create Students Table
    CREATE TABLE Students (
        id INT AUTO_INCREMENT PRIMARY KEY,
        first_name VARCHAR(100) NOT NULL,
        last_name VARCHAR(100) NOT NULL,
        email VARCHAR(255) UNIQUE NOT NULL,
        age INT NOT NULL,
        createdAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        updatedAt TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
    );
    
    -- Insert Data with Dummy Timestamps
    INSERT INTO Students (first_name, last_name, email, age, createdAt, updatedAt) VALUES
    ('Alvin', 'Cruz', 'john.doe@gmail.com', 22, '2023-01-01 10:00:00', '2023-01-01 10:00:00'),
    ('Jonathan', 'Aguirre', 'jane.smith@gmail.com', 20, '2023-01-02 11:00:00', '2023-01-02 11:00:00'),
    ('Arjon', 'Gellido', 'emily.johnson@gmail.com', 21, '2023-01-03 12:00:00', '2023-01-03 12:00:00'),
    ('Michael', 'Calisto', 'michael.williams@gmail.com', 23, '2023-01-04 13:00:00', '2023-01-04 13:00:00'),
    ('Sarah', 'Ramirez', 'sarah.brown@gmail.com', 22, '2023-01-05 14:00:00', '2023-01-05 14:00:00');
    
    ```
    

**2. Queries**

- Using Sequelize, complete the following queries to retrieve data from the `Students` table:
    1. *Retrieve All Students:*
        - Fetch all students from the `Students` table.
    2. *Find Student by ID:*
        - Fetch a student by ID when the ID link is clicked.
    3. *Find Students by Age:*
        - Fetch all students who are 22 years old.
    4. *Find Student by Last Name:*
        - Fetch a student with the last name Smith.
    5. *Count Total Students:*
        - Count the total number of students in the table.

**3. Sample Code Snippets**

- Use the following sample code snippets as guidance:
    
    ```tsx
    // Sample query to fetch all students
    const allStudents = await Student.findAll({
        attributes: ['id', 'first_name', 'last_name', 'email']
    });
    
    // Sample query to find a student by ID
    const studentById = await Student.findOne({
        where: { id: :id },   // Replace :id with actual student ID
        attributes: ['first_name', 'last_name', 'email']
    });
    
    ```
    

**Expected Outputs**

- **Students List:** A list of all students with their `id`, `first_name`, `last_name`, and `email`.
- **Buttons to Perform the Challenges:** Interface elements to execute each query challenge.

**Additional Notes**

- Ensure that you validate your queries using MySQL Workbench or a similar tool.
- Submit your query files and any screenshots or exports showing the results.
