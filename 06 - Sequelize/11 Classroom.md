# Assignment: Query One-to-Many Relationships with ORM

## Objective:
In this assignment, you will work with Sequelize to implement and query a one-to-many relationship between two models: Classroom and Student. Your tasks will include creating, reading, and deleting records while managing these relationships effectively.

![Wireframe](./assets/ClassroomManagementSystem.png)

**Estimated Time to Completion:** 90 mins  
**Level of Complexity:** Medium

## Instructions

### Define Models:

**Classroom Model:**
- Define attributes such as id and name.

**Student Model:**
- Define attributes such as id, name, and classroomId (foreign key to Classroom).

### Set Up Relationships:
- Establish a one-to-many relationship where a Classroom can have many Students, and each Student belongs to one Classroom.

![ERD](./assets/students_erd.png)

### Implement Routes:

- `/index`: Display all classrooms.
  - Implement functionality so that clicking on a classroom shows all students assigned to that classroom.
- `/class/new`: Route to create a new classroom.
- `/student/new`: Route to create a new student and assign them to a classroom.

### Implement CRUD Operations:

**Read:**
- Retrieve all students for a specific classroom.
- Retrieve all classrooms.
- Retrieve all students.

**Create:**
- Add new classrooms.
- Add new students and assign them to existing classrooms.

**Delete:**
- Remove classrooms (ensure proper handling of associated students).
- Remove students.

### Validate:
- Ensure that all CRUD operations are working correctly and that relationships are managed properly.

## Sample Code Guidance

### Model Definitions:

**Classroom Model:**
- Should have attributes like id and name.

**Student Model:**
- Should have attributes like id, name, and classroomId as a foreign key.

### Relationships:
- Use Sequelize's `hasMany` and `belongsTo` methods to set up the one-to-many relationship.

### Routes Overview:
- `/index`: Render a list of all classrooms.
- `/class/new`: Form for creating a new classroom.
- `/student/new`: Form for creating a new student and assigning them to a classroom.
- `/class/:id/students`: Show all students for a specific classroom.

## Evaluation Criteria & Learning Objectives
- Define and implement one-to-many relationships between Sequelize models.
- Create routes to handle CRUD operations for Classroom and Student.
- Ensure relationships are respected and managed correctly.
- Validate the functionality of the implemented routes and operations.

## Directions

### Define Models and Relationships:
- Create Classroom and Student models with the appropriate attributes and relationships.

### Implement Routes and CRUD Operations:
- Set up routes and functionality to handle the CRUD operations as described.

### Test the Implementation:
- Ensure all routes and operations work as expected and handle data relationships correctly.

### Submit Your Work:
- Provide a link to your code repository with the completed assignment.
- Include any relevant documentation or screenshots to demonstrate your implementation.

## Expected Outputs
- **Model Definitions:** Correctly defined Classroom and Student models with one-to-many relationships.
- **CRUD Operations:** Functional routes for creating, reading, and deleting records.
- **Data Validation:** Proper handling of relationships and data integrity.

## Stretch Requirements:
- Implement additional validation or error handling as needed.
- Enhance functionality with more complex queries or features if desired.
