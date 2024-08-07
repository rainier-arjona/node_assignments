### controllers/noteController.ts
```ts
import { Request, Response } from 'express';
import * as noteModel from '../models/noteModel';

/**
 * Handles the request to get all notes.
 * 
 * @param {Request} req - The request object.
 * @param {Response} res - The response object.
 */
export function getNotes(req: Request, res: Response) {
    const notes = noteModel.getAllNotes();
    res.render('notes', { notes });
}

/**
 * Handles the request to get a specific note by ID.
 * 
 * @param {Request} req - The request object.
 * @param {Response} res - The response object.
 */
export function getNoteById(req: Request, res: Response) {
    const noteId = parseInt(req.params.id);
    const note = noteModel.getNoteById(noteId);
    if (note) {
        res.render('note', { note });
    } else {
        res.status(404).send('Note not found');
    }
}

/**
 * Handles the request to create a new note.
 * 
 * @param {Request} req - The request object.
 * @param {Response} res - The response object.
 */
export function createNote(req: Request, res: Response) {
    const { title, content } = req.body;
    const newNote = noteModel.createNote({ title, content });
    res.redirect('/notes');
}

/**
 * Handles the request to update an existing note.
 * 
 * @param {Request} req - The request object.
 * @param {Response} res - The response object.
 */
export function updateNote(req: Request, res: Response) {
    const noteId = parseInt(req.params.id);
    const { title, content } = req.body;
    const updatedNote = noteModel.updateNote(noteId, { title, content });
    if (updatedNote) {
        res.redirect(`/notes/${updatedNote.id}`);
    } else {
        res.status(404).send('Note not found');
    }
}

/**
 * Handles the request to delete a specific note by ID.
 * 
 * @param {Request} req - The request object.
 * @param {Response} res - The response object.
 */
export function deleteNoteById(req: Request, res: Response) {
    const noteId = parseInt(req.params.id);
    const success = noteModel.deleteNoteById(noteId);
    if (success) {
        res.redirect('/notes');
    } else {
        res.status(404).send('Note not found');
    }
}
```
### models/noteModel.ts
```ts
// Temporary in-memory storage for notes
let notes: { id: number, title: string, content: string }[] = [];
let nextId = 1;

/** Get all notes */
export function getAllNotes() {
    return notes;
}

/** Get a note by ID */
export function getNoteById(id: number) {
    return notes.find(n => n.id === id);
}

/** Create a new note */
export function createNote(note: { title: string, content: string }) {
    const newNote = { id: nextId++, ...note };
    notes.push(newNote);
    return newNote;
}

/** Update a note */
export function updateNote(id: number, updateData: { title?: string, content?: string }) {
    const note = notes.find(n => n.id === id);
    if (note) {
        note.title = updateData.title || note.title;
        note.content = updateData.content || note.content;
        return note;
    }
    return null;
}

/** Delete a note by ID */
export function deleteNoteById(id: number) {
    const index = notes.findIndex(n => n.id === id);
    if (index !== -1) {
        notes.splice(index, 1);
        return true;
    }
    return false;
}
```
### routes/noteRoutes.ts
```ts
import express from 'express';
import * as noteController from '../controllers/noteController';

const router = express.Router();

/**
 * @route GET /notes
 * @desc Get all notes
 * @access Public
 */
router.get('/notes', noteController.getNotes);

/**
 * @route GET /notes/add
 * @desc Render new note form
 * @access Public
 */
router.get('/notes/add', (req, res) => res.render('newNote'));

/**
 * @route GET /notes/:id
 * @desc Get a note by ID
 * @access Public
 */
router.get('/notes/:id', noteController.getNoteById);

/**
 * @route POST /notes
 * @desc Create a new note
 * @access Public
 */
router.post('/notes', noteController.createNote);

/**
 * @route PUT /notes/:id
 * @desc Update a note by ID
 * @access Public
 */
router.put('/notes/:id', noteController.updateNote);

/**
 * @route PATCH /notes/:id
 * @desc Update a note by ID
 * @access Public
 */
router.patch('/notes/:id', noteController.updateNote);

/**
 * @route DELETE /notes/:id
 * @desc Delete a note by ID
 * @access Public
 */
router.delete('/notes/:id', noteController.deleteNoteById);

export default router;
```
### server.ts
```ts
import express, { Request, Response } from 'express';
import path from 'path';
import methodOverride from 'method-override';
import noteRoutes from './routes/noteRoutes';

/**
 * Creates an instance of the Express application.
 *
 * @returns {Express} The Express application instance.
 */
const app = express();
const port = 3000;

/**
 * Middleware
 */
app.use(express.urlencoded({ extended: true }));
app.use(methodOverride('_method')); // Enable PUT and PATCH methods

/* Set EJS as the view engine */
app.set('view engine', 'ejs');
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));
app.set('views', path.join(__dirname, '..', 'src', 'views'));

/* Mount routes */
app.use(noteRoutes);

/**
 * GET /
 * Render the index page
 */
app.get('/', (req: Request, res: Response) => {
    res.render('index');
});

/* Start the server */
app.listen(port, () => {
    console.log(`Server running at http://localhost:${port}`);
});
```