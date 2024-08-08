### server.ts
```ts
import express from 'express';
import path from 'path';
import { Book, Author } from './models';

const app = express();
const port = 3000;

app.set('view engine', 'ejs');
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));
app.set('views', path.join(__dirname, '..', 'src', 'views'));
app.use(express.urlencoded({ extended: true }));

/**
 * GET /
 * Fetches all books and authors and renders the index page.
 */
app.get('/', async (req, res) => {
    try {
        const books = await Book.findAll({ include: [Author] });
        const authors = await Author.findAll({ include: [Book] });
        res.render('index', { books, authors });
    } catch (error) {
        console.error('Error fetching books and authors:', error);
        res.status(500).send('Internal Server Error');
    }
});

/**
 * GET /books/new
 * Renders the new book form.
 */
app.get('/books/new', async (req, res) => {
    try {
        const authors = await Author.findAll();
        res.render('newBook', { authors });
    } catch (error) {
        console.error('Error fetching authors:', error);
        res.status(500).send('Internal Server Error');
    }
});

/**
 * POST /books/add
 * Adds a new book and associates it with authors.
 */
app.post('/books/add', async (req, res) => {
    try {
        const { title, authors } = req.body;
        const book = await Book.create({ title });

        if (authors && Array.isArray(authors)) {
            const authorInstances = await Author.findAll({ where: { id: authors } });
            await book.addAuthors(authorInstances);
        }

        res.redirect('/');
    } catch (error) {
        console.error('Error creating book:', error);
        res.status(500).send('Internal Server Error');
    }
});

/**
 * GET /authors/new
 * Renders the new author form.
 */
app.get('/authors/new', async (req, res) => {
    try {
        const books = await Book.findAll();
        res.render('newAuthor', { books });
    } catch (error) {
        console.error('Error fetching books:', error);
        res.status(500).send('Internal Server Error');
    }
});

/**
 * POST /authors/add
 * Adds a new author and associates them with books.
 */
app.post('/authors/add', async (req, res) => {
    try {
        const { name, bio, books } = req.body;
        const author = await Author.create({ name, bio });

        if (books && Array.isArray(books)) {
            const bookInstances = await Book.findAll({ where: { id: books } });
            await author.addBooks(bookInstances);
        }

        res.redirect('/');
    } catch (error) {
        console.error('Error creating author:', error);
        res.status(500).send('Internal Server Error');
    }
});

/**
 * GET /books/:id
 * Fetches a book by ID and renders its details.
 */
app.get('/books/:id', async (req, res) => {
    try {
        const book = await Book.findByPk(req.params.id, { include: [Author] });
        if (!book) return res.status(404).send('Book not found');
        res.render('bookDetails', { book });
    } catch (error) {
        console.error('Error fetching book details:', error);
        res.status(500).send('Internal Server Error');
    }
});

/**
 * GET /authors/:id
 * Fetches an author by ID and renders their details.
 */
app.get('/authors/:id', async (req, res) => {
    try {
        const author = await Author.findByPk(req.params.id, { include: [Book] });
        if (!author) return res.status(404).send('Author not found');
        res.render('authorDetails', { author });
    } catch (error) {
        console.error('Error fetching author details:', error);
        res.status(500).send('Internal Server Error');
    }
});

/**
 * POST /books/:id/delete
 * Deletes a book by ID.
 */
app.post('/books/:id/delete', async (req, res) => {
    try {
        const book = await Book.findByPk(req.params.id);
        if (!book) return res.status(404).send('Book not found');
        await book.destroy();
        res.redirect('/');
    } catch (error) {
        console.error('Error deleting book:', error);
        res.status(500).send('Internal Server Error');
    }
});

/**
 * POST /authors/:id/delete
 * Deletes an author by ID.
 */
app.post('/authors/:id/delete', async (req, res) => {
    try {
        const author = await Author.findByPk(req.params.id);
        if (!author) return res.status(404).send('Author not found');
        await author.destroy();
        res.redirect('/');
    } catch (error) {
        console.error('Error deleting author:', error);
        res.status(500).send('Internal Server Error');
    }
});

/**
 * Starts the server on the specified port.
 */
app.listen(port, () => {
    console.log(`Server is running on http://localhost:${port}`);
});
```
### sync.ts
```ts
import { sequelize } from './models';

const syncDatabase = async () => {
    try {
        await sequelize.sync({ force: true });
        console.log('Database synchronized successfully.');
    } catch (error) {
        console.error('Error synchronizing database:', error);
    }
};

syncDatabase();
```

### migration/20240807034029-create-book-author.js
```js
const { DataTypes } = require('sequelize');

module.exports = {
	up: async (queryInterface) => {
		await queryInterface.createTable('BookAuthor', {
			BookId: {
				type: DataTypes.INTEGER,
				references: {
					model: 'Books',
					key: 'id',
				},
				onDelete: 'CASCADE',
				onUpdate: 'CASCADE',
			},
			AuthorId: {
				type: DataTypes.INTEGER,
				references: {
					model: 'Authors',
					key: 'id',
				},
				onDelete: 'CASCADE',
				onUpdate: 'CASCADE',
			},
			createdAt: {
				allowNull: false,
				type: DataTypes.DATE,
				defaultValue: DataTypes.NOW,
			},
			updatedAt: {
				allowNull: false,
				type: DataTypes.DATE,
				defaultValue: DataTypes.NOW,
			},
		});
	},

	down: async (queryInterface) => {
		await queryInterface.dropTable('BookAuthor');
	},
};
```
### models/author.ts
```ts
import { DataTypes, Model } from 'sequelize';
import sequelize from '../config/database';
import { Book } from './book';

export class Author extends Model {
    public id!: number;
    public name!: string;
    public bio!: string;
}

