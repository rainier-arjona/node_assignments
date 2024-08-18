### server.ts
```ts
import express, { Request, Response } from 'express';
import path from 'path';
import bodyParser from 'body-parser';
import session from 'express-session';
import sequelize from './config/database';
import Enrollment from './models/Enrollment';

const app = express();
const port = 3000;

/**
 * Middleware to parse URL-encoded data.
 */
app.use(bodyParser.urlencoded({ extended: true }));

/**
 * Set EJS as the view engine and define the views directory.
 */
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, '..', 'src', 'views'));

/**
 * Serve static files from the public directory.
 */
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));

/**
 * Configure the session with a secret key and settings.
 */
app.use(session({
    secret: 'secretPolice',
    resave: false,
    saveUninitialized: true,
    cookie: { secure: false }
}));

/**
 * Synchronize the Sequelize models with the database.
 * Logs success or error.
 */
sequelize.sync().then(() => {
    console.log("Database synced!");
}).catch(err => {
    console.error("Error syncing database:", err);
});

/**
 * GET /
 * Renders the list of enrolled students.
 * 
 * @param req - Express request object.
 * @param res - Express response object.
 */
app.get('/', async (req: Request, res: Response) => {
    try {
        const students = await Enrollment.findAll();
        res.render("index", { students });
    } catch (error) {
        res.status(500).send("Error retrieving enrollment data");
    }
});

/**
 * POST /submit
 * Handles form submission for new enrollment.
 * 
 * @param req - Express request object.
 * @param res - Express response object.
 */
app.post("/submit", async (req: Request, res: Response) => {
    try {
        await Enrollment.create({
            name: req.body.name,
            email: req.body.email,
            number: req.body.number,
            course: req.body.course,
            start_date: req.body.start_date,
        });

        res.redirect("/");
    } catch (error) {
        res.status(500).send("Error saving enrollment data");
    }
});

/**
 * GET /edit/:id
 * Renders the edit page for a specific enrollment.
 * 
 * @param req - Express request object.
 * @param res - Express response object.
 */
app.get('/edit/:id', async (req: Request, res: Response) => {
    try {
        const enrollment = await Enrollment.findByPk(req.params.id);
        if (enrollment) {
            res.render('edit', { enrollment_data: enrollment });
        } else {
            res.status(404).send('Data not found');
        }
    } catch (error) {
        res.status(500).send('Error retrieving enrollment data');
    }
});

/**
 * POST /update/:id
 * Updates the enrollment data for a specific ID.
 * 
 * @param req - Express request object.
 * @param res - Express response object.
 */
app.post('/update/:id', async (req: Request, res: Response) => {
    try {
        const enrollment = await Enrollment.findByPk(req.params.id);
        if (enrollment) {
            enrollment.name = req.body.name;
            enrollment.email = req.body.email;
            enrollment.number = req.body.number;
            enrollment.course = req.body.course;
            enrollment.start_date = req.body.start_date;

            await enrollment.save();
            res.redirect('/');
        } else {
            res.status(404).send('Data not found');
        }
    } catch (error) {
        res.status(500).send('Error updating enrollment data');
    }
});

/**
 * POST /delete/:id
 * Deletes an enrollment record for a specific ID.
 * 
 * @param req - Express request object.
 * @param res - Express response object.
 */
app.post('/delete/:id', async (req: Request, res: Response) => {
    try {
        const enrollment = await Enrollment.findByPk(req.params.id);
        if (enrollment) {
            await enrollment.destroy();
            res.redirect('/');
        } else {
            res.status(404).send('Data not found');
        }
    } catch (error) {
        res.status(500).send('Error deleting enrollment data');
    }
});

/**
 * Starts the Express server.
 */
app.listen(port, () => {
    console.log(`Server is running at http://localhost:${port}`);
});
```

### model/Enrollment.ts
```ts
import { DataTypes, Model } from 'sequelize';
import sequelize from '../config/database';

