### Assignment: Note Taking App

In this assignment, you will build a simple CRUD application using Express. The goal is to manage notes with basic CRUD operations while rendering the data through EJS templates. The notes will be temporarily stored in a server variable, and you will verify the application by testing the various routes.

![./assets/Note%20Taking%20App.png](./assets/Note%20Taking%20App.png)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Medium

**Instructions**

1. **Read through the directions below.** Note: You will be provided with any necessary files to get started.
2. **Implement the routes and logic** as outlined.
3. **Test each route** using a browser or tools like Postman.
4. **Submit your GitHub URL with the completed code by the due date.**

**Evaluation Criteria & Learning Objectives**

- **Implement CRUD operations with Express and EJS:** Develop functional routes to handle Create, Read, Update, and Delete operations for notes using Express and render the data with EJS templates.
- **Handle various HTTP methods (GET, POST, PATCH, PUT, DELETE):** Ensure that the application correctly processes different types of HTTP requests and updates the note data accordingly.
- **Use temporary storage in server variables to manage data:** Manage note data temporarily within the server's memory, allowing for CRUD operations without permanent storage.
- **Render data using EJS templates:** Create and use EJS templates to display notes and provide a user interface for interacting with the application.

**Directions**

Build an Express application that allows you to create, read, update, and delete notes. The application should use EJS templates to render data.

**MVP Requirements: CRUD Operations with EJS Rendering**

1. **`GET /notes`**: Render a list of all notes using an EJS template.
2. **`GET /notes/:id`**: Render a single note based on its ID using an EJS template.
3. **`POST /notes`**: Create a new note. The form submission should be handled by a POST request, and the page should redirect to the `/notes` route after creation.
4. **`PATCH /notes/:id`**: Update specific fields of an existing note. The update form should handle partial updates and redirect to the `/notes/:id` route to display the updated note.
5. **(OPTIONAL) `PUT /notes/:id`**: Replace an existing note entirely. The update form should handle full replacements and redirect to the `/notes/:id` route to display the updated note.
6. **`DELETE /notes/:id`**: Delete a note by its ID. Implement a delete button on the note detail page that sends a DELETE request and redirects to the `/notes` route after deletion.

Temporarily store the notes in a server variable (e.g., an array). Ensure that the notes can be accessed, updated, and deleted as needed.

**Expected Outputs**

1. **`GET /notes`**: A rendered EJS template displaying a list of all notes.
2. **`GET /notes/:id`**: A rendered EJS template displaying a single note.
3. **`POST /notes`**: Confirmation of note creation with a redirect to the notes list.
4. **`PATCH /notes/:id`**: Updated details of a note with a redirect to the note's detail page.
5. **(OPTIONAL) `PUT /notes/:id`**: Full replacement of note details with a redirect to the note's detail page.
6. **`DELETE /notes/:id`**: Confirmation of note deletion with a redirect to the notes list.

**Stretch Requirements**

- Implement input validation to ensure that the note data is in the correct format.
- Add basic error handling to provide meaningful messages for invalid requests.