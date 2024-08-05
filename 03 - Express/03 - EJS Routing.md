# EJS Routing

Create a basic web application using Express.js and EJS to replicate the provided wireframe layout.
Implement GET routes to serve different pages and content.
Utilize EJS templating to dynamically render HTML content.

---

![EJS Routing](/10%20-%20Assets/EJSTemplating.png)

[**Image Assets**](https://drive.google.com/file/d/11CKo4D0aiGPdYYKCNWbxu2K6dRBcLqsH/view?usp=sharing)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Beginner

**Instructions:**

1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your code for evaluation.

**Evaluation Criteria & Learning Objectives:**

- Configure basic routing
- Serve static files
- Utilize EJS templating
- Render dynamic content based on provided data

---

**Directions:**

### 1. Set Up the Project

**Note:** You have already learned how to set up an Express.js project with TypeScript, so the basic setup steps are omitted.

### 2. Create the Express Application

1. **Configure Middleware:**
    - Configure essential middleware for using EJS and serving static files.
2. **Implement GET Routes:**
    - Create the following routes:
        - **GET /**: Serve a static HTML file named `index.html` located in a `public` folder.
        - **GET /weather**: Render an EJS template named `weather.ejs`. Pass weather data to the template.
        - **GET /products**: Render an EJS template named `products.ejs`. Pass a list of products to the template.

### 3. Create EJS Templates

1. **Main Page Template (`index.ejs`):**
    - Create an EJS template to display the home page with links to the weather and products pages.
2. **Weather Page Template (`weather.ejs`):**
    - Create an EJS template to display the weather data.
3. **Products Page Template (`products.ejs`):**
    - Create an EJS template to display a list of products using an EJS loop.

---

**Expected Output:**

- A web application with three pages:
    - **Home page** with links to weather and products.
    - **Weather page** displaying temperature and conditions.
    - **Products page** displaying a list of products.

**Additional Notes:**

- You can enhance the design by adding CSS styles to the HTML files.
