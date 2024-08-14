### CCTV

In this assignment, you'll build a basic Node.js web server to simulate a CCTV system with multiple camera feeds. You will implement basic routing to serve different HTML pages for each camera feed and serve static files to enhance the user interface.

---

![../10%20-%20Assets/CCTV.png](../10%20-%20Assets/cctv.png)

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

**Stretch Requirements: Additional Content**

- Instead of image files, update each camera feed page to include additional static content or text.
- Ensure that each camera feed page displays relevant content as described in the updated HTML files.

**Additional Notes:**

- Focus on understanding the core concepts of Node.js routing and file serving.
