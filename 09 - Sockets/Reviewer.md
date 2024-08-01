# Assignment: Team-Based Trivia Game Application

In this assignment, you'll develop a web application that allows users to participate in a team-based trivia game. The application will include user authentication, team and room management, and a trivia quiz interface. You will also implement CRUD operations and RESTful APIs for managing game data.

![Wireframe](../10%-%Assets/TriviaMeta.png)

## Estimated Time to Completion
2-3 hours

## Level of Complexity
Medium

## Instructions
1. Read through the directions below.
2. Complete the necessary elements as outlined.
3. Submit your GitHub URL by the due date.

## Evaluation Criteria & Learning Objectives
- Implement user authentication
- Manage teams, players, and rooms
- Develop and manage CRUD operations for teams, players, and rooms
- Build and test RESTful APIs for game data management

## Directions
Build a trivia game application with the following features:

### MVP Requirements

#### User Login
- Implement user authentication, allowing users to log in or register to access the game.

#### Player Manager
- **Teams & Players:** Users can create teams and add players to them, maintaining a one-to-many relationship.
- **Manage Players:** Users can update player details, such as profile information.
- **Assign Players to Teams:** Players can be assigned to specific teams.

#### Room Management
- **Rooms:** Users can create, update (e.g., change room title or category), and delete game rooms.
- **Trivia Game:** Implement a trivia quiz interface where players answer questions in categories like Animals, Foods, Movies, etc.

#### CRUD Operations & API
- **Teams:** Provide CRUD functionality to manage teams.
- **Players:** Provide CRUD functionality to manage players.
- **Rooms:** Provide CRUD functionality for room management.
- **APIs:** Develop RESTful APIs to handle operations for teams, players, and rooms. Ensure that changes in player data are reflected within their respective teams.

#### Game Interface
- **Gameplay:** Players can participate in a trivia game within a room, answer questions, and view scores.

## Expected Outputs
- **User Login:** Users can log in and see their profile and options to join or create teams and rooms.
- **Player & Team Management:** Users can view, add, edit, and delete teams and players.
- **Room & Game Management:** Users can create rooms, start games, and manage gameplay.
- **CRUD API:** APIs should return JSON responses for teams, players, and rooms.

## Stretch Requirements
- Implement a scoring system that tracks correct answers and displays team scores.
- Add real-time features using WebSockets, such as live updates of scores and player statuses.
- (Optional) Implement JWT for securing API endpoints.
