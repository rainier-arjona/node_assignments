# CCTV

In this assignment, you'll build a basic Node.js web server to simulate a CCTV system with multiple camera feeds. You will implement basic routing to serve different HTML pages for each camera and serve static files to enhance the user interface.

---

![CCTV](../10%20-%20Assets/CCTV.png)

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Easy

**Instructions:**

1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your code for evaluation.

**Evaluation Criteria & Learning Objectives:**

- Create a Node.js server
- Implement basic routing
- Serve static files

**Directions:**
Build a Node.js web server that simulates a CCTV system with multiple camera feeds.

**MVP Requirements: Basic Routing**

- Create a Node.js server using the `http` and `fs` modules.
- Implement routing logic to serve different HTML pages for each camera feed (`/cam1`, `/cam2`, ..., `/cam5`).
- Serve the main page (`/`) and a CSS file (`/public/styles.css`).

**Expected Output:**
The server should listen on port 3000. When you access `http://localhost:3000`, you should see the main page with links to the camera feeds. Clicking on a camera link should display the corresponding camera feed page.

**Stretch Requirements: Image Serving**

- Serve image files from the `images` directory using the `fs` module.
- Display an image on each camera feed page.

**Additional Notes:**

- Focus on understanding the core concepts of Node.js routing and file serving.

```jsx
const http = require('http');
const fs = require('fs');
const path = require('path');

const server = http.createServer((req, res) => {
    let filePath = path.join(__dirname, 'public', req.url === '/' ? 'index.html' : req.url);
    let extname = path.extname(filePath);
    let contentType = 'text/html';

    switch (extname) {
        case '.css':
            contentType = 'text/css';
            break;
        case '.js':
            contentType = 'text/javascript';
            break;
        case '.jpg':
        case '.jpeg':
        case '.png':
            contentType = 'image/' + extname.substring(1);
            break;
    }

    fs.readFile(filePath, (err, content) => {
        if (err) {
            if (err.code === 'ENOENT') {
                fs.readFile(path.join(__dirname, 'public', '404.html'), (err, content) => {
                    res.writeHead(404, { 'Content-Type': 'text/html' });
                    res.end(content, 'utf8');
                });
            } else {
                res.writeHead(500);
                res.end(`Server Error: ${err.code}`);
            }
        } else {
            res.writeHead(200, { 'Content-Type': contentType });
            res.end(content, 'utf8');
        }
    });
});

const PORT = process.env.PORT || 3000;
server.listen(PORT, () => console.log(`Server running on port ${PORT}`));
```

Create a `public` folder in your project directory and add the following files:

- `index.html` for the main page.
- `styles.css` for the CSS.
- Separate HTML files for each camera feed (`cam1.html`, `cam2.html`, ..., `cam5.html`).

For the stretch requirements, add image files to an `images` directory and update the camera feed HTML files to display these images.