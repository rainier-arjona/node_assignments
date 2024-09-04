### Assignment: Debugging a One-to-Many Movie Application

In this assignment, you'll be provided with a simple Express and TypeScript application designed to manage movies and their reviews. The application has several intentional errors that you need to debug and fix. This includes issues with routes, types, and CRUD operations for a one-to-many relationship.

**Estimated Time to Completion:** 90 mins

**Level of Complexity:** Medium

**Instructions**

1. Read through the directions below. Note: you will be provided any necessary files on which to work.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

**Evaluation Criteria & Learning Objectives**

- Ensure that all routes are properly defined and correctly mapped, enabling CRUD operations for movies and reviews.
- Resolve all TypeScript type issues to ensure the application is type-safe.
- Confirm that Sequelize models are correctly set up with a one-to-many relationship between movies and reviews.
- Verify that all CRUD operations for movies and reviews are functioning as intended.
- Ensure that the application behaves correctly and that all routes and CRUD operations work as expected when tested.

---

**Directions**

1. **Download the Provided Code:** You will be given a zip file containing a simple Express and TypeScript application with intentional issues related to movies and reviews.
    
    **Download here:** [Movies & Reviews](https://drive.google.com/file/d/1R5eiX6arWu0peoH63JEVRO6Cr9YeclBN/view?usp=sharing)
    
2. **Debug the Application:**
    - **Routes:** Check and correct any routing issues. Ensure routes are properly handling CRUD operations for movies and reviews.
    - **Types:** Look for TypeScript errors and resolve them to ensure type safety.
    - **Models:** Verify that Sequelize models for movies and reviews are correctly set up with a one-to-many relationship. A movie should have many reviews.
    - **CRUD Operations:** Test and fix CRUD operations for both movies and reviews to ensure they work correctly. This includes creating, reading, updating, and deleting.
3. **Test and Verify:** Run the application, test each endpoint, and ensure that all CRUD operations and relationships function as intended.

**MVP Requirements: Debug and Validate CRUD Operations**

- Identify and Fix Errors:
    - **Routes:** Correct any incorrectly defined or implemented routes.
    - **Types:** Fix TypeScript type errors.
    - **Models:** Ensure the Sequelize models are correctly defined with proper one-to-many relationships (Movies and Reviews).
    - **CRUD Operations:** Make sure that Create, Read, Update, and Delete operations for movies and reviews are functioning correctly.
- Test: Run the application and test each route to ensure all CRUD operations work as expected.

**Expected Outputs**

- **Corrected Code:** The code should have all identified issues fixed, with proper routes, types, models, and CRUD operations.
- **Functional Routes:** All routes should work as expected for creating, reading, updating, and deleting movies and reviews.
- **TypeScript Errors Resolved:** All TypeScript errors should be fixed.
- **Model Definitions:** Sequelize models should correctly implement the one-to-many relationship between movies and reviews.
- **Application Tested:** The application should be fully tested, with all CRUD operations and relationships functioning correctly.