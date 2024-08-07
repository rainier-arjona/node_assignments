### server.ts
```ts
import express from 'express';
import path from 'path';
import movieRoutes from './routes/movieRoutes';
import reviewRoutes from './routes/reviewRoutes';

const app = express();
const port = 3000;

app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Serve static files
app.use(express.static(path.join(__dirname, 'public')));

// Set view engine
app.set('view engine', 'ejs');
app.set('views', path.join(__dirname, '..', 'src', 'views'));

// Use movie routes
app.use('/', movieRoutes);
app.use('/', reviewRoutes);

app.listen(port, () => {
    console.log(`Server is running on http://localhost:${port}`);
});
```

### models/movie.ts
```ts
import { DataTypes, Model } from 'sequelize';
import sequelize from '../config/database';
import Review from './review'; // Ensure Review is imported here

export class Movie extends Model {
    public id!: number;
    public title!: string;
    public description?: string;

    public async addReviews(reviews: Review[]) {
        await this.addReviews(reviews);
    }
}

Movie.init({
    title: {
        type: DataTypes.STRING,
        allowNull: false,
    },
    description: {
        type: DataTypes.TEXT,
        allowNull: true,
    },
}, {
    sequelize,
    modelName: 'Movie',
});

// Define associations here
Movie.hasMany(Review, { foreignKey: 'movieId', as: 'reviews' });

export default Movie;

```
### models/review.ts
```ts
import { DataTypes, Model } from 'sequelize';
import sequelize from '../config/database';
import Movie from './movie'; // Ensure Movie is imported here

export class Review extends Model {
    public id!: number;
    public content!: string;
    public movieId!: number;
}

Review.init({
    content: {
        type: DataTypes.TEXT,
        allowNull: false,
    },
    movieId: {
        type: DataTypes.INTEGER,
        references: {
            model: Movie, // Ensure Movie is used here
            key: 'id',
        },
        allowNull: false,
    },
}, {
    sequelize,
    modelName: 'Review',
});

// Define associations here
Review.belongsTo(Movie, { foreignKey: 'movieId', as: 'movie' });

export default Review;

```
### models/index.ts
```ts
import sequelize from '../config/database';
import Movie from './movie';
import Review from './review';

// Define associations
Movie.hasMany(Review, { foreignKey: 'movieId', as: 'reviews' });
Review.belongsTo(Movie, { foreignKey: 'movieId', as: 'movie' });

export { Movie, Review, sequelize };

```
### routes/movieRoutes.ts
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
### routes/reviewRoutes.ts
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
### views/index.ejs
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
### views/movieForm.ejs
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
### views/reviewForm.ejs
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
