### Milestone Assignment: User Authentication with JWT

In this assignment, you will create a user authentication system using Express.js and JWT. The application will allow users to register, log in, and access a protected route (/welcome) only if they are authenticated. You will also implement JWT expiration and refresh tokens.

![../10%20-%20Assets/Login%20Registration.png](../10%20-%20Assets/Login%20Registration.png)

**Estimated Time to Completion:** 2 hours

**Level of Complexity:** High

**Instructions**

1. **Set Up the Express Application**
    
    *Note: Basic setup for Express.js and TypeScript is assumed.*
    
2. **Install Dependencies**
    - Install the required packages:
        
        ```
        npm install jsonwebtoken bcryptjs express
        
        ```
        
3. **Implement JWT Middleware**
    - **Create JWT Middleware**
    Implement middleware to verify and decode JWT tokens, managing access control.
4. **Define Models**
    - **User Model**
    Define a model with attributes such as id, username, and password (hashed).
5. **Create Routes**
    - **Registration Route (/register)**
        
        Create a route to register a new user.
        
        - Hash the password before storing it in the database.
    - **Login Route (/login)**
        
        Create a route for users to log in.
        
        - Generate a JWT upon successful authentication.
        - Send the JWT to the client.
    - **Protected Route (/welcome)**
        
        Create a protected route that requires authentication.
        
        - Redirect unauthorized users to the login page or return a 401 Unauthorized response.
    - **Refresh Token Route (/refresh)**
        
        Implement a route to refresh tokens.
        
        - Generate a new JWT when the existing token is expired or about to expire.
6. **Implement JWT Logic**
    - **Generate JWT**
        
        When a user logs in:
        
        - Create a JWT with an expiration time.
        - Send it to the client.
    - **Verify JWT**
        
        Implement middleware to verify the JWT on protected routes.
        
    - **Handle Expiration and Refresh**
        - Understand and implement token expiration.
        - Implement token refresh to maintain user sessions.
7. **Create EJS Templates**
    - **Registration Template (register.ejs)**
        
        Design a form to allow users to register.
        
    - **Login Template (login.ejs)**
        
        Design a form for users to log in.
        
    - **Welcome Template (welcome.ejs)**
        
        Display a welcome message for authenticated users.
        
8. **Test Your Application**
    - **Registration and Login**
        
        Ensure that:
        
        - Users can register and log in.
        - JWTs are correctly issued.
    - **Protected Route**
        
        Test that:
        
        - The /welcome route is accessible only with a valid JWT.
    - **Token Refresh**
        
        Verify that:
        
        - Tokens can be refreshed correctly.
9. **Submit Your Work**
    - **Submit your GitHub URL with the completed code by the due date.**

**Evaluation Criteria & Learning Objectives**

- **User Authentication:** Proper implementation of user registration and login processes using JWT.
- **JWT Handling:** Correct generation, verification, and refresh of JWTs.
- **Route Protection:** Secure access to protected routes, ensuring only authenticated users can access them.
- **Password Security:** Proper hashing of passwords before storing them in the database.
- **Token Expiration and Refresh:** Effective management of JWT expiration and refreshing to maintain user sessions.

**Expected Outputs**

- **Registration and Login:** Functional routes for user registration and login.
- **JWT Handling:** Proper JWT issuance, verification, and refresh.
- **Protected Access:** Secure access to the /welcome route based on authentication.
- **Templates:** EJS templates for registration, login, and welcome pages.

**Stretch Requirements**

- **Implement additional features like password reset or email verification.**
- **Enhance security measures or improve the user experience.**