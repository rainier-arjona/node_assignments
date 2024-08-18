# Debugging Assignment: JWT Authentication Issues

In this debugging assignment, you will identify and fix issues related to JWT implementation in an Express.js application. This assignment will focus on debugging problems with token creation, expiration, and route protection.

**Estimated Time to Completion:** 1.5 hours  
**Level of Complexity:** High

## Instructions

### 1. Review the Application Code

#### Application Overview
You have been provided with a sample Express.js application that uses JWT for authentication. The application includes endpoints for registration, login, protected routes, and token refresh.

#### Files to Review
- `src/server.ts` (Express setup and route handlers)
- `src/middleware/authMiddleware.ts` (JWT verification middleware)
- `src/routes/userRoutes.ts` (Routes for registration, login, and protected access)
- `src/routes/tokenRoutes.ts` (Routes for token refresh)

### 2. Identify and Fix Issues

#### Issue 1: JWT Creation
- **Problem:** The JWT is not being created correctly during login.
- **Debugging Task:** Check the login route and `authMiddleware.ts` for issues with JWT generation. Verify that the token is signed with the correct secret and has the proper expiration time.

#### Issue 2: Token Expiration
- **Problem:** Tokens are not expiring as expected, or expiration time is not being enforced.
- **Debugging Task:** Examine the token expiration settings and ensure that the `jsonwebtoken` package is configured properly to handle token expiration.

#### Issue 3: Protected Routes
- **Problem:** Protected routes are accessible without a valid JWT or the middleware is not functioning correctly.
- **Debugging Task:** Review the `authMiddleware.ts` to ensure that JWT verification is implemented correctly. Test the `/welcome` route to ensure it properly checks for valid tokens.

#### Issue 4: Token Refresh
- **Problem:** The token refresh endpoint does not issue a new token or handles the refresh process incorrectly.
- **Debugging Task:** Check the `tokenRoutes.ts` for issues with token refreshing logic. Ensure that a new JWT is issued properly when an existing token is refreshed.

### 3. Verify Your Fixes

#### JWT Creation
- Ensure that logging in creates a valid JWT and that the token contains the correct claims and expiration.

#### Token Expiration
- Test that tokens expire correctly and that users need to refresh tokens after the expiration time.

#### Protected Routes
- Confirm that protected routes are only accessible with a valid JWT. Unauthorized access should be denied.

#### Token Refresh
- Verify that the token refresh endpoint issues a new JWT and that the old token is invalidated or handled properly.

### 4. Submit Your Work

#### Provide a Link to Your Repository
- Share your code repository with the completed fixes.

#### Include Documentation
- Add any relevant documentation or explanations of the issues and how you resolved them.

## Evaluation Criteria & Learning Objectives

- **JWT Creation:** Fix issues related to the correct generation of JWTs during login.
- **Token Expiration:** Ensure proper handling of token expiration and enforcement.
- **Protected Routes:** Verify that protected routes are secured and only accessible with valid tokens.
- **Token Refresh:** Correctly implement and verify the token refresh mechanism.

## Expected Outputs

- **Fixed JWT Creation:** Correctly created JWTs with appropriate claims and expiration.
- **Proper Expiration Handling:** Tokens expire as expected, and users must refresh tokens.
- **Secured Protected Routes:** Routes are properly protected and only accessible with valid tokens.
- **Functional Token Refresh:** Token refresh endpoint correctly issues new tokens.

## Stretch Requirements

- Implement additional security features or improvements in token handling.
- Explore advanced JWT features or integrate with other authentication mechanisms.
