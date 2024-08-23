### Assignment: EJS Routing

Create a basic web application using Express.js and EJS to replicate the provided wireframe layout. Implement GET routes to serve different pages and content. Utilize EJS templating to dynamically render HTML content.

![/10%20-%20Assets/EJSTemplating.png](/10%20-%20Assets/EJSTemplating.png)

Image assets here: [**Image Assets**](https://drive.google.com/file/d/11CKo4D0aiGPdYYKCNWbxu2K6dRBcLqsH/view?usp=sharing)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Beginner

**Instructions:**

1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives:**

- **Configure basic routing:** Set up Express routes to handle different URLs.
- **Serve static files:** Serve images and other static assets using Express.
- **Utilize EJS templating:** Use EJS to render dynamic HTML content.
- **Render dynamic content based on provided data:** Pass data to EJS templates to display dynamic content.

**Directions:**

**1. Set Up the Project**

- Set up your Express.js project.

**2. Create the Express Application**

- **Configure Middleware:**
    - Configure essential middleware for using EJS and serving static files.
- **Implement GET Routes:**
    - Create the following routes:
        - **GET /**: Serve the EJS template file named `index.ejs` located in the `views` folder, and serve static assets such as images from the `public` folder.
        - **GET /weather**: Render an EJS template named `weather.ejs`. Pass weather data to the template.
        - **GET /products**: Render an EJS template named `products.ejs`. Pass a list of products to the template.

**3. Create EJS Templates**

- **Main Page Template (`index.ejs`):** Create an EJS template to display a gallery of images on the home page, where the image URLs and titles are provided by the server.
- **Weather Page Template (`weather.ejs`):** Create an EJS template to display the weather data (static).
- **Products Page Template (`products.ejs`):** Create an EJS template to display a list of products using an EJS loop.

**Expected Output:**

- A web application with three pages:
    - **Home page** with links to weather and products.
    - **Weather page** displaying temperature and conditions.
    - **Products page** displaying a list of products.

**Additional Notes:**

- You can enhance the design by adding CSS styles to the HTML files.