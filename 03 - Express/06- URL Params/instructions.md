### Assignment: Handling URL Parameters with Express.js and EJS

Create an Express.js application that dynamically handles URL parameters and renders corresponding data using EJS templating.

![/10%20-%20Assets/URLParameters.png](/10%20-%20Assets/URLParameters.png)

**Estimated Time to Completion:** 60 minutes

**Level of Complexity:** Beginner

**Instructions:**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives:**

- Learn to set up and configure a TypeScript-based Express project.
- Implement routing to manage and utilize URL parameters.

---

**Directions:**

Set up the project with TypeScript, Express.js, and EJS. Configure middleware for EJS and URL parameter parsing. Create GET routes to display a color from the URL and double a number from the URL, rendering these results in EJS templates.

**MVP Requirements: Implementing Dynamic Routes with EJS in Express**

- **Create the Express Application**
    1. **Configure Middleware:**
        - Set up middleware to use EJS and parse URL parameters.
    2. **Implement GET Routes:**
        - Create the following routes:
            - *GET /color/:color*: Render an EJS template that displays the color from the URL parameter and optionally changes the font color.
            - *GET /number/:number*: Render an EJS template that doubles the number from the URL parameter and shows the result.

**Expected Outputs:**

- A web application with two dynamic routes:
    - **/color/:color**: Displays the color passed in the URL and changes the font color accordingly.
    - **/number/:number**: Doubles the number passed in the URL and displays the result.

**Additional Notes:**

- Enhance the design by adding CSS styles to the HTML files.
- Explore additional EJS features like conditional statements and includes.
- Add error handling for invalid URL parameters if needed.