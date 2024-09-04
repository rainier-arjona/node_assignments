### Assignment: Job Application

Create a job application form using Express.js and EJS that allows users to submit their job application details. The application should utilize sessions to store form data and display it on a separate resume page.

![/10%20-%20Assets/JobApplication.png](/10%20-%20Assets/JobApplication.png)

**Estimated Time to Completion:** 120 minutes

**Level of Complexity:** Medium

**Instructions:**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives:**

- Create POST routes with JSON and HTML file responses.

---

**Directions**

Set up a job application form by creating routes to display the form, handle submissions, and show the submitted data. Use sessions to store and pass the form data between routes.

**MVP Requirements: Implementing a Job Application Form with Express and EJS**

Implement the Job Application Form:
1. **Create a Route for the Job Application Form:**
        - Define a GET route at `/` to render the job application form using the `index.ejs` template.
2. **Handle Form Submission:**
        - Define a POST route at `/submit` to handle form submissions.
        - Store the submitted form data in the session using `req.session`.
        - Redirect users to a new route to display the submitted data.
3. **Display Submitted Data:**
        - Define a GET route at `/resume` to render the resume page using the `resume.ejs` template.
        - Retrieve the form data from the session and pass it to the `resume.ejs` template for display.

**Expected Output:**

- The job application form should be accessible at `http://localhost:3000`.
- Submitting the form should redirect to a page displaying the submitted data (`/resume`).

**Additional Notes:**

- Ensure that all form fields are validated and handled correctly.
- Feel free to add styling to enhance the user experience.
- Explore additional features or improvements if time permits, such as form validation or handling optional fields.

