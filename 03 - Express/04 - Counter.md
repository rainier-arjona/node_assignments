### Assignment: Counter (Express session)

Create a simple counter application using Express.js, TypeScript, and sessions. The application will have two buttons: one to increase the counter and one to decrease it. Each button will have its own URL route to handle the increase or decrease action. The main page will display the current counter value each time.

![/10%20-%20Assets/Counter.png](/10%20-%20Assets/Counter.png)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Medium

**Instructions:**

1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives:**

- **Set up an Express.js application with TypeScript:** Learn to configure and structure a TypeScript-based Express project.
- **Configure basic routing in Express.js:** Implement basic routing to handle different URL requests.
- **Utilize sessions to persist data across requests:** Understand how to maintain state across different HTTP requests using sessions.
- **Use EJS templating to render dynamic HTML:** Leverage EJS to dynamically generate HTML content based on server-side data.
- **Implement GET routes to handle counter actions:** Create routes to increase, decrease, and display the counter value.

**Directions**

1. **Set-up the project**
2. **Create the Express Application**
    - **Configure Session Middleware:**
        - Configure the session middleware in your Express application to manage session data.
    - **Create Routes:**
        - Create three routes:
            - A root route (`/`) to display the current counter value.
            - An increase route (`/increase`) to increment the counter.
            - A decrease route (`/decrease`) to decrement the counter.
    - **Implement Session Logic:**
        - Use sessions to store and update the counter value across requests.
3. **Create EJS Templates**
    - **Main Page Template (`index.ejs`):**
        - Create an EJS template to display the current counter value and the two buttons for increasing and decreasing the counter.

**Expected Output:**

- The application should be accessible at `http://localhost:3000`.
- The main page should display the current counter value and two buttons.
- Clicking the "Increase" button should increment the counter and refresh the page to show the updated value.
- Clicking the "Decrease" button should decrement the counter and refresh the page to show the updated value.

**Additional Notes:**

- Ensure your session configuration is secure and suitable for your development environment.
- Test each route thoroughly to confirm that the counter updates correctly and persists across requests.

---

**Solutions**

**src/server.ts**

```tsx
import express, { Request, Response } from 'express';
import path from 'path';
import session from 'express-session';

const app = express();
const port = 3000;

// Set EJS as the view engine
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, 'views'));

// Configure session middleware
app.use(session({
    secret: 'your_secret_key', // Replace with your own secret key
    resave: false,
    saveUninitialized: true,
    cookie: { secure: false } // Set to true if using HTTPS
}));

// Extend session type
declare module 'express-session' {
    interface SessionData {
        counter: number;
    }
}

// Initialize counter in session
app.use((req: Request, res: Response, next) => {
    if (req.session.counter === undefined) {
        req.session.counter = 0;
    }
    next();
});

// Define routes
app.get('/', (req: Request, res: Response) => {
    res.render('index', { counter: req.session.counter });
});

app.get('/increase', (req: Request, res: Response) => {
    req.session.counter++;
    res.redirect('/');
});

app.get('/decrease', (req: Request, res: Response) => {
    req.session.counter--;
    res.redirect('/');
});

app.listen(port, () => {
    console.log(`Server is running at <http://localhost>:${port}`);
});

```

**src/views/index.ejs**

```tsx
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Counter App</title>
</head>

<body>
    <h1>Counter Value: <%= counter %></h1>
    <form action="/increase" method="get">
        <button type="submit">Increase</button>
    </form>
    <form action="/decrease" method="get">
        <button type="submit">Decrease</button>
    </form>
</body>

</html>

```