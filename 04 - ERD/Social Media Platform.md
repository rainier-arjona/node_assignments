### Assignment: Social Media Platform

The goal of this assignment is to design a comprehensive Entity-Relationship Diagram (ERD) for a social media platform. The ERD will help visualize and understand the data model, entities, and relationships within the platform.

Use this wireframe as a reference to ensure that your ERD aligns with the user flows and functionalities depicted.

![Social Media Platform](/04%20-%20ERD/SocialNetworking.png)


**Estimated Time to Completion:** 120 mins

**Level of Complexity:** Medium

**Entities**
1. Users: *UserID, Username, Email, Password, DateJoined*
2. Posts: *PostID, UserID, Content, PostDate*
3. Comments: *CommentID, PostID, UserID, CommentText, CommentDate*
4. Likes: *LikeID, PostID, UserID, LikeDate*


**Learning Objectives**
- Understand how to identify and define entities and their attributes in a social media context.
- Learn to establish relationships between users, posts, comments, and likes.
- Practice setting up complex many-to-many relationships and ensuring data consistency.
- Gain experience in creating ERDs that model interactive and user-driven platforms.

---

**Relationships**
- A user can create multiple posts.
- A post can have multiple comments from different users.
- A user can like multiple posts, and a post can be liked by multiple users

**Tasks**
1. Design the ERD for the Social Media Platform.
2. Identify primary keys, foreign keys, and relationships between the entities.
3. Ensure the relationships reflect the given rules and constraints.