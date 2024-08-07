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
app.use(express.json()); // Parse JSON bodies
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
 * GET /api/notes
 * Return a JSON array containing all notes
 */
app.get('/api/notes', (req: Request, res: Response) => {
    res.json(notes);
});

/**
 * GET /api/notes/:id
 * Return a JSON object representing a single note
 */
app.get('/api/notes/:id', (req: Request, res: Response) => {
    const noteId: number = parseInt(req.params.id);
    const note = notes.find(n => n.id === noteId);
    if (note) {
        res.json(note);
    } else {
        res.status(404).json({ error: 'Note not found' });
    }
});

/**
 * POST /api/notes
 * Create a new note
 */
app.post('/api/notes', (req: Request, res: Response) => {
    const { title, content } = req.body;
    if (!title || !content) {
        return res.status(400).json({ error: 'Title and content are required' });
    }
    const newNote = { id: nextId++, title, content };
    notes.push(newNote);
    res.status(201).json(newNote);
});

/**
 * PATCH /api/notes/:id
 * Update specific fields of an existing note
 */
app.patch('/api/notes/:id', (req: Request, res: Response) => {
    const noteId: number = parseInt(req.params.id);
    const note = notes.find(n => n.id === noteId);
    if (note) {
        const { title, content } = req.body;
        if (title) note.title = title;
        if (content) note.content = content;
        res.json(note);
    } else {
        res.status(404).json({ error: 'Note not found' });
    }
});

/**
 * PUT /api/notes/:id
 * Replace an existing note entirely
 */
app.put('/api/notes/:id', (req: Request, res: Response) => {
    const noteId: number = parseInt(req.params.id);
    const noteIndex = notes.findIndex(n => n.id === noteId);
    if (noteIndex !== -1) {
        const { title, content } = req.body;
        if (!title || !content) {
            return res.status(400).json({ error: 'Title and content are required' });
        }
        notes[noteIndex] = { id: noteId, title, content };
        res.json(notes[noteIndex]);
    } else {
        res.status(404).json({ error: 'Note not found' });
    }
});

/**
 * DELETE /api/notes/:id
 * Delete a note by its ID
 */
app.delete('/api/notes/:id', (req: Request, res: Response) => {
    const noteId: number = parseInt(req.params.id);
    const noteIndex = notes.findIndex(n => n.id === noteId);
    if (noteIndex !== -1) {
        notes.splice(noteIndex, 1);
        res.status(204).send(); // No content
    } else {
        res.status(404).json({ error: 'Note not found' });
    }
});

// Start the server
app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});
```