### use the same setup with student info I
---
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

### add.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Add Student</title>
</head>
<body>
    <h1>Add Student</h1>
    <form action="/students/add" method="POST">
        <label for="first_name">First Name:</label>
        <input type="text" id="first_name" name="first_name" required>
        <label for="last_name">Last Name:</label>
        <input type="text" id="last_name" name="last_name" required>
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required>
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" required>
        <button type="submit">Add</button>
    </form>
</body>
</html>
```

### index.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Info</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            background-color: #f8f9fa;
        }

        .header-container {
            width: 100%;
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 20px;
            background-color: #343a40;
            color: white;
        }

        .header-container h1 {
            margin: 0;
            flex: 1;
        }

        .button-links {
            display: flex;
            gap: 10px;
        }

        .button-link {
            display: inline-block;
            padding: 10px 20px;
            background-color: #007bff;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            text-align: center;
        }

        .button-link:hover {
            background-color: #0056b3;
        }

        table {
            width: 100%;
            max-width: 1000px;
            border-collapse: collapse;
            margin-top: 20px;
            background-color: white;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        table, th, td {
            border: 1px solid #ddd;
        }

        th, td {
            padding: 10px;
            text-align: left;
        }

        th {
            background-color: #f4f4f4;
        }

        .delete-button {
            color: red;
            border: none;
            background: none;
            cursor: pointer;
        }

        .delete-button:hover {
            text-decoration: underline;
        }
    </style>
</head>

<body>
    <div class="header-container">
        <h1><%= students.length %> Student(s)</h1>
        <div class="button-links">
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
                        <td><%= student.id %></td>
                        <td><%= student.first_name %></td>
                        <td><%= student.last_name %></td>
                        <td><%= student.email %></td>
                        <td><%= student.age %></td>
                        <td>
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