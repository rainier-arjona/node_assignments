### Assignment: Node.js Routing

In this assignment, you'll build a Node.js application to demonstrate basic routing using the built-in `http` module. Your goal is to create various routes that return specific strings when accessed.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Understand and implement the foundational concepts of server creation using Node.js and the `http` module.
- Effectively configure static routes that correctly map to specific URL paths, demonstrating an understanding of routing principles in Node.js.
- Develop an understanding of how to handle and send responses to clients through different endpoints.

---

**Direction**

- **Setup:**
    - Create a new Node.js application.
    - Use the built-in `http` module to create a server that listens for incoming requests.


**MVP requirements: Routing Implementation**

Implement the following static routes in your Node.js application:
1. **Home Route:**
    - When the user visits `/`, return the string **"Welcome to our website!"** as the response.
2. **Services Route:**
    - When the user visits `/services`, return the string **"Our Services"** as the response.
3. **Pricing Route:**
    - When the user visits `/pricing`, return the string **"Our Pricing"** as the response.
4. **Contact Route:**
    - When the user visits `/contact`, return the string **"Contact Us"** as the response.
5. **About Route:**
    - When the user visits `/about`, return the string **"About Us"** as the response.

Submission:
- Ensure that your server is properly set up and all routes return the correct strings.

**Expected Outputs**

- Accessing `http://localhost:3000/` should display **"Welcome to our website!"**.
- Accessing `http://localhost:3000/services` should display **"Our Services"**.
- Accessing `http://localhost:3000/pricing` should display **"Our Pricing"**.
- Accessing `http://localhost:3000/contact` should display **"Contact Us"**.
- Accessing `http://localhost:3000/about` should display **"About Us"**.

**Stretch Requirements**

- Consider implementing additional routes or functionalities to further enhance your Node.js application. For example, you could add a route that returns the current server time.