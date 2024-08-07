### middleware/jwtMiddleware.ts
```ts
import dotenv from 'dotenv';
import jwt from 'jsonwebtoken';

dotenv.config();
const secretKey = process.env.JWT_SECRET || 'default_secret_key';

export const generateToken = (counter: number) => {
    return jwt.sign({ counter }, secretKey, { expiresIn: '1h' });
};
```

### server.ts
```ts
// src/server.ts
import express from 'express';
import path from 'path';
import cookieParser from 'cookie-parser';
import { generateToken } from './middleware/jwtMiddleware';

const app = express();
const port = 3000;

app.set('view engine', 'ejs');
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));
app.set('views', path.join(__dirname, '..', 'src', 'views'));
app.use(express.urlencoded({ extended: true }));
app.use(cookieParser());

let counter = 0; // Initial counter value

app.get('/', (req, res) => {
    res.render('index', { counter });
});

app.post('/increase', (req, res) => {
    counter++;
    const token = generateToken(counter);
    res.cookie('token', token);
    res.redirect('/');
});

app.post('/decrease', (req, res) => {
    counter--;
    const token = generateToken(counter);
    res.cookie('token', token);
    res.redirect('/');
});

app.listen(port, () => {
    console.log(`Server is running on http://localhost:${port}`);
});

```

### views/index.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Counter Application</title>
</head>
<body>
    <h1>Counter: <%= counter %></h1>
    <form action="/increase" method="POST">
        <button type="submit">Increase</button>
    </form>
    <form action="/decrease" method="POST">
        <button type="submit">Decrease</button>
    </form>
</body>
</html>

```