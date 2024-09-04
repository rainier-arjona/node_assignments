### Assignment: Fixing Errors in a Node.js Online Bookstore

In this assignment, you'll analyze a provided Node.js code snippet that simulates a basic online bookstore. However, there are errors in the code causing unexpected behavior. Your task is to identify and correct these errors to ensure the bookstore functions correctly.

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Understand and identify issues in Node.js code related to HTTP status codes, headers, and routing logic.
- Apply correct HTTP status codes and headers to match the intended responses.
- Implement correct routing to ensure the proper handling of different URLs.
- Verify that the code fixes have resolved the issues and that the application behaves as expected.

---

**Directions**

Fix the provided Node.js code to ensure the online bookstore functions as expected. The code contains errors related to HTTP status codes, Content-Type headers, and routing logic. Correct these errors and test the code to verify the fixes.

**MVP Requirements: Code Analysis and Error Correction**
1. **Analyze the code:** Carefully examine the code, paying attention to:
    - HTTP status codes
    - Content-Type headers
    - Routing logic (URL matching)
    - Response bodies
2. **Identify the errors:** Determine the specific parts of the code that are causing incorrect behavior.
3. **Correct the errors:** Modify the code to fix the issues and ensure the bookstore operates as expected.
4. **Test the code:** Run the corrected code and verify that the bookstore functions correctly.

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
        res.statusCode = 404;
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

- Review the HTTP status codes and routing logic for each route to ensure they match the expected behavior.

**Expected Output**

- The server should listen on port 3000.
- Accessing `http://localhost:3000/` should display "Welcome to our Bookstore!".
- Accessing `http://localhost:3000/books` should display "List of Books".
- Accessing `http://localhost:3000/authors` should display "List of Authors".
- Accessing `http://localhost:3000/genres` should display "List of Genres".
- Accessing `http://localhost:3000/cart` should display "Your Shopping Cart" with a 200 status code.
- Accessing any other route should display "Page not found" with a 404 status code.
