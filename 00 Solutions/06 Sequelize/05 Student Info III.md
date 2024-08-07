### server.ts

```ts
import express from 'express';
import path from 'path';
import { Student } from './models/student';

const app = express();
const port = 3000;

app.set('view engine', 'ejs');
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));
app.set('views', path.join(__dirname, '..', 'src', 'views'));
app.use(express.urlencoded({ extended: true }));

/**
 * Route to handle showing all students
 * @param {express.Request} req - The request object
 * @param {express.Response} res - The response object
 */
app.get('/', async (req, res) => {
    try {
        const students = await Student.findAll();
        res.render('index', { students });
    } catch (error) {
        console.log(error);
        res.status(500).send('Error fetching students');
    }
});

/**
 * Route to handle fetching a student by ID
 * @param {express.Request} req - The request object
 * @param {express.Response} res - The response object
 */
app.get('/students/:id', async (req, res) => {
    try {
        const id = req.params.id;
        const student = await Student.findByPk(id);
        res.render('index', { students: student ? [student] : [] });
    } catch (error) {
        console.log(error);
        res.status(500).send('Error fetching student');
    }
});

/**
 * Route to handle fetching students by age
 * @param {express.Request} req - The request object
 * @param {express.Response} res - The response object
 */
app.get('/students/age/:age', async (req, res) => {
    try {
        const age = req.params.age;
        const students = await Student.findAll({ where: { age } });
        res.render('index', { students });
    } catch (error) {
        console.log(error);
        res.status(500).send('Error fetching students');
    }
});

/**
 * Route to handle fetching students by last name
 * @param {express.Request} req - The request object
 * @param {express.Response} res - The response object
 */
app.get('/students/lastname/:lastname', async (req, res) => {
    try {
        const lastName = req.params.lastname;
        const students = await Student.findAll({ where: { last_name: lastName } });
        res.render('index', { students });
    } catch (error) {
        console.log(error);
        res.status(500).send('Error fetching students');
    }
});

/**
 * Route to render the edit student form
 * @param {express.Request} req - The request object
 * @param {express.Response} res - The response object
 */
app.get('/edit/:id', async (req, res) => {
    try {
        const id = req.params.id;
        const student = await Student.findByPk(id);
        if (student) {
            res.render('edit', { student });
        } else {
            res.status(404).send('Student not found');
        }
    } catch (error) {
        console.log(error);
        res.status(500).send('Error fetching student');
    }
});

/**
 * Route to handle updating a student
 * @param {express.Request} req - The request object
 * @param {express.Response} res - The response object
 */
app.post('/students/update/:id', async (req, res) => {
    try {
        const id = req.params.id;
        const { first_name, last_name, email, age } = req.body;
        const student = await Student.findByPk(id);
        if (student) {
            await student.update({ first_name, last_name, email, age });
            res.redirect('/');
        } else {
            res.status(404).send('Student not found');
        }
    } catch (error) {
        console.log(error);
        res.status(500).send('Error updating student');
    }
});

/**
 * Route to render the add student form
 * @param {express.Request} req - The request object
 * @param {express.Response} res - The response object
 */
app.get('/add', (req, res) => {
    res.render('add');
});

/**
 * Route to handle adding a new student
 * @param {express.Request} req - The request object
 * @param {express.Response} res - The response object
 */
app.post('/students/add', async (req, res) => {
    try {
        const { first_name, last_name, email, age } = req.body;
        await Student.create({ first_name, last_name, email, age });
        res.redirect('/');
    } catch (error) {
        console.log(error);
        res.status(500).send('Error adding student');
    }
});

/**
 * Route to handle deleting a student by ID
 * @param {express.Request} req - The request object
 * @param {express.Response} res - The response object
 */
app.post('/students/delete/:id', async (req, res) => {
    try {
        const id = req.params.id;
        await Student.destroy({ where: { id } });
        res.redirect('/');
    } catch (error) {
        console.log(error);
        res.status(500).send('Error deleting student');
    }
});

app.listen(port, () => {
    console.log(`Server is running on http://localhost:${port}`);
});
```

### edit.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Edit Student</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>

<body>
    <h1>Edit Student</h1>
    <form action="/students/update/<%= student.id %>" method="POST" class="form">
        <label for="first_name">First Name:</label>
        <input type="text" id="first_name" name="first_name" value="<%= student.first_name %>" required>
        <label for="last_name">Last Name:</label>
        <input type="text" id="last_name" name="last_name" value="<%= student.last_name %>" required>
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" value="<%= student.email %>" required>
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" value="<%= student.age %>" required>
        <button type="submit">Update</button>
    </form>
</body>
</html>
```