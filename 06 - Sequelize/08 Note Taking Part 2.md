# Assignment: Note Taking App - JSON Responses

In this assignment, you'll build upon the CRUD notes application from Part 1 by converting your routes to an API that responds with JSON data. You'll prefix your routes with `/api` and ensure that all responses are in JSON format. Your goal is to create a functional API to manage notes and verify it by testing the routes using Postman.

![./assets/Note%20Taking%20App.png](./assets/Note%20Taking%20App.png)

**Estimated Time to Completion:** 90 mins

**Level of Complexity:** Medium

## Instructions

1. Review the requirements and understand how to implement API routes.
2. Update the existing routes from Part 1 to respond with JSON data instead of rendering EJS templates.
3. Test each route using Postman to ensure that the API works correctly and returns the expected JSON responses.
4. Submit your GitHub URL by the due date.

## Evaluation Criteria & Learning Objectives

- Implement API routes with Express to handle CRUD operations.
- Respond with JSON data for each route.
- Use sequelize storage to manage data.
- Test API endpoints using Postman.

## Directions

Transform the routes from Part 1 to create an API that handles CRUD operations and returns JSON data.

### MVP Requirements: CRUD API Operations

- **`GET /api/notes`**: Return a JSON array containing all notes. Each note should be represented as a JSON object.
- **`GET /api/notes/:id`**: Return a JSON object representing a single note based on its ID. If the note is not found, return a 404 status with an appropriate error message.
- **`POST /api/notes`**: Create a new note. The request body should contain the note details in JSON format. After creation, return the newly created note as a JSON object with a 201 status.
- **`PATCH /api/notes/:id`**: Update specific fields of an existing note. The request body should contain the fields to be updated in JSON format. Return the updated note as a JSON object with a 200 status. If the note is not found, return a 404 status with an error message.
- **(OPTIONAL) `PUT /api/notes/:id`**: Replace an existing note entirely. The request body should contain the complete note data in JSON format. Return the replaced note as a JSON object with a 200 status. If the note is not found, return a 404 status with an error message.
- **`DELETE /api/notes/:id`**: Delete a note by its ID. Return a 204 status with no content on successful deletion. If the note is not found, return a 404 status with an error message.

### Testing

- **Use Postman** to test each API endpoint. Verify that the responses are in JSON format and match the expected output.

### Expected Outputs

- **`GET /api/notes`**: JSON array of all notes.
- **`GET /api/notes/:id`**: JSON object of a single note or a 404 error if not found.
- **`POST /api/notes`**: JSON object of the newly created note or an error message.
- **`PATCH /api/notes/:id`**: JSON object of the updated note or a 404 error if not found.
- **(OPTIONAL) `PUT /api/notes/:id`**: JSON object of the replaced note or a 404 error if not found.
- **`DELETE /api/notes/:id`**: 204 status for successful deletion or a 404 error if not found.

### Stretch Requirements

- Implement input validation to ensure that the note data is in the correct format before saving.
- Add detailed error handling to provide meaningful messages for invalid requests or errors.
