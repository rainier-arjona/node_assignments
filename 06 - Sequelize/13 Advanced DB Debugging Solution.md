Project Setup
1. Initialize Project

```js
mkdir movie-app
cd movie-app
npm init -y

npm install express sequelize sequelize-typescript typescript ts-node @types/node @types/express ejs
npm install sequelize mysql2
```

2. Create Directory Structure
```
movie-app
├── src
│   ├── config
│   │   └── database.ts
│   ├── models
│   │   ├── movie.ts
│   │   └── review.ts
│   ├── routes
│   │   ├── movieRoutes.ts
│   │   └── reviewRoutes.ts
│   ├── views
│   │   ├── index.ejs
│   │   ├── movieForm.ejs
│   │   ├── reviewForm.ejs
│   └── app.ts
├── package.json
└── tsconfig.json
```

1. Setup Sequelize Configuration
Create src/config/database.ts:

```ts
import { Sequelize } from 'sequelize-typescript';

const sequelize = new Sequelize({
  dialect: 'mysql',
  host: 'localhost',
  username: 'root', // Adjust as necessary
  password: '',     // Adjust as necessary
  database: 'movie_db',
  models: [__dirname + '/../models']  // Path to your models
});

export default sequelize;
```

2. Define Models
Create src/models/movie.ts:

```ts
import { Model, DataTypes } from 'sequelize';
import sequelize from '../config/database';
import Review from './review';

class Movie extends Model {
  public id!: number;
  public title!: string;
  public description!: string;
  public createdAt!: Date;
  public updatedAt!: Date;
}

Movie.init({
  title: {
    type: DataTypes.STRING,
    allowNull: false
  },
  description: {
    type: DataTypes.TEXT,
    allowNull: true
  }
}, {
  sequelize,
  tableName: 'movies'
});

Movie.hasMany(Review, { foreignKey: 'movieId' });
Review.belongsTo(Movie, { foreignKey: 'movieId' });

export default Movie;
```

Create src/models/review.ts:
```ts
import { Model, DataTypes } from 'sequelize';
import sequelize from '../config/database';
import Movie from './movie';

class Review extends Model {
  public id!: number;
  public movieId!: number;
  public content!: string;
  public createdAt!: Date;
  public updatedAt!: Date;
}

Review.init({
  movieId: {
    type: DataTypes.INTEGER,
    references: {
      model: Movie,
      key: 'id'
    },
    allowNull: false
  },
  content: {
    type: DataTypes.TEXT,
    allowNull: false
  }
}, {
  sequelize,
  tableName: 'reviews'
});

export default Review;
```

3. Setup Routes
Create src/routes/movieRoutes.ts:

```ts
import { Router } from 'express';
import Movie from '../models/movie';

const router = Router();

// Create Movie
router.post('/movies', async (req, res) => {
  try {
    const { title, description } = req.body;
    const newMovie = await Movie.create({ title, description });
    res.redirect('/');
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// Get all Movies
router.get('/', async (req, res) => {
  try {
    const movies = await Movie.findAll();
    res.render('index', { movies });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// Get Movie Form
router.get('/movies/new', (req, res) => {
  res.render('movieForm');
});

export default router;
```

Create src/routes/reviewRoutes.ts:

```ts
import { Router } from 'express';
import Review from '../models/review';
import Movie from '../models/movie';

const router = Router();

// Create Review
router.post('/reviews', async (req, res) => {
    try {
        const { movieId, content } = req.body;
        await Review.create({ movieId, content });
        res.redirect(`/movies/${movieId}`);
    } catch (error) {
        res.status(500).json({ error: (error as Error).message });
    }
});

// Get Reviews for a Movie
router.get('/movies/:id/reviews', async (req, res) => {
    try {
        const movieId = parseInt(req.params.id, 10);
        const movie = await Movie.findByPk(movieId, { include: Review });
        if (movie) {
            res.render('reviewForm', { movie });
        } else {
            res.status(404).send('Movie not found');
        }
    } catch (error) {
        res.status(500).json({ error: (error as Error).message });
    }
});

export default router;
```

4. Setup Views
Create src/views/index.ejs:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Movies</title>
</head>
<body>
    <h1>Movies List</h1>
    <ul>
        <% movies.forEach(movie => { %>
            <li>
                <%= movie.title %> - <%= movie.description %>
                <a href="/movies/<%= movie.id %>/reviews">View Reviews</a>
            </li>
        <% }) %>
    </ul>
    <a href="/movies/new">Add New Movie</a>
</body>
</html>
```

Create src/views/movieForm.ejs:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Add Movie</title>
</head>
<body>
    <h1>Add a New Movie</h1>
    <form action="/movies" method="POST">
        <label for="title">Title:</label>
        <input type="text" id="title" name="title" required><br>
        <label for="description">Description:</label>
        <textarea id="description" name="description"></textarea><br>
        <input type="submit" value="Add Movie">
    </form>
    <a href="/">Back to Movies List</a>
</body>
</html>
```

Create src/views/reviewForm.ejs:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Reviews for <%= movie.title %></title>
</head>
<body>
    <h1>Reviews for <%= movie.title %></h1>
    <ul>
        <% movie.reviews.forEach(review => { %>
            <li><%= review.content %></li>
        <% }) %>
    </ul>
    <form action="/reviews" method="POST">
        <input type="hidden" name="movieId" value="<%= movie.id %>">
        <label for="content">Review Content:</label>
        <textarea id="content" name="content" required></textarea><br>
        <input type="submit" value="Add Review">
    </form>
    <a href="/">Back to Movies List</a>
</body>
</html>
```

5. Initialize Express App
Create src/app.ts:
```ts
import { Router } from 'express';
import Movie from '../models/movie';

const router = Router();

// Create Movie
router.post('/movies', async (req, res) => {
    try {
        const { title, description } = req.body;
        const newMovie = await Movie.create({ title, description });
        res.redirect('/');
    } catch (error) {
        res.status(500).json({ error: (error as Error).message });
    }
});

// Get all Movies
router.get('/', async (req, res) => {
    try {
        const movies = await Movie.findAll();
        res.render('index', { movies });
    } catch (error) {
        res.status(500).json({ error: (error as Error).message });
    }
});

// Get Movie Form
router.get('/movies/new', (req, res) => {
    res.render('movieForm');
});

export default router;
```

6. Run the Application
Make sure you have MySQL running and create a database named movie_db. Then run the application:
npx ts-node src/app.ts
