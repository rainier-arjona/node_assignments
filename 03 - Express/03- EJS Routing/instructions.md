### Assignment: EJS Routing

Create a basic web application using Express.js and EJS to replicate the provided wireframe layout. Implement GET routes to serve different pages and content. Utilize EJS templating to dynamically render HTML content.

![/10%20-%20Assets/EJSTemplating.png](/10%20-%20Assets/EJSTemplating.png)

Image assets here: [**Image Assets**](https://drive.google.com/file/d/11CKo4D0aiGPdYYKCNWbxu2K6dRBcLqsH/view?usp=sharing)

**Estimated Time to Completion:** 90 minutes

**Level of Complexity:** Beginner

**Instructions:**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives:**

- Create GET routes with JSON and HTML file responses.
- Implement EJS Templating.

---

**Directions:**

Set up your Express.js project. Configure middleware for EJS and static files. Implement the required GET routes to serve EJS templates for the main page, weather page, and products page. Create EJS templates to display images, weather data, and a product list.

**MVP Requirements: EJS templates and Routes**

- Create the Express Application
    1. **Configure Middleware:**
        - Configure essential middleware for using EJS and serving static files.
    2. **Implement GET Routes:**
        - Create the following routes:
            - **GET /**: Serve the EJS template file named `index.ejs` located in the `views` folder, and serve static assets such as images from the `public` folder.
            - **GET /weather**: Render an EJS template named `weather.ejs`. Pass weather data to the template.
            - **GET /products**: Render an EJS template named `products.ejs`. Pass a list of products to the template.

- Create EJS Templates

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