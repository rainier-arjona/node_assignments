# Assignment: Fixing Errors in a Node.js Online Bookstore

In this assignment, you'll analyze a provided Node.js code snippet that simulates a basic online bookstore. However, there are errors in the code causing unexpected behavior. Your task is to identify and correct these errors to ensure the bookstore functions correctly.

---

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. **Analyze the code:** Carefully examine the code, paying attention to the following:
    - HTTP status codes
    - Content-Type headers
    - Routing logic (URL matching)
    - Response bodies
2. **Identify the error:** Determine the specific part of the code that is causing the incorrect behavior.
3. **Correct the error:** Modify the code to fix the issue and ensure the bookstore operates as expected.
4. **Test the code:** Run the corrected code and verify that the bookstore functions correctly.

**Evaluation Criteria & Learning Objectives**

- Analyze and debug Node.js code
- Correct HTTP status codes and headers
- Implement proper routing logic
- Ensure accurate response bodies

---

**Directions**
Fix the provided Node.js code to ensure the online bookstore functions as expected. The code contains errors related to HTTP status codes, Content-Type headers, and routing logic. Correct these errors and test the code to verify the fixes.

**Code with Errors**

```jsx
const http = require('http');

const server = http.createServer((req, res) => {
    if (req.url === '/') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html');
        res.end('Welcome to our Bookstore!');
    } else if (req.url === '/books') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain');
        res.end('List of Books');
    } else if (req.url === '/authors') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain');
        res.end('List of Authors');
    } else if (req.url === '/genres') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain');
        res.end('List of Genres');
    } else if (req.url === '/cart') {
        res.statusCode = 404;
        res.setHeader('Content-Type', 'text/plain');
        res.end('Your Shopping Cart');
    } else {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain');
        res.end('Page not found');
    }
});

const port = 3000;
server.listen(port, () => {
    console.log(`Server running at http://localhost:${port}/`);
});

```

**Hints**

- Focus on the logic related to the shopping cart.
- Consider the appropriate HTTP status code for a successful request.

---

**Expected Output**

- The server should listen on port 3000.
- Accessing `http://localhost:3000/` should display "Welcome to our Bookstore!".
- Accessing `http://localhost:3000/books` should display "List of Books".
- Accessing `http://localhost:3000/authors` should display "List of Authors".
- Accessing `http://localhost:3000/genres` should display "List of Genres".
- Accessing `http://localhost:3000/cart` should display "Your Shopping Cart" with a 200 status code.
- Accessing any other route should display "Page not found" with a 404 status code.

---

# Solution

```jsx
const http = require('http');

/**
 * Create a server that handles different routes.
 * @param {Object} req - The request object.
 * @param {Object} res - The response object.
 */
const server = http.createServer((req, res) => {
    /**
     * Home route.
     * @route GET /
     */
    if (req.url === '/') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/html');
        res.end('Welcome to our Bookstore!');
    
    /**
     * Books route.
     * @route GET /books
     */
    } else if (req.url === '/books') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain');
        res.end('List of Books');
    
    /**
     * Authors route.
     * @route GET /authors
     */
    } else if (req.url === '/authors') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain');
        res.end('List of Authors');
    
    /**
     * Genres route.
     * @route GET /genres
     */
    } else if (req.url === '/genres') {
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain');
        res.end('List of Genres');
    
    /**
     * Cart route.
     * @route GET /cart
     */
    } else if (req.url === '/cart') {
        // Fixed part: Changed statusCode from 404 to 200
        res.statusCode = 200;
        res.setHeader('Content-Type', 'text/plain');
        res.end('Your Shopping Cart');
    
    /**
     * Catch-all route for undefined paths.
     * @route GET *
     */
    } else {
        // Fixed part: Changed statusCode from 200 to 404
        res.statusCode = 404;
        res.setHeader('Content-Type', 'text/plain');
        res.end('Page not found');
    }
});

// Set the port for the server to listen on
const port = 3000;
server.listen(port, () => {
    console.log(`Server running at http://localhost:${port}/`);
});

```

**Summary of Fixes:**

1. Changed the status code for the `/cart` route from 404 to 200 to indicate a successful request.
2. Changed the status code for the catch-all route from 200 to 404 to correctly indicate that the page was not found.