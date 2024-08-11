```lua
+---------+      1   +---------+
|  User   |---------| Profile |
+---------+      1   +---------+
| UserID  |<------->| UserID  |
| Username|         | ProfileID|
| Email   |         | FirstName|
| PasswordHash |     | LastName |
| CreatedAt |       | DateOfBirth|
| UpdatedAt |       | Bio      |
+---------+         | ProfilePictureURL |
                   | CreatedAt |
                   | UpdatedAt |
                   +---------+

```

```sql

CREATE TABLE Users (
    UserID INT AUTO_INCREMENT PRIMARY KEY,
    Username VARCHAR(50) NOT NULL UNIQUE,
    Email VARCHAR(100) NOT NULL UNIQUE,
    Password VARCHAR(255) NOT NULL,
    CreatedAt TIMESTAMP DEFAULT 
    UpdatedAt TIMESTAMP DEFAULT 
);


CREATE TABLE Profiles (
    ProfileID INT AUTO_INCREMENT PRIMARY KEY,
    UserID INT UNIQUE, -- Ensures each user has exactly one profile
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
);

```