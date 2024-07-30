# Hello World (sequelize)

Create a Node.js application using Express and Sequelize to connect to a MySQL database and display a "Hello, World!" message in the browser. Verify that the connection to the database is successfully established.

---

![Hello World](/10%20-%20Assets/HelloWorld%20(Sequelize).png)

**Estimated Time to Completion:** 60 minutes

**Level of Complexity:** Beginner

**Instructions:**

1. **Setup Your Project:**
    - Create a new directory for your project and initialize a Node.js project.
    - Install the required dependencies: Express, Sequelize, MySQL2, and TypeScript-related packages.
2. **Configure Sequelize:**
    - Create a configuration file to set up Sequelize to connect to your MySQL database. This file should include the necessary database credentials and configuration details.
3. **Implement the Application:**
    - Create an Express server that initializes Sequelize with your MySQL configuration.
    - Test the database connection by authenticating Sequelize and logging a success or error message.
    - Set up a route that returns a "Hello, World!" message when accessed.
4. **Verify Your Application:**
    - Run your server and navigate to `http://localhost:3000/` in your browser to confirm that the "Hello, World!" message is displayed.
    
    ![Untitled](Hello%20World%20(sequelize)%20136137f799da40f38514fe40e00871f1/Untitled%201.png)
    
    - Ensure that your application logs a message indicating whether the connection to the database was successful or failed.
    

**Tasks:**

1. **Create the Project Directory and Initialize:**
    - Create the necessary directories and files for your project structure.
    - Initialize TypeScript and set up configuration files.
2. **Configure Sequelize:**
    - Set up the `config/config.json` file with MySQL database connection details.
    - Write the Sequelize initialization code to connect to your database.
3. **Develop the Server:**
    - Create an `index.ts` or `server.ts` file to set up the Express server.
    - Integrate Sequelize and test the connection.
    - Implement a route that returns a "Hello, World!" message.
4. **Run and Test:**
    - Build and start your application.
    - Check the browser for the "Hello, World!" message.
    - Review console output to confirm the database connection status.
    

**Deliverables:**

- Submit a link to your GitHub repository containing the complete project.
- Ensure your project includes all necessary files and configurations for running the application.

**Evaluation Criteria & Learning Objectives:**

- Correctly configure Sequelize to connect to a MySQL database.
- Successfully initialize and test the connection to the database.
- Set up and run an Express server with a basic route.
- Demonstrate successful connection to the database and display of the "Hello, World!" message.