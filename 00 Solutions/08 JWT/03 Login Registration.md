### middleware/authMiddleware.ts
```ts
import { Request, Response, NextFunction } from 'express';
import jwt from 'jsonwebtoken';

const jwtSecret  = 'secretPolice';

export const verifyToken = (req: Request, res: Response, next: NextFunction) => {
    const token = req.headers['authorization']?.split(' ')[1];

    if (!token) {
        return res.status(401).json({ message: 'No token provided' });
    }

    jwt.verify(token, jwtSecret , (err: any, decoded: any) => {
        if (err) {
            return res.status(401).json({ message: 'Failed to authenticate token' });
        }

        req.user = decoded;
        next();
    });
};
```

### middleware/jwthMiddleware.ts
```ts
import { Request, Response, NextFunction } from 'express';
import jwt from 'jsonwebtoken';

const jwtSecret = 'secretPolice'; // Replace with your actual secret key

export const verifyToken = (req: Request, res: Response, next: NextFunction) => {
    const token = req.cookies.token; // Get token from cookies

    if (!token) {
        return res.redirect('/auth/login'); // Redirect if no token
    }

    jwt.verify(token, jwtSecret, (err: any, decoded: any) => {
        if (err) {
            return res.redirect('/auth/login'); // Redirect if token is invalid
        }

        req.user = decoded; // Attach user data to request
        next();
    });
};

```

### models/index.ts
```ts
import User from "./userModel";

export { User };
```

### models/userModel.ts
```ts
import { Model, DataTypes } from 'sequelize';
import sequelize from '../config/database';
import bcrypt from 'bcryptjs';

class User extends Model {
    public id!: number;
    public email!: string;
    public firstName!: string;
    public lastName!: string;
    public password!: string;

    static async hashPassword(password: string): Promise<string> {
        return bcrypt.hash(password, 10);
    }

    static async comparePassword(password: string, hashedPassword: string): Promise<boolean> {
        return bcrypt.compare(password, hashedPassword);
    }
}

User.init({
    id: {
        type: DataTypes.INTEGER,
        autoIncrement: true,
        primaryKey: true
    },
    email: {
        type: DataTypes.STRING,
        allowNull: false,
        unique: true
    },
    firstName: {
        type: DataTypes.STRING,
        allowNull: false
    },
    lastName: {
        type: DataTypes.STRING,
        allowNull: false
    },
    password: {
        type: DataTypes.STRING,
        allowNull: false
    }
}, {
    sequelize,
    tableName: 'users'
});

export default User;

```

### routes/authRoutes.ts
```ts
import express, { Request, Response } from 'express';
import jwt from 'jsonwebtoken';
import bcrypt from 'bcryptjs';
import User from '../models/userModel';

const router = express.Router();
const jwtSecret = 'secretPolice'; // Replace with your actual secret key

// Registration route
router.get('/register', (req: Request, res: Response) => {
    res.render('register', { title: 'Register' });
});

router.post('/register', async (req: Request, res: Response) => {
    const { email, firstName, lastName, password } = req.body;

    try {
        const hashedPassword = await bcrypt.hash(password, 10);
        await User.create({ email, firstName, lastName, password: hashedPassword });
        res.redirect('/auth/login');
    } catch (error) {
        console.error('Error registering user:', error);
        res.render('error', { title: 'Error', message: 'Error registering user' });
    }
});

// Login route
router.get('/login', (req: Request, res: Response) => {
    res.render('login', { title: 'Login' });
});

// Login route
router.post('/login', async (req: Request, res: Response) => {
    const { email, password } = req.body;

    try {
        const user = await User.findOne({ where: { email } });
        if (!user || !(await bcrypt.compare(password, user.password))) {
            return res.render('error', { title: 'Login Error', message: 'Invalid credentials' });
        }

        const token = jwt.sign({ id: user.id, email: user.email, firstName: user.firstName }, jwtSecret, { expiresIn: '1h' });

        console.log('Generated Token:', token); // Debug log

        res.cookie('token', token, { httpOnly: true, secure: false }); // For HTTP, use secure: false
        res.redirect('/welcome');
    } catch (error) {
        console.error('Error logging in:', error);
        res.render('error', { title: 'Error', message: 'Error logging in' });
    }
});


export default router;

```
### routes/protectedRoutes.ts
```ts
import express, { Request, Response } from 'express';
import { verifyToken } from '../middleware/jwtMiddleware';

const router = express.Router();

// Protected route
router.get('/welcome', verifyToken, (req: Request, res: Response) => {
    res.json({ message: `Welcome, ${req.user.username}` });
});

export default router;

```

