```lua
  +---------+       +---------+       +---------+
  |  User   |  1    |  Post   |  1    | Comment |
  |---------|-------|---------|-------|---------|
  | UserID  |<----->| PostID  |<----->| CommentID|
  | Username|       | UserID  |       | PostID  |
  | Email   |       | Content |       | UserID  |
  | ...     |       | ...     |       | Content |
  +---------+       +---------+       +---------+

      +---------+
      |  Like   |
      |---------|
      | LikeID  |
      | PostID  |
      | UserID  |
      +---------+

      User <---- M ----> Like M <---- 1 ----> Post
```

**Relationship**
*User to Post:*
- One-to-Many: A user can create multiple posts. 
*Post to Comment:*
- One-to-Many: A post can have multiple comments. 
*User to Post (through Like):*
- Many-to-Many: A user can like multiple posts, and a post can be liked by multiple users. 