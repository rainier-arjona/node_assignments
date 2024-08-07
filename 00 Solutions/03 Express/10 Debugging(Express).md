### server.ts

```ts
import express, { Request, Response } from 'express';
import path from 'path';
import bodyParser from 'body-parser';
import session from 'express-session';

const app = express();
const port = 3000;

// body parser
app.use(bodyParser.urlencoded({ extended: true }));

// Set EJS as the view engine
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, '..', 'src', 'views'));

// Configure session middleware
app.use(session({
    secret: 'secretPolice', // Replace with your own secret key
    resave: false,
    saveUninitialized: true,
    cookie: { secure: false } // Set to true if using HTTPS
}));

// Extend session type
declare module 'express-session' {
    interface SessionData {
        enrollment_data: {
            name: string;          // Fixed type
            email: string;         // Fixed type
            number: string;        // Fixed type
            course: string;        // Fixed type
            start_date: string;    // Fixed type
        };
    }
}

// Define a route to render an EJS template
app.get('/', (req: Request, res: Response) => {
    res.render("index");
});

app.post("/submit", (req: Request, res: Response) => {
    req.session.enrollment_data = {
        name: req.body.name,
        email: req.body.email,
        number: req.body.number,
        course: req.body.course,
        start_date: req.body.start_date
    };
    res.redirect("/resume");
});

app.get("/resume", (req: Request, res: Response) => {
    // Retrieve data from session
    const enrollment_data = req.session.enrollment_data;

    // Render the resume view with the data
    if (enrollment_data) {  // Check if enrollment_data exists
        res.render("resume", enrollment_data);
    } else {
        res.status(404).send('Data not found'); // Return an error if no data is found
    }
});

app.listen(port, () => {
    console.log(`Server is running at http://localhost:${port}`);
});
```

### index.ejs
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Course Enrollment Form</title>
</head>

<body>
    <div class="border">
        <h1>Course Enrollment Form</h1>
        <form action="/submit" method="POST">
            <label for="name">Full Name:</label>
            <input type="text" id="name" name="name" required><br><br>

            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required><br><br>

            <label for="number">Phone Number:</label>
            <input type="tel" id="number" name="number" required><br><br>

            <label for="course">Course:</label>
            <input type="text" id="course" name="course" required><br><br>

            <label for="start_date">Start Date:</label>
            <input type="date" id="start_date" name="start_date" required><br><br>

            <input type="submit" value="Submit">
        </form>
    </div>
</body>

</html>
```

### resume.ejs
```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Enrollment Details</title>
    </head>
    <body>
        <div class="border">
            <h1>Enrollment Details</h1>
            <p>Full Name: <%= enrollment_data.name %></p>  <!-- Fixed placeholder -->
            <p>Email: <%= enrollment_data.email %></p>  <!-- Fixed placeholder -->
            <p>Phone Number: <%= enrollment_data.number %></p>  <!-- Fixed placeholder -->
            <p>Course: <%= enrollment_data.course %></p>  <!-- Fixed placeholder -->
            <p>Start Date: <%= enrollment_data.start_date %></p>  <!-- Fixed placeholder -->
            <a href="/">Return</a>
        </div>
    </body>
</html>
```

## Outline of Fixes
1 .Type Definitions in server.ts:
- Updated the SessionData type in express-session to reflect the correct data types (string for all fields).

2. Session Data Handling in server.ts:
- Added a check in the /resume route to handle cases where enrollment_data might not be set. If enrollment_data is not found, return a 404 error message.

3. EJS Template Fixes:
- Corrected the placeholders in resume.ejs to match the session data keys. The placeholders now use the correct variable names (<%= enrollment_data.name %>, etc.).