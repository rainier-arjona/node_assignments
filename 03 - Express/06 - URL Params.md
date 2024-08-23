### Assignment: Handling URL Parameters with Express.js and EJS

Create an Express.js application that dynamically handles URL parameters and renders corresponding data using EJS templating.

![/10%20-%20Assets/URLParameters.png](/10%20-%20Assets/URLParameters.png)

**Estimated Time to Completion:** 60 minutes

**Level of Complexity:** Beginner

**Instructions:**

1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives:**

- **Create an Express.js application using TypeScript:** Learn to set up and configure a TypeScript-based Express project.
- **Configure basic routing to handle URL parameters:** Implement routing to manage and utilize URL parameters.
- **Utilize EJS templating to render dynamic content:** Use EJS templates to dynamically display data based on URL parameters.
- **Implement GET routes with URL parameters:** Develop GET routes to handle and process URL parameters effectively.

**Directions:**

1. **Set Up the Project**
    - Set up the project with TypeScript, Express.js, and EJS.
2. **Create the Express Application**
    - **Configure Middleware:**
        - Set up middleware to use EJS and parse URL parameters.
    - **Implement GET Routes:**
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