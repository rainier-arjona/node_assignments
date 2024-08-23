### Assignment: Job Application

Create a job application form using Express.js and EJS that allows users to submit their job application details. The application should utilize sessions to store form data and display it on a separate resume page.

![/10%20-%20Assets/JobApplication.png](/10%20-%20Assets/JobApplication.png)

**Estimated Time to Completion:** 120 minutes

**Level of Complexity:** Medium

**Instructions:**

1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL with the completed code by the due date.

**Evaluation Criteria & Learning Objectives:**

- **Establish an Express.js application with TypeScript:** Learn to set up and configure a TypeScript-based Express project.
- **Configure session management in Express:** Implement session management to handle user data.
- **Create GET and POST routes:** Develop routes to display and submit the job application form.
- **Use EJS templating to render dynamic HTML:** Create dynamic HTML pages using EJS templates.
- **Handle form submissions and session data:** Manage form data submission and session storage effectively.

**Directions**

1. **Implement the Job Application Form:**
    - **Create a Route for the Job Application Form:**
        - Define a GET route at `/` to render the job application form using the `index.ejs` template.
    - **Handle Form Submission:**
        - Define a POST route at `/submit` to handle form submissions.
        - Store the submitted form data in the session using `req.session`.
        - Redirect users to a new route to display the submitted data.
    - **Display Submitted Data:**
        - Define a GET route at `/resume` to render the resume page using the `resume.ejs` template.
        - Retrieve the form data from the session and pass it to the `resume.ejs` template for display.

**Expected Output:**

- The job application form should be accessible at `http://localhost:3000`.
- Submitting the form should redirect to a page displaying the submitted data (`/resume`).

**Additional Notes:**

- Ensure that all form fields are validated and handled correctly.
- Feel free to add styling to enhance the user experience.
- Explore additional features or improvements if time permits, such as form validation or handling optional fields.

