### server.ts
```ts
import express from 'express';
import path from 'path';
import { Classroom, Student, sequelize } from './models';
import { ValidationError as SequelizeValidationError } from 'sequelize';

const app = express();
const port = 3000;

app.set('view engine', 'ejs');
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));
app.set('views', path.join(__dirname, '..', 'src', 'views'));
app.use(express.urlencoded({ extended: true }));
app.use(express.json());

// Display all classrooms
app.get('/', async (req, res) => {
    try {
        const classrooms = await Classroom.findAll();
        res.render('index', { classrooms });
    } catch (error) {
        console.error('Error fetching classrooms:', error);
        res.status(500).send('Internal Server Error');
    }
});

app.get('/class/new', (req, res) => {
    res.render('newClass');
});

// Create a new classroom
app.post('/class/add', async (req, res) => {
    try {
        await Classroom.create({ name: req.body.name });
        res.redirect('/');
    } catch (error) {
        // Basic error handling
        if (error instanceof SequelizeValidationError) {
            // Pass the errors array to the EJS view
            res.status(400).render('newClass', { errors: error.errors });
        } else {
            res.status(500).send('Internal Server Error');
        }
    }
});

// Display all students in a specific classroom
app.get('/classroom/:id', async (req, res) => {
    try {
        const classroom = await Classroom.findByPk(req.params.id, {
            include: [{ model: Student, as: 'students' }],
        });
        if (!classroom) return res.status(404).send('Classroom not found');
        res.render('classroom', { classroom });
    } catch (error) {
        console.error('Error fetching classroom:', error);
        res.status(500).send('Internal Server Error');
    }
});

// Create a new student (pass classrooms to the view)
app.get('/student/new', async (req, res) => {
    try {
        const classrooms = await Classroom.findAll();
        res.render('newStudent', { classrooms });
    } catch (error) {
        // Basic error handling
        if (error instanceof SequelizeValidationError) {
            // Pass the errors array to the EJS view
            res.status(400).render('newClass', { errors: error.errors });
        } else {
            res.status(500).send('Internal Server Error');
        }
    }
});

// Create a new student
app.post('/student', async (req, res) => {
    try {
        await Student.create({ name: req.body.name, classroomId: req.body.classroomId });
        res.redirect('/');
    } catch (error) {
        console.error('Error creating student:', error);
        res.status(500).send('Internal Server Error');
    }
});

// Delete a classroom
app.post('/classroom/:id/remove', async (req, res) => {
    try {
        const classroom = await Classroom.findByPk(req.params.id);
        if (!classroom) return res.status(404).send('Classroom not found');
        await classroom.destroy();
        res.redirect('/');
    } catch (error) {
        console.error('Error deleting classroom:', error);
        res.status(500).send('Internal Server Error');
    }
});

// Delete a student
app.post('/student/:id/delete', async (req, res) => {
    try {
        const student = await Student.findByPk(req.params.id);
        if (!student) return res.status(404).send('Student not found');
        await student.destroy();
        res.redirect('/');
    } catch (error) {
        console.error('Error deleting student:', error);
        res.status(500).send('Internal Server Error');
    }
});

app.listen(port, () => {
    console.log(`Server is running on http://localhost:${port}`);
});
```

### models/classroom.ts
```ts
import { Model, DataTypes } from 'sequelize';
import sequelize from '../config/database';

class Classroom extends Model {
    public id!: number;
    public name!: string;
}

Classroom.init({
    id: {
        type: DataTypes.INTEGER,
        autoIncrement: true,
        primaryKey: true,
    },
    name: {
        type: DataTypes.STRING,
        allowNull: false,
        validate: {
            notEmpty: {
                msg: 'Classroom name cannot be empty',
            },
        },
    },
}, {
    sequelize,
    modelName: 'Classroom',
});

export default Classroom;
```

### models/students.ts
```ts
import { Model, DataTypes } from 'sequelize';
import sequelize from '../config/database';
import Classroom from './classroom';

class Student extends Model {
    public id!: number;
    public name!: string;
    public classroomId!: number;
}

