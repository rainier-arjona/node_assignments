# Assignment: Books & Authors
In this assignment, you’ll build a basic application to manage many-to-many relationships between books and authors. 
You'll need to implement features to create, read, and delete books and authors, as well as manage their associations.

![ERD](../assets/Books%20&%20Authors.png)

**Estimated Time to Completion:** 90 mins

**Level of Complexity:** Medium

## Instructions
1. **Understand the Assignment:** Review the requirements and make sure you understand how many-to-many relationships work and how to implement them using Sequelize.

2. **Set Up Your Models:** Define the models for Book and Author and establish a many-to-many relationship between them. Use Sequelize to create and synchronize these models with your database.

![ERD](../assets/Books%20&%20Authors%20ERD.png)

3. **Implement CRUD Operations:**
    - **Create New Records:** Implement routes to create new books and authors and assign them to each other.
    - **Read Records:** Implement routes to list all books and authors. When clicking on a book or author, show their related records (e.g., authors of a book or books of an author).
    - **Delete Records:** Implement functionality to delete books and authors, ensuring that the associations are handled correctly.

4. **Test Your Application:** Make sure that all routes work as expected. Check that you can create, view, and delete records and that the associations between books and authors are correctly managed.

5. **Submit Your Work:** Submit your GitHub URL by the due date.

## Evaluation Criteria & Learning Objectives
- Define and manage many-to-many relationships using Sequelize
- Implement CRUD operations for models with many-to-many relationships
- Use Sequelize queries to handle complex relationships and associations
- Ensure data integrity and correct management of relationships when creating, updating, and deleting records

## Directions
### MVP Requirements: Many-to-Many Relationship Management
**Index Page:**
- Create a route to show a list of all books and all authors on a single page.
- Ensure that each entry in the list is clickable to view more details.

**Details Pages:**
- For Books: Create a route to show all authors associated with a selected book.
- For Authors: Create a route to show all books written by a selected author.

**Create New Records:**
- Implement routes to create new books and authors.
- Include functionality to assign authors to books and vice versa when creating new records.

**Delete Records:**
- Implement routes to delete books and authors.
- Ensure that deleting a book or author correctly updates the associations.

**Routes:**
- /books/new: Route to create a new book and assign authors to it.
- /authors/new: Route to create a new author and assign books to them.

### Expected Outputs
- Index Page: Displays all books and authors.
- Book Details Page: Lists all authors associated with the selected book.
- Author Details Page: Lists all books associated with the selected author.
- Create New Records: Forms for adding new books and authors, with assignment functionality.
- Delete Records: Functionality to delete books and authors, with correct handling of associations.