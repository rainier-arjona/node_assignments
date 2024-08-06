# Milestone Assignment: User Authentication with JWT

## Objective
In this assignment, you will create a user authentication system using Express.js and JWT. The application will allow users to register, log in, and access a protected route (/welcome) only if they are authenticated. You will also implement JWT expiration and refresh tokens.

![wireframe](../10%20-%20Assets/Login%20Registration.png)

**Estimated Time to Completion:** 2 hours  
**Level of Complexity:** High

## Instructions

### 1. Set Up the Express Application
*Note: Basic setup for Express.js and TypeScript is assumed.*

### 2. Install Dependencies
Install Required Packages:
```sh
npm install jsonwebtoken bcryptjs express
```
## 3. Implement JWT Middleware

### Create JWT Middleware
Implement middleware to verify and decode JWT tokens, managing access control.

## 4. Define Models

### User Model
Define a model with attributes such as id, username, and password (hashed).

## 5. Create Routes

### Registration Route (/register)
Create a route to register a new user. Hash the password before storing it in the database.

### Login Route (/login)
Create a route for users to log in. Generate a JWT upon successful authentication and send it to the client.

### Protected Route (/welcome)
Create a protected route that requires authentication. Redirect unauthorized users to the login page or return a 401 Unauthorized response.

### Refresh Token Route (/refresh)
Implement a route to refresh tokens. Generate a new JWT when the existing token is expired or about to expire.

## 6. Implement JWT Logic

### Generate JWT
When a user logs in, create a JWT with an expiration time and send it to the client.

### Verify JWT
Implement middleware to verify the JWT on protected routes.

### Handle Expiration and Refresh
Understand and implement token expiration and refresh to maintain user sessions.

## 7. Create EJS Templates

### Registration Template (register.ejs)
Design a form to allow users to register.

### Login Template (login.ejs)
Design a form for users to log in.

### Welcome Template (welcome.ejs)
Display a welcome message for authenticated users.

## 8. Test Your Application

### Registration and Login
Ensure that users can register and log in, and that JWTs are correctly issued.

### Protected Route
Test that the /welcome route is accessible only with a valid JWT.

### Token Refresh
Verify that tokens can be refreshed correctly.

## 9. Submit Your Work

### Provide a Link to Your Repository
Share your code repository with the completed assignment.

### Include Documentation
Add any relevant documentation or screenshots to demonstrate your implementation.

## Evaluation Criteria & Learning Objectives

- **User Authentication**: Implement user registration and login with JWT.
- **JWT Management**: Correctly handle JWT issuance, verification, and refresh.
- **Protected Routes**: Ensure that protected routes are accessible only to authenticated users.
- **Password Security**: Hash passwords before storing them in the database.
- **Token Expiration and Refresh**: Implement expiration and refresh mechanisms for JWTs.

## Expected Outputs

- **Registration and Login**: Functional routes for user registration and login.
- **JWT Handling**: Proper JWT issuance, verification, and refresh.
- **Protected Access**: Secure access to the /welcome route based on authentication.
- **Templates**: EJS templates for registration, login, and welcome pages.

## Stretch Requirements

- Implement additional features like password reset or email verification.
- Enhance security measures or improve the user experience.
