### server.ts

```ts
import express, { Request, Response } from 'express';
import path from 'path';
import methodOverride from 'method-override';

const app = express();
const port = 3000;

/**
 * Middleware
 */
app.use(express.urlencoded({ extended: true }));
app.use(methodOverride('_method')); // Enable PUT and PATCH methods

// Set EJS as the view engine
app.set('view engine', 'ejs');
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));
app.set('views', path.join(__dirname, '..', 'src', 'views'));

// Temporary in-memory storage for notes
let notes: { id: number, title: string, content: string }[] = [];
let nextId = 1;

/**
 * GET /
 * Render the index page
 */
app.get('/', (req: Request, res: Response) => {
    res.render('index');
});

/**
 * GET /notes
 * Render list of all notes
 */
app.get('/notes', (req: Request, res: Response) => {
    res.render('notes', { notes });
});

/**
 * GET /notes/add
 * Render the new note page
 */
app.get('/notes/add', (req: Request, res: Response) => {
    res.render('newNote');
});

/**
 * GET /notes/:id
 * Render a single note
 */
app.get('/notes/:id', (req: Request, res: Response) => {
    const noteId: number = parseInt(req.params.id);
    const note = notes.find(n => n.id === noteId);
    if (note) {
        res.render('note', { note });
    } else {
        res.status(404).send('Note not found');
    }
});

/**
 * POST /notes
 * Create a new note
 */
app.post('/notes', (req: Request, res: Response) => {
    const { title, content } = req.body;
    const newNote = { id: nextId++, title, content };
    notes.push(newNote);
    res.redirect('/notes');
});

/**
 * PUT /notes/:id
 * Replace a note
 */
app.put('/notes/:id', (req: Request, res: Response) => {
    const noteId: number = parseInt(req.params.id);
    const note = notes.find(n => n.id === noteId);
    if (note) {
        const { title, content } = req.body;
        note.title = title;
        note.content = content;
        res.redirect(`/notes/${note.id}`);
    } else {
        res.status(404).send('Note not found');
    }
});

/**
 * PATCH /notes/:id
 * Update a note
 */
app.patch('/notes/:id', (req: Request, res: Response) => {
    const noteId: number = parseInt(req.params.id);
    const note = notes.find(n => n.id === noteId);
    if (note) {
        const { title, content } = req.body;
        if (title) note.title = title;
        if (content) note.content = content;
        res.redirect(`/notes/${note.id}`);
    } else {
        res.status(404).send('Note not found');
    }
});

/**
 * DELETE /notes/:id
 * Delete a note
 */
app.delete('/notes/:id', (req: Request, res: Response) => {
    const noteId: number = parseInt(req.params.id);
    const noteIndex = notes.findIndex(n => n.id === noteId);
    if (noteIndex !== -1) {
        notes.splice(noteIndex, 1);
        res.redirect('/notes');
    } else {
        res.status(404).send('Note not found');
    }
});

// Start the server
app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});
```

### views/index.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Note Taking App</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
    <h1>Welcome to Your Notes</h1>
    <h2>Organbize your thoughts easily</h2>
    <a href="/notes">View Notes</a>
</body>
</html>
```
### views/newNote.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Add Note</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
    <div class="container">
        <h1>Add Note</h1>
        <form action="/notes" method="POST">
            <label for="title">Title:</label>
            <input type="text" id="title" name="title" required>
            <label for="content">Content:</label>
            <textarea id="content" name="content" required></textarea>
            <button type="submit">Add Note</button>
        </form>
        <a href="/notes">Back to List</a>
    </div>
</body>
</html>
```
### views/notes.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Note Taking App</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
    <div class="container">
        <h1>Notes</h1>
        <ul>
            <% notes.forEach(note => { %>
                <li>
                    <a href="/notes/<%= note.id %>"><%= note.title %></a>
                    <span>- Last Updated: <%= new Date().toLocaleDateString() %></span>
                </li>
            <% }); %>
        </ul>
        <a href="/notes/add">Add New Note</a>
    </div>
</body>
</html>
```
### views/note.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><%= note.title %></title>
    <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
    <div class="container">
        <h1><%= note.title %></h1>
        <form action="/notes/<%= note.id %>?_method=PUT" method="POST">
            <label for="title">Title:</label>
            <input type="text" id="title" name="title" value="<%= note.title %>" required>
            <p>Last Updated: <%= new Date().toLocaleDateString() %></p>
            <label for="content">Content:</label>
            <textarea id="content" name="content" required><%= note.content %></textarea>
            <button type="submit">Update Note</button>
        </form>
        <form action="/notes/<%= note.id %>?_method=DELETE" method="POST">
            <button type="submit">Delete Note</button>
        </form>
        <a href="/notes">Back to List</a>
    </div>
</body>
</html>
```