### Assignment: Note Taking App

In this assignment, you will build a simple CRUD application using Express. The goal is to manage notes with basic CRUD operations while rendering the data through EJS templates. The notes will be temporarily stored in a server variable, and you will verify the application by testing the various routes.

![./assets/Note%20Taking%20App.png](./assets/Note%20Taking%20App.png)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Implement CRUD operations with Express and EJS.
- Handle various HTTP methods (GET, POST, PATCH, PUT, DELETE).
- Use temporary storage in server variables to manage data.
- Render data using EJS templates.

---

**Directions**

Build an Express application that allows you to create, read, update, and delete notes. The application should use EJS templates to render data.

**MVP Requirements: : CRUD Operations with EJS Rendering**

- **CRUD Operations with EJS Rendering**
    - **`GET /notes`**: Render a list of all notes using an EJS template.
    - **`GET /notes/:id`**: Render a single note based on its ID using an EJS template.
    - **`POST /notes`**: Create a new note. The form submission should be handled by a POST request, and the page should redirect to the `/notes` route after creation.
    - **`PATCH /notes/:id`**: Update specific fields of an existing note. The update form should handle partial updates and redirect to the `/notes/:id` route to display the updated note.
    - **(OPTIONAL) `PUT /notes/:id`**: Replace an existing note entirely. The update form should handle full replacements and redirect to the `/notes/:id` route to display the updated note.
    - **`DELETE /notes/:id`**: Delete a note by its ID. Implement a delete button on the note detail page that sends a DELETE request and redirects to the `/notes` route after deletion.

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