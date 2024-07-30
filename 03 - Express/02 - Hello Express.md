# Hello Express

Construct a dynamic personal portfolio website using Express.js and EJS that displays details about a person. Utilize Express.js routing to serve this information on the root route of your website and render the content using EJS templating.

---

![Hello Express](/10%20-%20Assets/HelloExpress.png)

**Estimated Time to Completion:** 120 minutes

**Level of Complexity:** Medium

**Instructions:**

1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your code for evaluation.

**Evaluation Criteria & Learning Objectives:**

- Establish an Express.js application with TypeScript
- Configure fundamental routing
- Serve static files (CSS, images)
- Employ EJS templating to render dynamic HTML
- Pass JSON data to EJS templates

---

**Directions**

**Create the Express Application:**

1. Set up an Express application using the `express` module in TypeScript.
2. Define essential middleware for parsing JSON data and using EJS as the template engine.
3. Establish a port for the server to listen on.

**Implement Basic Routing:**

1. Create a route handler for the root path (`/`) to serve the portfolio data.
2. Render the `index.ejs` template for the root route, passing the necessary data.

**Integrate JSON Data:**

1. Create a TypeScript object containing the details about John (name, age, occupation, email, address).
2. Pass this object to the EJS template to dynamically populate the content.

**Create EJS Template:**

1. Design an `index.ejs` template to display John's details.
2. Use EJS syntax to render data passed from the route handler.

**Example Code Structure:**

**TypeScript Express Application (app.ts):**

```tsx
import express, { Request, Response } from 'express';
import path from 'path';

const app = express();
const port = 3000;

// Middleware for parsing JSON and using EJS
app.set('view engine', 'ejs');
app.use(express.static(path.join(__dirname, 'public')));

// Define JSON data for John (missing parts)
// TODO: Complete the JSON data

// Route handler for root path
app.get('/', (req: Request, res: Response) => {
  // TODO: Pass the JSON data to the EJS template
  res.render('index', { john: /* TODO: Add data here */ });
});

app.listen(port, () => {
  console.log(`Server listening on port ${port}`);
});
```

**Expected Output:**
A dynamic personal portfolio website accessible at `http://localhost:3000`. The site should display:

- John’s name, age, occupation, email, and address information.

**Additional Notes:**

- Ensure that all static files (CSS, images) are served correctly from the `public` directory.
- Feel free to style the page as per your preference.
- Explore additional EJS features or advanced routing techniques if desired.