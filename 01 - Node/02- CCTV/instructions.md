### Assignment: CCTV

In this assignment, you'll build a basic Node.js web server to simulate a CCTV system with multiple camera feeds. You will implement basic routing to serve different HTML pages for each camera feed.

---

![../10%20-%20Assets/CCTV.png](../10%20-%20Assets/cctv.png)

**Estimated Time to Completion:** 60 mins

**Level of Complexity:** Easy

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Create a Node server, with multiple GET routes, returning raw json or an html file

---

**Directions:**

Build a Node.js web server that simulates a CCTV system with multiple camera feeds.

1. **Setup:**
    - Create a new Node.js application.
    - Use the `http` and `fs` modules to create a server that listens for incoming requests and serves HTML pages.
2. **Submission:**
    - Ensure that your server is properly set up and all routes return the correct HTML content.
    - **Bonus:** Include a simple CSS file to style the pages.

**MVP Requirements: Basic Routing**

- Create a Node.js server using the `http` and `fs` modules.
- Implement routing logic to serve different HTML pages for each camera feed (`/cam1`, `/cam2`, ..., `/cam5`).
- Serve the main page (`/`).

**Expected Output**

- The server should listen on port 3000.
- Accessing `http://localhost:3000` should display the main page with links to the camera feeds.
- Clicking on a camera link (e.g., `http://localhost:3000/cam1`) should display the corresponding camera feed page.

**Stretch Requirements**

- Enhance each camera feed page by including additional static content or text instead of image files.
- Ensure that each camera feed page is distinct and displays relevant content as described in the updated HTML files.

**Additional Notes**

- Focus on understanding the core concepts of Node.js routing and file serving to successfully simulate the CCTV system.