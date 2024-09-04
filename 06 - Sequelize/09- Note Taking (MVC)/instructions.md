### Assignment: Note Taking App (MVC with Sequelize)

In this assignment, you will enhance the Note Taking App by restructuring your application into an MVC (Model-View-Controller) architecture and integrating Sequelize for database management. This will involve organizing your application code into distinct components to improve maintainability and scalability while using Sequelize to handle data storage and retrieval.

![./assets/Note%20Taking%20App.png](./assets/Note%20Taking%20App.png)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Modularize an express project into an MVC framework

---

**Directions**

1. Understand MVC and Sequelize: Review the MVC (Model-View-Controller) architecture and Sequelize ORM to see how they fit with your existing application.

2. Refactor Part 2:
    - Transform the API routes from Part 2 into an MVC structure by separating routes, business logic, and data management into Models, Views, and Controllers.
    - Use Sequelize to manage database interactions.
3. Test Your Refactored Application: Ensure that your refactored application still works correctly and meets all requirements from Part 2.

**MVP Requirements: Implementing MVC Structure with Sequelize**

  1. Models
      - **Create a `noteModel.ts` file** to manage note data using Sequelize. Define a `Note` model with appropriate fields and methods for CRUD operations.
          Example methods in `noteModel.ts` might include:
          - `findAllNotes()`
          - `findNoteById(id)`
          - `createNote(noteData)`
          - `updateNote(id, updateData)`
          - `deleteNoteById(id)`
  2. Controllers
      - **Create a `noteController.ts` file** to handle incoming requests and interact with the model. This file should include methods to process requests and return appropriate responses. Example methods in `noteController.ts` might include:
          - `getNotes(req, res)`
          - `getNoteById(req, res)`
          - `createNote(req, res)`
          - `updateNote(req, res)`
          - `deleteNoteById(req, res)`
  3. Routes
      - **Update your route definitions in a `noteRoutes.ts` file** to use the methods defined in the controller.Example routes in `noteRoutes.ts` might include:
          - `router.get('/notes', noteController.getNotes)`
          - `router.get('/notes/:id', noteController.getNoteById)`
  4. Main Application
      - In your main application file (e.g., `server.ts`), set up Express to use the routes defined in `noteRoutes.ts` and configure Sequelize to connect to your database.
          
          ```tsx
          /src
            /controllers
              noteController.ts
            /models
              noteModel.ts
            /routes
              noteRoutes.ts
            server.ts
          
          ```  

**Expected Outputs**

- **`GET /notes:`** Render a list of all notes as an HTML page.
- **`GET /notes/add:`** Render a form to add a new note as an HTML page.
- **`POST /notes:`** Handle form submission to create a new note and redirect to the notes list.
- **`GET /notes/:id/edit:`** Render a form to edit an existing note as an HTML page.
- **`PUT /notes/:id:`** Handle form submission to update a note and redirect to the updated note view.
- **`DELETE /notes/:id:`** Handle note deletion and redirect to the notes list.

**Stretch Requirements**

- **Implement validation and error handling** in the model and controller layers.