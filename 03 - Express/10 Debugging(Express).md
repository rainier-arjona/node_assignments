Assignment: Debugging Express Application
## Assignment: Debugging (Express)

In this assignment, you'll improve your debugging skills by identifying and fixing issues in a provided Express application. Your goal is to make sure the application functions correctly and meets the specified requirements.

![ERD](../10%20-%20Assets/Debugging(express).png)

**Estimated Time to Completion:** 60 minutes

**Level of Complexity:** Medium

### Instructions

1. Read through the provided code and instructions. You will be given files to work with.
2. Identify and fix issues in the provided Express application code.
3. Test the application to ensure it functions as expected.
4. Submit your GitHub URL by the due date.

### Evaluation Criteria & Learning Objectives

- Correctly identify and resolve issues in Express route handlers and middleware.
- Ensure proper session handling and data retrieval.
- Validate EJS templates to ensure dynamic data is rendered correctly.

### Provided Code

**server.ts**
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
            name: number;
            email: boolean;
            number: number;
            course: boolean;
            start_date: date;
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
    res.render("resume", enrollment_data);
});

app.listen(port, () => {
    console.log(`Server is running at http://localhost:${port}`);
});
```

**views/index.ejs**
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

**views/resume.ejs**
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
            <p>Full Name: <%= names %></p>
            <p>Email: <%= email %></p>
            <p>Phone Number: <% number %></p>
            <p>Course: <%= courses %></p>
            <p>Start Date: <% start_date %></p>
            <a href="/">Return</a>
        </div>
    </body>
</html>
```

### Assignment Tasks

1. **Review the Code:**
   - Examine the `server.ts` file and the EJS templates (`index.ejs` and `resume.ejs`) to understand their functionality.
2. **Identify and Fix Issues:**
   - In `server.ts`:
     - Check Route Handlers: Ensure the `/submit` route correctly stores session data. Verify that the `/resume` route correctly retrieves and displays session data.
     - Fix Type Definitions: Make sure the session data type definitions are accurate.
     - Correct Import Errors: Address any issues with importing and using modules.
   - In `index.ejs` and `resume.ejs`:
     - Check Placeholders: Ensure that the EJS templates use correct syntax for placeholders and variables.
     - Verify Form Handling: Confirm that form data is properly captured and submitted.
3. **Test the Application:**
   - Run the server and test the form submission and data display functionality.
   - Ensure that data is correctly stored in the session and rendered on the `/resume` page.
4. **Submit Your Work:**
   - Zip your updated project and submit it by the due date.
   - Include a brief description of the issues you identified and how you resolved them.

### Expected Outcomes

- The application should correctly render the form on the `/` route.
- Data submitted via the form should be displayed correctly on the `/resume` route.

### Hints for Debugging

- Verify that the session data is correctly assigned and retrieved using `req.session`.
- Ensure that EJS placeholders in `resume.ejs` match the data keys.
- Look out for any error messages or issues in the console and address them.
