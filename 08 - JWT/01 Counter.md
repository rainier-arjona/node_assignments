# Milestone Assignment: Counter Application with JWT

## Objective
In this assignment, you will create a simple counter application using Express.js and JWT (JSON Web Tokens) to manage and persist the counter value. The application will have two buttons to increase or decrease the counter, with JWT used to handle state across requests.

![COUNTER](../10%20-%20Assets/Counter.png)

**Estimated Time to Completion:** 90 minutes  
**Level of Complexity:** Medium

## Instructions

### 1. Set Up the Express Application
*Note: Basic setup for Express.js and TypeScript is assumed.*

### 2. Create and Configure JWT Middleware

#### Install Dependencies:
- Install `jsonwebtoken` and `express`.

#### Implement JWT Middleware:
- Create middleware to verify and decode JWT tokens, managing the counter value.

### 3. Define Routes

#### Root Route (/):
- Display the current counter value.

#### Increase Route (/increase):
- Increment the counter and update the JWT token.

#### Decrease Route (/decrease):
- Decrement the counter and update the JWT token.

### 4. Create EJS Template

#### Main Page Template (index.ejs):
- Design an EJS template to display the current counter value and provide buttons for increasing and decreasing the counter.

### 5. Implement JWT Logic

#### Initialize JWT:
- When a counter action is performed, generate a new JWT with the updated counter value and send it to the client.

#### Verify JWT:
- Ensure that JWT is correctly verified on each request to manage counter state.

## Evaluation Criteria & Learning Objectives
- **JWT Implementation:** Correctly use JWT to handle counter state.
- **Routing:** Functional routes to increment and decrement the counter.
- **EJS Rendering:** Dynamic display of counter value using EJS.
- **Data Persistence:** Proper management of state across requests using JWT.

## Directions

### Set Up JWT Middleware:
- Implement JWT verification and decoding middleware.

### Create Routes:
- Implement the routes to handle counter actions and manage JWT.

### Design the EJS Template:
- Create a template to render the counter value and provide buttons for counter actions.

### Test Your Application:
- Ensure that counter updates correctly and persists across requests using JWT.

### Submit Your Work:
- Provide a link to your code repository.
- Include any relevant documentation or screenshots to demonstrate your implementation.

## Expected Outputs
- **Functional Application:** The application should correctly display the counter value and update it based on user actions.
- **JWT Management:** JWT should correctly manage and persist the counter state.
- **EJS Template:** The counter value should be dynamically rendered on the main page.

## Stretch Requirements
- Implement additional validation or error handling.
- Add extra features or functionality if desired.
