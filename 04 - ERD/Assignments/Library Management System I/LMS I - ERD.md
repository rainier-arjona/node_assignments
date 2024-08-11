**ERD Diagram**
```lua
+----------------+    +----------------+     +----------------+
|    Authors     |    |     Books      |     | Members        |
+----------------+    +----------------+     +----------------+
| AuthorID (PK)  |1  | BookID (PK)     |N  | MemberID (PK)    |
| FirstName      |---| Title           |   | FirstName        |
| LastName       |   | ISBN            |   | LastName         |
| Biography      |   | YearPublished   |   | DateOfBirth      |
+----------------+   | AuthorID (FK)   |   | MembershipDate   |
                     | Publisher       |   +----------------+
                     +----------------+