Student.init({
    id: {
        type: DataTypes.INTEGER,
        autoIncrement: true,
        primaryKey: true,
    },
    name: {
        type: DataTypes.STRING,
        allowNull: false,
        validate: {
            notEmpty: {
                msg: 'Student name cannot be empty',
            },
        },
    },
    classroomId: {
        type: DataTypes.INTEGER,
        allowNull: false,
        references: {
            model: Classroom,
            key: 'id',
        },
        validate: {
            isInt: {
                msg: 'Classroom ID must be an integer',
            },
            notNull: {
                msg: 'Classroom ID is required',
            },
        },
    },
}, {
    sequelize,
    modelName: 'Student',
});

Student.belongsTo(Classroom, { foreignKey: 'classroomId' });
Classroom.hasMany(Student, { foreignKey: 'classroomId' });

export default Student;
```
### models/index.ts
```ts
import sequelize from '../config/database';
import Classroom from './classroom';
import Student from './student';

Classroom.hasMany(Student, { foreignKey: 'classroomId', as: 'students' });
Student.belongsTo(Classroom, { foreignKey: 'classroomId', as: 'classroom' });

export { Classroom, Student, sequelize };
```
### views/index.ejs
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Classroom Management</title>
</head>

<body>
    <header>
        <nav>
            <a href="/">Classroom Management</a>
            <a href="/">Home</a>
            <a href="/class/new">Add Classroom</a>
            <a href="/student/new">Add Student</a>
        </nav>
    </header>
    <main>
        <h1>All Classrooms</h1>
        <ul>
            <% classrooms.forEach(classroom => { %>
                <li>
                    <a href="/classroom/<%= classroom.id %>"><%= classroom.name %></a>
                    <p>Grade: <%= classroom.grade %></p>
                </li>
            <% }) %>
        </ul>
    </main>
</body>

</html>

```
### views/classroom.ejs
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Classroom Management</title>
</head>

<body>
    <header>
        <nav>
            <a href="/">Classroom Management</a>
            <a href="/">Home</a>
            <a href="/class/new">Add Classroom</a>
            <a href="/student/new">Add Student</a>
        </nav>
    </header>
    <main>
        <h1>Students in <%= classroom.name %> Class</h1>
        <form action="/classroom/<%= classroom.id %>/remove" method="post">
            <input type="submit" value="Remove Class">
        </form>
        <ul>
            <% classroom.students.forEach(student => { %>
                <li>
                    <p><%= student.name %></p>
                    <form action="/student/<%= student.id %>/delete" method="post">
                        <input type="submit" value="Delete">
                    </form>
                </li>
            <% }) %>
        </ul>
    </main>
</body>

</html>
```
### views/newClass.ejs
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Classroom Management</title>
</head>

<body>
    <header>
        <nav>
            <a href="/">Classroom Management</a>
            <a href="/">Home</a>
            <a href="/class/new">Add Classroom</a>
            <a href="/student/new">Add Student</a>
        </nav>
    </header>
    <main>
        <h1>Add Classroom</h1>
        <form action="/class/add" method="POST">
            <label for="name">Classroom Name</label>
            <input type="text" name="name" id="name" required>
            <label for="grade">Grade</label>
            <input type="number" name="grade" id="grade" required>
            <button type="submit">Create</button>
            <% if (typeof errors !== 'undefined') { %>
                <ul>
                    <% errors.forEach(error => { %>
                        <li><%= error.message %></li>
                    <% }) %>
                </ul>
            <% } %>
        </form>
    </main>
</body>

</html>

```
### views/newStudent.ejs
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Classroom Management</title>
</head>

<body>
    <header>
        <nav>
            <a href="/">Classroom Management</a>
            <a href="/">Home</a>
            <a href="/class/new">Add Classroom</a>
            <a href="/student/new">Add Student</a>
        </nav>
    </header>
    <main>
        <h1>Add Student</h1>
        <form action="/student" method="POST">
            <label for="name">Student Name</label>
            <input type="text" name="name" id="name" required>
            <label for="classroomId">Classroom</label>
            <select name="classroomId" id="classroomId" required>
                <% classrooms.forEach(classroom => { %>
                    <option value="<%= classroom.id %>"><%= classroom.name %></option>
                <% }) %>
            </select>
            <button type="submit">Enroll</button>
            <% if (typeof errors !== 'undefined') { %>
                <ul>
                    <% errors.forEach(error => { %>
                        <li><%= error.message %></li>
                    <% }) %>
                </ul>
            <% } %>
        </form>
    </main>
</body>

</html>
```