### types/express.d.ts
```ts
import { User } from '../models/userModel'; // Adjust the path to your User model

declare global {
    namespace Express {
        interface Request {
            user?: User; // Adjust the type as needed, or use `any` if you prefer
        }
    }
}

```

### views/error.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><%= title %></title>
</head>
<body>
    <h1><%= title %></h1>
    <p><%= message %></p>
    <a href="/">Back to Home</a>
</body>
</html>

```
### views/index.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Login</title>
</head>
<body>
    <nav>
        <a href="/auth/register">Register</a>
        <a href="/auth/login">Login</a>
    </nav>
</body>
</html>
```
### views/login.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><%= title %></title>
</head>
<body>
    <h1>Login</h1>
    <form action="/auth/login" method="POST">
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required>
        <br>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required>
        <br>
        <button type="submit">Login</button>
    </form>
    <a href="/">Back to Home</a>
</body>
</html>

```
### views/register.ejs
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
    <form action="/auth/register" method="POST">
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required>
        <br>
        <label for="firstName">First Name:</label>
        <input type="text" id="firstName" name="firstName" required>
        <br>
        <label for="lastName">Last Name:</label>
        <input type="text" id="lastName" name="lastName" required>
        <br>
        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required>
        <br>
        <button type="submit">Register</button>
    </form>
    <a href="/">Back to Home</a>
</body>
</html>

```
### views/welcome.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Welcome</title>
</head>
<body>
    <h1>Welcome!</h1>
    <p>Welcome back, <%= username %>!</p>
</body>
</html>

```

### server.ts
```ts
import express from 'express';
import bodyParser from 'body-parser';
import cookieParser from 'cookie-parser'; // Import cookie-parser
import authRoutes from './routes/authRoutes';
import path from 'path';
import jwt from 'jsonwebtoken';

const app = express();
const port = 3000;
const jwtSecret = 'secretPolice'; // Replace with your actual secret key

app.set('view engine', 'ejs');
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));
app.set('views', path.join(__dirname, '..', 'src', 'views'));
app.use(express.urlencoded({ extended: true }));
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.use(cookieParser()); // Use cookie-parser middleware

// Define routes
app.use('/auth', authRoutes);

// Define a root route
app.get('/', (req, res) => {
    res.render('index', { title: 'Home Page' });
});

// Token verification middleware
const authenticateToken = (req: express.Request, res: express.Response, next: express.NextFunction) => {
    const token = req.cookies.token;
    
    if (!token) return res.redirect('/auth/login');
    
    jwt.verify(token, jwtSecret, (err: any, user: any) => {
        if (err) {
            console.error('JWT Verify Error:', err);
            return res.redirect('/auth/login');
        }
        req.user = user;
        next();
    });
};

// Protected route using authenticateToken middleware
app.get('/welcome', authenticateToken, (req, res) => {
    res.render('welcome', { title: 'Welcome', username: req.user.firstName });
});

// Error handling middleware
app.use((err: any, req: express.Request, res: express.Response, next: express.NextFunction) => {
    console.error(err.stack);
    res.status(500).render('error', { title: 'Error', message: 'Something went wrong!' });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
});

```