Author.init({
    name: {
        type: DataTypes.STRING,
        allowNull: false,
    },
    bio: {
        type: DataTypes.TEXT,
        allowNull: true,
    },
}, {
    sequelize,
    modelName: 'Author',
});
```
### models/book.ts
```ts
import { DataTypes, Model } from 'sequelize';
import sequelize from '../config/database';
import { Author } from './author';

export class Book extends Model {
    public id!: number;
    public title!: string;
}

Book.init({
    title: {
        type: DataTypes.STRING,
        allowNull: false,
    },
}, {
    sequelize,
    modelName: 'Book',
});
```
### models/index.ts
```ts
import sequelize from '../config/database';
import { Book } from './book';
import { Author } from './author';

Book.belongsToMany(Author, { through: 'BookAuthor' });
Author.belongsToMany(Book, { through: 'BookAuthor' });

export { Book, Author, sequelize };
```

### types/sequelize.d.ts
```ts
import { Author } from '../models/author';
import { Book } from '../models/book';

declare module 'sequelize/types' {
    interface Model {
        addAuthors(authors: Author[]): Promise<void>;
        addBooks(books: Book[]): Promise<void>;
    }
}
```
### views/index.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Books & Authors</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
    <header>
        <nav>
            <a href="/">Books & Authors</a>
            <a href="/">Home</a>
            <a href="/books/new">Add Book</a>
            <a href="/authors/new">Add Author</a>
        </nav>
    </header>
    <main>
        <h1>Books & Authors</h1>
        <section>
            <h2>Books</h2>
            <ul class="book-list">
                <% books.forEach(book => { %>
                    <li>
                        <a href="/books/<%= book.id %>"><%= book.title %></a>
                        <ul class="author-list-inline">
                            <% book.Authors.forEach(author => { %>
                                <li><%= author.name %></li>
                            <% }) %>
                        </ul>
                    </li>
                <% }) %>
            </ul>
        </section>
        <section>
            <h2>Authors</h2>
            <ul class="author-list">
                <% authors.forEach(author => { %>
                    <li><a href="/authors/<%= author.id %>"><%= author.name %></a></li>
                <% }) %>
            </ul>
        </section>
    </main>
</body>
</html>

```
### views/newAuthor.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>New Author</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
    <header>
        <nav>
            <a href="/">Books & Authors</a>
            <a href="/">Home</a>
            <a href="/books/new">Add Book</a>
            <a href="/authors/new">Add Author</a>
        </nav>
    </header>
    <main>
        <h1>Create New Author</h1>
        <form action="/authors/add" method="POST">
            <label for="name">Name:</label>
            <input type="text" name="name" id="name" required>
            <label for="bio">Bio:</label>
            <input type="text" name="bio" id="bio" required>
            <label for="books">Books (Select multiple with Ctrl/Cmd):</label>
            <select name="books[]" id="books" multiple>
                <% books.forEach(book => { %>
                    <option value="<%= book.id %>"><%= book.title %></option>
                <% }) %>
            </select>
            <button type="submit">Create</button>
        </form>
    </main>
</body>
</html>

```
### views/newBook.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>New Book</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
    <header>
        <nav>
            <a href="/">Books & Authors</a>
            <a href="/">Home</a>
            <a href="/books/new">Add Book</a>
            <a href="/authors/new">Add Author</a>
        </nav>
    </header>
    <main>
        <h1>Create New Book</h1>
        <form action="/books/add" method="POST">
            <label for="title">Title:</label>
            <input type="text" name="title" id="title" required>
            <label for="authors">Authors (Select multiple with Ctrl/Cmd):</label>
            <select name="authors[]" id="authors" multiple>
                <% authors.forEach(author => { %>
                    <option value="<%= author.id %>"><%= author.name %></option>
                <% }) %>
            </select>
            <button type="submit">Create</button>
        </form>
    </main>
</body>
</html>

```
### views/authorDetails.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Author Details</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
    <header>
        <nav>
            <a href="/">Books & Authors</a>
            <a href="/">Home</a>
            <a href="/books/new">Add Book</a>
            <a href="/authors/new">Add Author</a>
        </nav>
    </header>
    <main>
        <form class="delete-form" action="/authors/<%= author.id %>/delete" method="POST" onsubmit="return confirm('Are you sure you want to delete this author?');">
            <input type="submit" value="Delete Author">
        </form>
        <h1><%= author.name %></h1>
        <p><%= author.bio %></p>
        <h2>Books</h2>
        <ul class="book-list">
            <% if (author.Books && author.Books.length > 0) { %>
                <% author.Books.forEach(book => { %>
                    <li>
                        <%= book.dataValues.title %>
                        <form class="delete-form" action="/books/<%= book.dataValues.id %>/delete" method="POST" onsubmit="return confirm('Are you sure you want to delete this book?');">
                            <input type="submit" value="Delete">
                        </form>
                    </li>
                <% }) %>
            <% } else { %>
                <li>No books found.</li>
            <% } %>
        </ul>
    </main>
</body>
</html>

```
### views/bookDetails.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Book Details</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
    <header>
        <nav>
            <a href="/">Books & Authors</a>
            <a href="/">Home</a>
            <a href="/books/new">Add Book</a>
            <a href="/authors/new">Add Author</a>
        </nav>
    </header>
    <main>
        <h1><%= book.title %></h1>
        <h2>Authors</h2>
        <ul class="author-list">
            <% if (book.Authors && book.Authors.length > 0) { %>
                <% book.Authors.forEach(author => { %>
                    <li><%= author.dataValues.name %></li>
                <% }) %>
            <% } else { %>
                <li>No authors found.</li>
            <% } %>
        </ul>
    </main>
</body>
</html>

```
