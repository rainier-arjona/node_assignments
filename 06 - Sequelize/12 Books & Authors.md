### Assignment: Books & Authors

In this assignment, you’ll build a basic application to manage many-to-many relationships between books and authors. You'll need to implement features to create, read, and delete books and authors, as well as manage their associations.

![../10%20-%20Assets/Books&Authors.png](../10%20-%20Assets/Books&Authors.png)

**Estimated Time to Completion:** 90 mins

**Level of Complexity:** Medium

**Instructions**

1. **Understand the Assignment:**
    - Review the requirements and make sure you understand how many-to-many relationships work and how to implement them using Sequelize.
2. **Set Up Your Models:**
    - Define the models for Book and Author and establish a many-to-many relationship between them.
    - Use Sequelize to create and synchronize these models with your database.
    
    ![./assets/Books%20&%20Authors%20ERD.png](./assets/Books%20&%20Authors%20ERD.png)
    
3. **Implement CRUD Operations:**
    - **Create New Records:** Implement routes to create new books and authors and assign them to each other.
    - **Read Records:** Implement routes to list all books and authors. When clicking on a book or author, show their related records (e.g., authors of a book or books of an author).
    - **Delete Records:** Implement functionality to delete books and authors, ensuring that the associations are handled correctly.
4. **Test Your Application:**
    - Make sure that all routes work as expected. Check that you can create, view, and delete records and that the associations between books and authors are correctly managed.
5. **Submit Your Work:**
    - Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- **Define and manage many-to-many relationships using Sequelize:** Properly set up and manage relationships between models.
- **Implement CRUD operations for models with many-to-many relationships:** Ensure all CRUD functionality is implemented and operational.
- **Use Sequelize queries to handle complex relationships and associations:** Manage relationships and data integrity effectively.
- **Ensure data integrity and correct management of relationships when creating, updating, and deleting records:** Verify that data is handled correctly and associations are maintained.

**Directions**

**MVP Requirements: Many-to-Many Relationship Management**

1. **Index Page:**
    - Create a route to show a list of all books and all authors on a single page.
    - Ensure that each entry in the list is clickable to view more details.
2. **Details Pages:**
    - **For Books:** Create a route to show all authors associated with a selected book.
    - **For Authors:** Create a route to show all books written by a selected author.
3. **Create New Records:**
    - Implement routes to create new books and authors.
    - Include functionality to assign authors to books and vice versa when creating new records.
4. **Delete Records:**
    - Implement routes to delete books and authors.
    - Ensure that deleting a book or author correctly updates the associations.
5. **Routes:**
    - **/books/new:** Route to create a new book and assign authors to it.
    - **/authors/new:** Route to create a new author and assign books to them.

**Expected Outputs**

- **Index Page:** A single page displaying all books and authors. Each entry should be clickable to view more details.
- **Book Details Page:** A page that lists all authors associated with the selected book, with a clear view of the relationships.
- **Author Details Page:** A page that lists all books associated with the selected author, showing the connections clearly.
- **Create New Records:** Forms that allow for the creation of new books and authors, with functionality to assign relationships between them.
- **Delete Records:** Functionality that allows for the deletion of books and authors, ensuring that relationships are updated correctly without orphaned records.