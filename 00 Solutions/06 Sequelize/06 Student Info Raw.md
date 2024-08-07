### server.ts
```ts
import express from 'express';
import path from 'path';
import { Student } from './models/student';
import sequelize from './config/database';

const app = express();
const port = 3000;

app.set('view engine', 'ejs');
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));
app.set('views', path.join(__dirname, '..', 'src', 'views'));
app.use(express.urlencoded({ extended: true }));
app.use(express.json());

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
 * Route to handle filtering students by age using raw SQL queries
 * @param {express.Request} req - The request object
 * @param {express.Response} res - The response object
 */
app.get('/students/filter', async (req, res) => {
    try {
        const ageFilter = req.query.age as string;
        
        let query = 'SELECT * FROM Students';
        const replacements: any[] = [];
        
        if (ageFilter === 'above20') {
            query += ' WHERE age > ?';
            replacements.push(20);
        } else if (ageFilter === 'below20') {
            query += ' WHERE age <= ?';
            replacements.push(20);
        }
        
        const [results] = await sequelize.query(query, { replacements });
        
        res.render('index', { students: results });
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
app.get('/age/:age', async (req, res) => {
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
app.get('/name/:lastname', async (req, res) => {
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

### index.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Info</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>

<body>
    <div class="header-container">
        <h1><%= students.length %> Student(s)</h1>
        <div class="button-links">
            <a href="/" class="button-link">Fetch All</a>
            <a href="/age/22" class="button-link">Fetch 22 Years Old</a>
            <a href="/name/Smith" class="button-link">Fetch Last Name Smith</a>
            <form action="/students/filter" method="GET">
                <input type="radio" id="age1" name="age" value="above20">
                <label for="age1">Above 20</label>
                <input type="radio" id="age2" name="age" value="below20">
                <label for="age2">20 or Below</label>
                <button type="submit">Filter</button>
            </form>                      
            <a href="/add" class="button-link">Add Student</a>
        </div>
    </div>

    <!-- Display students in a single table -->
    <table>
        <thead>
            <tr>
                <th>ID</th>
                <th>First Name</th>
                <th>Last Name</th>
                <th>Email</th>
                <th>Age</th>
                <th>Action</th>
            </tr>
        </thead>
        <tbody>
            <% if (students.length) { %>
                <% students.forEach(student => { %>
                    <tr>
                        <td><a href="students/<%= student.id %>"><%= student.id %></a></td>
                        <td><%= student.first_name %></td>
                        <td><%= student.last_name %></td>
                        <td><%= student.email %></td>
                        <td><%= student.age %></td>
                        <td>
                            <a href="edit/<%= student.id %>">Edit</a>
                            <span>|</span>
                            <form action="/students/delete/<%= student.id %>" method="POST">
                                <button type="submit" class="delete-button">Delete</button>
                            </form>
                        </td>
                    </tr>
                <% }); %>
            <% } else { %>
                <tr>
                    <td colspan="6">No student data available.</td>
                </tr>
            <% } %>
        </tbody>
    </table>
</body>
</html>
```