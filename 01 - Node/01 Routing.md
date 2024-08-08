# Assignment: Node.js Routing

In this assignment, you'll build a Node.js application to demonstrate basic routing using the built-in `http` module. Your goal is to create various routes that return specific strings when accessed.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. **Setup:**
    - Create a new Node.js application.
    - Use the built-in `http` module to create a server that listens for incoming requests.
2. **Routes:**
    - Implement the following routes in your Node.js application:
        - **Static Routes:**
            - When the user visits `/contact`, return the string **"Contact Us"** as the response.
            - When the user visits `/about`, return the string **"About Us"** as the response.
            - When the user visits `/services`, return the string **"Our Services"** as the response.
            - When the user visits `/`, return the string **"Welcome to our website!"** as the response.
            - When the user visits `/pricing`, return the string **"Our Pricing"** as the response.
3. **Submission:**
    - Ensure that your server is properly set up and all routes return the correct strings.
    - Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives**

- Create a Node.js application using the `http` module.
- Implement routing for various endpoints and verify correct responses.
- Understand basic routing and server setup in Node.js.

**Expected Outputs**

- Accessing `http://localhost:3000/contact` should display **"Contact Us"**.
- Accessing `http://localhost:3000/about` should display **"About Us"**.
- Accessing `http://localhost:3000/services` should display **"Our Services"**.
- Accessing `http://localhost:3000/` should display **"Welcome to our website!"**.
- Accessing `http://localhost:3000/pricing` should display **"Our Pricing"**.

**Stretch Requirements:**

- Consider implementing additional routes or functionalities to further enhance your Node.js application. For example, you could add a route that returns the current server time.
