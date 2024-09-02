### Milestone Assignment: CRUD, One-to-Many with Validations

In this milestone assignment, you will enhance the Classroom and Student application by incorporating validation into your Sequelize models and routes. You will implement and manage a one-to-many relationship between Classrooms and Students, ensuring data integrity through validations.

![../10%20-%20Assets/ClassroomManagementSystem.png](../10%20-%20Assets/ClassroomManagementSystem.png)

**Estimated Time to Completion:** 90 mins

**Level of Complexity:** Medium

**Instructions**

1. **Define Models:**
    
    **Classroom Model:**
    
    - Define attributes such as id and name.
    - Implement validation to ensure that name is a non-empty string.
    
    **Student Model:**
    
    - Define attributes such as id, name, and classroomId (foreign key to Classroom).
    - Implement validation to ensure that name is a non-empty string and that classroomId refers to a valid Classroom.
2. **Set Up Relationships:**
    - Establish a one-to-many relationship where a Classroom can have many Students, and each Student belongs to one Classroom.
3. **Implement Routes:**
    
    **/index:** Display all classrooms.
    
    - Implement functionality so that clicking on a classroom shows all students assigned to that classroom.
    
    **/class/new:** Route to create a new classroom with validation.
    
    **/student/new:** Route to create a new student and assign them to a classroom with validation.
    
4. **Implement CRUD Operations:**
    
    **Read:**
    
    - Retrieve all students for a specific classroom.
    - Retrieve all classrooms.
    - Retrieve all students.
    
    **Create:**
    
    - Add new classrooms with validation.
    - Add new students with validation and assign them to existing classrooms.
    
    **Delete:**
    
    - Remove classrooms (ensure proper handling of associated students).
    - Remove students.
5. **Validate:**
    - Implement and test validations for model attributes and relationships.
    - Ensure that all CRUD operations respect validations and handle errors appropriately.
6. **Submit Your Work:**
    - Provide a link to your code repository with the completed assignment.
    - Include any relevant documentation or screenshots to demonstrate your implementation.

**Sample Code Guidance**

- **Model Definitions:**
    
    **Classroom Model:**
    
    - Attributes: id (auto-generated), name (string, required).
    
    **Student Model:**
    
    - Attributes: id (auto-generated), name (string, required), classroomId (integer, foreign key, required).
- **Relationships:**
    - Use Sequelize's `hasMany` and `belongsTo` methods to set up the one-to-many relationship between Classroom and Student.
- **Routes Overview:**
    - **/index:** Render a list of all classrooms.
    - **/class/new:** Form for creating a new classroom with validation.
    - **/student/new:** Form for creating a new student with validation and assigning them to a classroom.
    - **/class/:id/students:** Show all students for a specific classroom.

**Evaluation Criteria & Learning Objectives**

- **Model Definitions:** Accurately define the Classroom and Student models with proper validation rules.
- **Relationships:** Correctly implement the one-to-many relationship between the Classroom and Student models using Sequelize.
- **CRUD Operations:** Develop functional routes for creating, reading, updating, and deleting Classrooms and Students, ensuring all operations handle validations effectively.
- **Data Integrity:** Maintain data integrity through robust validation and error handling in both the models and CRUD operations.

**Directions**

1. **Define Models and Relationships:**
    - Create Classroom and Student models with appropriate attributes and validations.
    - Set up the one-to-many relationship using Sequelize.
2. **Implement Routes and CRUD Operations:**
    - Set up routes for creating, reading, updating, and deleting records.
    - Ensure that routes respect model validations and handle errors gracefully.
3. **Test the Implementation:**
    - Verify that all routes and CRUD operations work correctly with validations.
    - Test that invalid data is properly rejected and appropriate errors are returned.

**Expected Outputs**

- **Model Definitions:** Correctly defined Classroom and Student models with validation rules.
- **CRUD Operations:** Functional routes for creating, reading, updating, and deleting records with validation.
- **Data Validation:** Proper handling of data integrity and error scenarios.

**Stretch Requirements**

- Implement additional validation or error handling as needed.
- Enhance functionality with more complex queries or features if desired.