class Enrollment extends Model {
    public id!: number;
    public name!: string;
    public email!: string;
    public number!: string;
    public course!: string;
    public start_date!: Date;
}

Enrollment.init(
    {
        id: {
            type: DataTypes.INTEGER.UNSIGNED,
            autoIncrement: true,
            primaryKey: true,
        },
        name: {
            type: DataTypes.STRING,
            allowNull: false,
        },
        email: {
            type: DataTypes.STRING,
            allowNull: false,
        },
        number: {
            type: DataTypes.STRING,
            allowNull: false,
        },
        course: {
            type: DataTypes.STRING,
            allowNull: false,
        },
        start_date: {
            type: DataTypes.DATE,
            allowNull: false,
        },
    },
    {
        sequelize,
        modelName: 'Enrollment',
        tableName: 'enrollments',
    }
);

export default Enrollment;
```

### views/index.ejs
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Enrolled Students</title>
        <link rel="stylesheet" href="CSS/style.css">
    </head>
    <body>
        <!-- Heading -->
        <h1>Enrolled Students</h1>
        
        <!-- Table -->
        <table>
            <thead>
                <tr>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Phone Number</th>
                    <th>Course</th>
                    <th>Start Date</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody>
                <% if (students.length > 0) { %>
                    <% students.forEach(student => { %>
                        <tr>
                            <!-- Student Details -->
                            <td><%= student.name %></td>
                            <td><%= student.email %></td>
                            <td><%= student.number %></td>
                            <td><%= student.course %></td>
                            <td><%= student.start_date.toDateString() %></td>
                            <td>
                                <!-- Edit Link -->
                                <a href="/edit/<%= student.id %>">Edit</a>
                                
                                <!-- Delete Form -->
                                <form action="/delete/<%= student.id %>" method="POST" style="display:inline;">
                                    <button type="submit">Delete</button>
                                </form>
                            </td>
                        </tr>
                    <% }) %>
                <% } else { %>
                    <!-- No Students Enrolled -->
                    <tr>
                        <td colspan="6">No students enrolled yet.</td>
                    </tr>
                <% } %>
            </tbody>
        </table>
        
        <!-- Add New Student Form -->
        <h2>Add New Student</h2>
        <form action="/submit" method="POST">
            <label for="name">Full Name:</label>
            <input type="text" id="name" name="name" required>
            
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required>
            
            <label for="number">Phone Number:</label>
            <input type="text" id="number" name="number" required>
            
            <label for="course">Course:</label>
            <input type="text" id="course" name="course" required>
            
            <label for="start_date">Start Date:</label>
            <input type="date" id="start_date" name="start_date" required>
            
            <button type="submit">Submit</button>
        </form>
    </body>
</html>
```

### views/edit.ejs
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Edit Enrollment</title>
        <link rel="stylesheet" href="/CSS/style.css">
    </head>
    <body>
        <!-- Heading -->
        <h1>Edit Enrollment Details</h1>
        
        <!-- Form for updating enrollment details -->
        <form action="/update/<%= enrollment_data.id %>" method="POST">
            <!-- Full Name -->
            <label for="name">Full Name:</label>
            <input type="text" id="name" name="name" value="<%= enrollment_data.name %>" required>
            
            <!-- Email -->
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" value="<%= enrollment_data.email %>" required>
            
            <!-- Phone Number -->
            <label for="number">Phone Number:</label>
            <input type="text" id="number" name="number" value="<%= enrollment_data.number %>" required>
            
            <!-- Course -->
            <label for="course">Course:</label>
            <input type="text" id="course" name="course" value="<%= enrollment_data.course %>" required>
            
            <!-- Start Date -->
            <label for="start_date">Start Date:</label>
            <input type="date" id="start_date" name="start_date" value="<%= enrollment_data.start_date.toISOString().split('T')[0] %>" required>
            
            <!-- Update button -->
            <button type="submit">Update</button>
        </form>
        
        <!-- Link to go back to the homepage -->
        <a class="back-link" href="/">Back</a>
    </body>
</html>
```
