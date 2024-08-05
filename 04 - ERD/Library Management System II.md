### Assignment: Library Management System

The goal of this assignment is to design a comprehensive database for a Library Management System. This system needs to store information about books, authors, the relationships between them, and the borrowing of books by library members. We will achieve this by designing an Entity-Relationship Diagram (ERD), identifying primary keys, foreign keys, and detailing the relationships among the entities.

![Library Management System](/erd/Library%20Management%20System.png)

**Estimated Time to Completion:** 90 mins

**Level of Complexity:** Medium

**Entities**
1. Books: *BookID, Title, Author, Genre, Published Date, ISBN* 
2. Members: *MemberID, FirstName, LastName, Address, Phone, Email*
2. Authors: *AuthorID, Name, Bio*
3. Borrows: *BorrowID, BookID, MemberID, BorrowDate, DueDate, ReturnDate*


**Learning Objectives**
- Understand how to identify and define entities and their attributes in a library context.
- Learn to establish relationships between entities, including one-to-many and many-to-many relationships.
- Practice setting up primary and foreign keys to ensure data integrity.

---

**Relationships**
- A book can have multiple authors.
- An author can write multiple books.
- A member can borrow multiple books. 
- A book can be borrowed by multiple members (not at the same time).

**Tasks**
1. Design the ERD for the Library Management System.
2. Identify primary keys, foreign keys, and relationships between the entities.
3. Ensure the relationships reflect the rules given above.