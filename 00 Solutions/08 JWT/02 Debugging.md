### middleware/authMiddleware.ts
```ts
import { Request, Response, NextFunction } from 'express';
import jwt from 'jsonwebtoken';

const secretKey = 'secretPolice';

/**
 * Middleware function to authenticate requests using JWT token.
 *
 * @param req - The Express request object.
 * @param res - The Express response object.
 * @param next - The next middleware function.
 * @returns A response indicating whether the request is authenticated or not.
 */
const authMiddleware = (req: Request, res: Response, next: NextFunction) => {
	const token = req.header('Authorization')?.replace('Bearer ', '');

	if (!token) {
		return res.status(401).send('Access denied.');
	}

	try {
		const decoded = jwt.verify(token, secretKey);
		req.user = decoded; // Attach the decoded token data to the request object
		next();
	} catch (err) {
		res.status(400).send('Invalid token.');
	}
};

export default authMiddleware;
```

### models/User.ts
```ts
import { Model, DataTypes } from 'sequelize';
import sequelize from '../config/database';

/**
 * Represents a User model.
 *
 * @class
 * @extends Model
 */
class User extends Model {
    public id!: number;
    public email!: string;
    public password!: string;
}

User.init(
    {
        id: {
            type: DataTypes.INTEGER,
            autoIncrement: true,
            primaryKey: true,
        },
        email: {
            type: DataTypes.STRING,
            unique: true,
            allowNull: false,
        },
        password: {
            type: DataTypes.STRING,
            allowNull: false,
        },
    },
    {
        sequelize,
        modelName: 'User',
    }
);

export default User;
```

### routes/tokenRoutes.ts
```ts
import { Router, Request, Response } from 'express';
import jwt from 'jsonwebtoken';

const router = Router();
const secretKey = 'secretPolice';

// Refresh Token
router.post('/refresh', (req: Request, res: Response) => {
    const { token } = req.body;

    try {
        /**
         * Decodes a JWT token using the provided secret key.
         * 
         * @param token - The JWT token to decode.
         * @param secretKey - The secret key used to decode the token.
         * @returns The decoded payload of the JWT token.
         */
        const decoded = jwt.verify(token, secretKey, { ignoreExpiration: true }) as jwt.JwtPayload;
        const newToken = jwt.sign({ id: decoded.id }, secretKey, { expiresIn: '1h' });
        res.send({ token: newToken });
    } catch (err) {
        res.status(400).send('Invalid token.');
    }
});

export default router;
```

### routes/userRoutes.ts
```ts
import { Router, Request, Response } from 'express';
import bcrypt from 'bcryptjs';
import jwt from 'jsonwebtoken';
import User from '../models/User';

const router = Router();
const secretKey = 'secretPolice';

// Registration
router.post('/register', async (req: Request, res: Response) => {
    const { email, password } = req.body;

    try {
        const hashedPassword = await bcrypt.hash(password, 10);
        const user = await User.create({ email, password: hashedPassword });
        res.status(201).send(user);
    } catch (err) {
        res.status(400).send('Error registering user.');
    }
});

// Login
router.post('/login', async (req: Request, res: Response) => {
    const { email, password } = req.body;

    try {
        const user = await User.findOne({ where: { email } });
        if (!user || !(await bcrypt.compare(password, user.password))) {
            return res.status(400).send('Invalid credentials.');
        }

        /**
         * Generates a JWT token for the given user ID.
         *
         * @param {number} id - The user ID.
         * @returns {string} - The generated JWT token.
         */
        const token = jwt.sign({ id: user.id }, secretKey, { expiresIn: '1h' });
        res.send({ token });
    } catch (err) {
        res.status(500).send('Error logging in.');
    }
});

export default router;
```

### types/express.d.ts
```ts
import { User } from '../models/userModel';

declare global {
    namespace Express {
        interface Request {
            user?: User;
        }
    }
}
```

### views/index.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>JWT Authentication Test</title>
    <style>
        body {
            font-family: Arial, sans-serif;
        }
        form {
            margin-bottom: 20px;
        }
        input {
            margin-right: 10px;
        }
    </style>
</head>
<body>
    <h1>JWT Authentication Test</h1>

    <!-- Registration Form -->
    <h2>Register</h2>
    <form action="/api/users/register" method="POST">
        <input type="email" name="email" placeholder="Email" required>
        <input type="password" name="password" placeholder="Password" required>
        <button type="submit">Register</button>
    </form>

    <!-- Login Form -->
    <h2>Login</h2>
    <form action="/api/users/login" method="POST">
        <input type="email" name="email" placeholder="Email" required>
        <input type="password" name="password" placeholder="Password" required>
        <button type="submit">Login</button>
    </form>

    <!-- Token Refresh Form -->
    <h2>Refresh Token</h2>
    <form action="/api/tokens/refresh" method="POST">
        <input type="text" name="token" placeholder="Old Token" required>
        <button type="submit">Refresh Token</button>
    </form>

    <!-- Access Protected Route -->
    <h2>Access Protected Route</h2>
    <form action="/welcome" method="GET">
        <input type="text" name="token" placeholder="Token" required>
        <button type="submit">Access Protected Route</button>
    </form>

    <p><strong>Note:</strong> To access protected routes, you need to include a valid token in the form field.</p>

    <!-- Display messages -->
    <% if (message) { %>
        <p><%= message %></p>
    <% } %>
</body>
</html>
```

### server.ts
```ts
import express from 'express';
import bodyParser from 'body-parser';
import path from 'path';
import userRoutes from './routes/userRoutes';
import tokenRoutes from './routes/tokenRoutes';
import authMiddleware from './middleware/authMiddleware';
import sequelize from './config/database';

const app = express();

// Set up EJS
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, '..', 'src', 'views'));

app.use(bodyParser.urlencoded({ extended: true })); // Handle form submissions

app.use('/api/users', userRoutes);
app.use('/api/tokens', tokenRoutes);

// Serve the main view
app.get('/', (req, res) => {
    res.render('index', { message: req.query.message });
});

// Protected route example
app.get('/welcome', authMiddleware, (req, res) => {
    res.send('Welcome to the protected route!');
});

const PORT = process.env.PORT || 3000;

app.listen(PORT, async () => {
    console.log(`Server running on port ${PORT}`);
    try {
        await sequelize.authenticate();
        console.log('Database connected.');
    } catch (err) {
        console.error('Database connection error:', err);
    }
});
```

### sync.ts
```ts
import sequelize from './config/database'; // Import your Sequelize instance
import './models';

sequelize.sync({ force: false })
    .then(() => {
        console.log('Database synchronized');
        process.exit(0); // Exit the script after syncing
    })
    .catch((error: Error) => {
        console.error('Error syncing the database:', error);
        process.exit(1); // Exit the script with an error code
    });
```
