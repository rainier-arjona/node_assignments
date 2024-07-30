# My Portfolio

In this assignment, you'll build a basic personal portfolio website using Express.js and TypeScript. Create these pages from the wireframe below, use Express.js routing to manage distinct pages, and integrate JSON data to dynamically populate content within specific sections. You will also use EJS as a template engine to render dynamic content.

---

![My Portfolio.png](/10%20-%20Assets/MyPortfolio.png)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your code for evaluation.

**Evaluation Criteria & Learning Objectives**

- Implement routing with Express.js and TypeScript
- Serve static files (HTML, CSS, images)
- Integrate JSON data into routes
- Utilize a template engine for dynamic content (optional)

---

**Directions**

Build a personal portfolio website using Express.js and TypeScript.

**MVP Requirements: Portfolio Website**

- **Create Routes**: Set up route handlers for each page of the portfolio:
    - Home
    - About
    - Contact
    - Skills
- **Serve Static Files**: Use Express to serve static HTML, CSS, and image files.
- **Integrate JSON Data**:
    - Create a JSON file (`portfolio.json`) containing data such as skills and projects.
    - Read and use this JSON data within your routes to dynamically populate the content.

Example JSON data (`portfolio.json`):

**Example Code Structure:**

`portfolio-website/
├── data/
│   └── skills.json
├── public/
│   ├── css/
│   └── images/
├── views/
│   ├── home.ejs
│   ├── about.ejs
│   ├── contact.ejs
│   └── skills.ejs
├── app.js
└── package.json`

Example JSON data (`portfolio.json`):

```json
{
    "skills": [
      "JavaScript",
      "TypeScript",
      "Node.js",
      "Express",
      "HTML",
      "CSS"
    ],
    "projects": [
      {
        "title": "Project One",
        "description": "A description of the first project."
      },
      {
        "title": "Project Two",
        "description": "A description of the second project."
      }
    ],
    "contact": {
      "email": "example@example.com",
      "phone": "+1234567890"
    }
  }
```

```tsx
import express, { Request, Response } from 'express';
import path from 'path';
import fs from 'fs';

const app = express();
const port = 3000;

// Serve static files
app.use(express.static(path.join(__dirname, 'public')));

// Read JSON data
const portfolioData = JSON.parse(fs.readFileSync(path.join(__dirname, 'portfolio.json'), 'utf8'));

// Routes
app.get('/', (req: Request, res: Response) => {
  res.sendFile(path.join(__dirname, 'views', 'home.html'));
});

app.get('/about', (req: Request, res: Response) => {
  res.sendFile(path.join(__dirname, 'views', 'about.html'));
});

app.get('/contact', (req: Request, res: Response) => {
  res.sendFile(path.join(__dirname, 'views', 'contact.html'));
});

app.get('/skills', (req: Request, res: Response) => {
  res.json(portfolioData.skills);
});

app.listen(port, () => {
  console.log(`Server is running on http://localhost:${port}`);
});
```

**Expected Output:**

A functional personal portfolio website accessible at `http://localhost:3000`. The website should exhibit the following:

- **Home Page**: Served from `home.html` in the `views` directory.
- **About Page**: Served from `about.html` in the `views` directory.
- **Contact Page**: Served from `contact.html` in the `views` directory.
- **Skills Page**: Returns JSON data from `portfolio.json`.

**Additional Notes:**

- Feel free to customize the wireframe and add more pages or sections as needed.