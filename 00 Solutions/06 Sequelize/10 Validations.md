### model/userModel.ts
```ts
import { DataTypes, Model, Optional } from 'sequelize';
import sequelize from '../config/database';

// Define the User attributes
interface UserAttributes {
    id: number;
    name: string;
    email: string;
    password: string;
}

// Define the creation attributes for the User model
interface UserCreationAttributes extends Optional<UserAttributes, 'id'> { }

// Define the User model
class User extends Model<UserAttributes, UserCreationAttributes> implements UserAttributes {
    public id!: number;
    public name!: string;
    public email!: string;
    public password!: string;

    // Timestamps
    public readonly createdAt!: Date;
    public readonly updatedAt!: Date;
}

// Initialize the User model
User.init({
    id: {
        type: DataTypes.INTEGER,
        autoIncrement: true,
        primaryKey: true,
    },
    name: {
        type: DataTypes.STRING(50),
        allowNull: false,
        validate: {
            notEmpty: true,
            len: [1, 50],
        },
    },
    email: {
        type: DataTypes.STRING,
        allowNull: false,
        unique: true,
        validate: {
            isEmail: true,
            notEmpty: true,
        },
    },
    password: {
        type: DataTypes.STRING,
        allowNull: false,
        validate: {
            notEmpty: true,
            len: [8, Infinity],
        },
    },
}, {
    sequelize, // Pass the Sequelize instance
    tableName: 'users', // Specify the table name
});

export default User;
```

### server.ts
```ts
import express from 'express';
import path from 'path';
import User from './models/userModel';
import { ValidationError } from 'sequelize';

const app = express();
const port = 3000;

app.set('view engine', 'ejs');
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));
app.set('views', path.join(__dirname, '..', 'src', 'views'));
app.use(express.urlencoded({ extended: true }));
app.use(express.json());

app.get('/', (req, res) => {
    res.render('index', { errors: [] });
});

app.post('/register', async (req, res) => {
    const { name, email, password } = req.body;
    try {
        await User.create({ name, email, password });
        res.send('User registered successfully');
    } catch (error) {
        const errors: string[] = [];
        // Check if the error is an instance of ValidationError
        if (error instanceof ValidationError) {
            error.errors.forEach(err => errors.push(err.message));
        } else {
            // Handle unexpected errors
            errors.push('An unexpected error occurred.');
        }
        res.render('index', { errors });
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
    <title>Register</title>
</head>
<body>
    <h1>Register</h1>
    <form action="/register" method="post">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        <br><br>

        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required>
        <br><br>

        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required>
        <br><br>

        <button type="submit">Register</button>
    </form>

    <% if (errors) { %>
        <div>
            <h2>Errors:</h2>
            <ul>
                <% errors.forEach(error => { %>
                    <li><%= error %></li>
                <% }) %>
            </ul>
        </div>
    <% } %>
</body>
</html>
```
