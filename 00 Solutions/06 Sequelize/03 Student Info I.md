### Folder Structure

```js
project-root/
├── src/
│   ├── public/
│   │   └── (your static assets like CSS, JS, images, if any)
│   ├── views/
│   │   └── index.ejs
│   ├── models/
│   │   └── student.js
│   ├── config/
│   │   ├── config.json
│   │   └── database.ts
│   └── server.js
├── dist/
│   └── server.js
├── node_modules/
├── package.json
└── package-lock.json
```

### config.json
```json
{
    "development": {
        "username": "root",
        "password": "root",
        "database": "students_db",
        "host": "127.0.0.1",
        "dialect": "mysql"
    },
}
```
### package.json
```json
{
  "name": "03-student-info-i",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "build": "tsc",
    "sync": "node dist/sync.js",
    "migrate": "sequelize db:migrate --config src/config/config.json",
    "migrate:undo": "sequelize db:migrate:undo --config src/config/config.json",
    "seed": "sequelize db:seed:all --config src/config/config.json",
    "seed:undo": "sequelize db:seed:undo --config src/config/config.json",
    "start": "node dist/server.js",
    "dev": "tsc-watch --onSuccess \"nodemon dist/server.js\"",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "description": "",
  "dependencies": {
    "dotenv": "^16.4.5",
    "ejs": "^3.1.10",
    "express": "^4.19.2",
    "mysql2": "^3.11.0",
    "sequelize": "^6.37.3",
    "tsc-watch": "^6.2.0"
  },
  "devDependencies": {
    "@types/express": "^4.17.21",
    "@types/node": "^22.0.0",
    "nodemon": "^3.1.4",
    "sequelize-cli": "^6.6.2",
    "ts-node": "^10.9.2",
    "ts-node-dev": "^2.0.0",
    "typescript": "^5.5.4"
  }
}
```

### tsconfig.json
```json
{
  "compilerOptions": {
    "target": "ES6",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "resolveJsonModule": true
  },
  "include": [
    "src/**/*"
, "src/config"  ],
  "exclude": [
    "node_modules",
    "dist"
  ]
}
```

### database.ts
```ts
import { Sequelize } from 'sequelize';
import dotenv from 'dotenv';

dotenv.config();

const sequelize = new Sequelize(
    process.env.DB_NAME!,
    process.env.DB_USERNAME!,
    process.env.DB_PASSWORD!,
    {
        host: process.env.DB_HOST,
        dialect: process.env.DB_DIALECT as 'mysql',
    }
);

export default sequelize;
```

### .env
```js
DB_USERNAME=root
DB_PASSWORD=root
DB_NAME=students_db
DB_HOST=127.0.0.1
DB_DIALECT=mysql
```

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

app.listen(port, () => {
    console.log(`Server is running on http://localhost:${port}`);
});
```

### models/student.ts
```ts
import { DataTypes, Model, Optional } from 'sequelize';
import sequelize from '../config/database';

interface StudentAttributes {
    id: number;
    first_name: string;
    last_name: string;
    email: string;
    age: number;
    createdAt?: Date;
    updatedAt?: Date;
}

interface StudentCreationAttributes extends Optional<StudentAttributes, 'id'> { }

/**
 * Represents a student.
 *
 * @remarks
 * This class is used to store information about a student.
 */
class Student extends Model<StudentAttributes, StudentCreationAttributes> implements StudentAttributes {
    public id!: number;
    public first_name!: string;
    public last_name!: string;
    public email!: string;
    public age!: number;
    public createdAt?: Date;
    public updatedAt?: Date;
}

Student.init(
    {
        id: {
            type: DataTypes.INTEGER.UNSIGNED,
            autoIncrement: true,
            primaryKey: true,
        },
        first_name: {
            type: DataTypes.STRING,
            allowNull: false,
        },
        last_name: {
            type: DataTypes.STRING,
            allowNull: false,
        },
        email: {
            type: DataTypes.STRING,
            allowNull: false,
            unique: true,
        },
        age: {
            type: DataTypes.INTEGER.UNSIGNED,
            allowNull: false,
        },
        createdAt: {
            type: DataTypes.DATE,
            defaultValue: DataTypes.NOW,
            field: 'createdAt',
        },
        updatedAt: {
            type: DataTypes.DATE,
            defaultValue: DataTypes.NOW,
            field: 'updatedAt',
        },
    },
    {
        sequelize,
        tableName: 'Students',
        timestamps: true,  // Enable timestamps
    }
);

export { Student };
```

### views/index.ejs

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
    </style>
</head>

<body>
    <div class="header-container">
        <h1><%= students.length %> Student(s)</h1>
        <div class="button-links">
            <a href="/" class="button-link">Fetch All</a>
            <a href="/students/age/22" class="button-link">Fetch 22 Years Old</a>
            <a href="/students/lastname/Smith" class="button-link">Fetch Last Name Smith</a>
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
                    </tr>
                <% }); %>
            <% } else { %>
                <tr>
                    <td colspan="5">No student data available.</td>
                </tr>
            <% } %>
        </tbody>
    </table>
</body>

</html>
```