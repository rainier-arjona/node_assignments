# Handling URL Parameters with Express.js and EJS

Create an Express.js application that dynamically handles URL parameters and renders corresponding data using EJS templating.

---

![URL Parameters](/10%20-%20Assets/URLParameters.png)

**Estimated Time to Completion:** 60 minutes

**Level of Complexity:** Beginner

---

**Instructions:**

1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your code for evaluation.

**Evaluation Criteria & Learning Objectives:**

- Create an Express.js application using TypeScript
- Configure basic routing to handle URL parameters
- Utilize EJS templating to render dynamic content
- Implement GET routes with URL parameters

---

**Directions:**

### 1. Set Up the Project

**Note:** You have already learned how to set up an Express.js project with TypeScript, so the basic setup steps are omitted.

### 2. Create the Express Application

1. **Configure Middleware:**
    - Configure essential middleware for using EJS and parsing URL parameters.
2. **Implement GET Routes:**
    - Create the following routes:
        - **GET /color/**: Render an EJS template that prints the color from the URL parameter and optionally changes the font color to the provided color.
        - **GET /number/**: Render an EJS template that doubles the number from the URL parameter and displays the result.

---

**Expected Outputs:**

- A web application with two dynamic routes:
    - **/color/**: Displays the color passed in the URL and changes the font color accordingly.
    - **/number/**: Doubles the number passed in the URL and displays the result.
    

**Additional Notes:**

- You can enhance the design by adding CSS styles to the HTML files.
- Explore more complex EJS features like conditional statements and includes.
- Consider adding error handling for invalid URL parameters.