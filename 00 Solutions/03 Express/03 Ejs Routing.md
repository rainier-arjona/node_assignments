### server.ts
```ts
import express, { Request, Response } from 'express';
import path from 'path';

const app = express();
const port = 3000;

/**
 * Set EJS as the view engine
 * @type {string}
 */
app.set('view engine', 'ejs');

/**
 * Serve static files from the 'public' folder
 * @type {string}
 */
app.use(express.static(path.join(__dirname, '..', 'src', 'public')));

/**
 * Set the 'views' directory for EJS templates
 * @type {string}
 */
app.set('views', path.join(__dirname, '..', 'src', 'views'));

/**
 * Define a route to render an EJS template with images
 * @param {Request} req - The request object
 * @param {Response} res - The response object
 */
app.get('/', (req: Request, res: Response) => {
    const images = [
        { url: '/images/ghibli1.jpg', alt: 'Totoro' },
        { url: '/images/ghibli2.jpg', alt: 'Arrietty' },
        { url: '/images/ghibli3.webp', alt: 'Spirited Away' },
        { url: '/images/ghibli4.jpg', alt: 'Princess Mononoke' },
        { url: '/images/ghibli5.jpg', alt: 'Ponyo' },
        { url: '/images/ghibli6.jpg', alt: 'Grave of the Fireflies' },
    ];

    res.render('index', { images });
});

app.get('/weather', (req: Request, res: Response) => {
    const weather = {
        city: 'New York',
        temperature: 21,
        description: 'Sunny',
        img: '/images/sunny.webp',
    };
    res.render('weather', { weather });
});

app.get('/products', (req: Request, res: Response) => {
    /**
     * Represents an array of products.
     * @typedef {Object} Product
     * @property {string} name - The name of the product.
     * @property {string} description - The description of the product.
     * @property {number} price - The price of the product.
     * @property {string} img - The image path of the product.
     */
    
    /**
     * An array of products.
     * @type {Product[]}
     */
    type Product = {
        name: string;
        description: string;
        price: number;
        img: string;
    };
    
    const products: Product[] = [
        {
            name: 'Laptop',
            description: 'A high-performance laptop with a 15.6-inch display, 16GB RAM, and a 512GB SSD. Ideal for professionals and gamers.',
            price: 1000,
            img: '/images/laptop.jpg'
        },
        {
            name: 'Wireless Earbuds',
            description: 'Compact and stylish wireless earbuds with noise cancellation and up to 8 hours of battery life. Perfect for on-the-go listening.',
            price: 150,
            img: '/images/earbuds.jpg'
        },
        {
            name: 'Smartwatch',
            description: 'A sleek smartwatch with a 1.3-inch touch display, heart rate monitoring, and GPS functionality. Track your fitness and stay connected.',
            price: 250,
            img: '/images/smartwatch.jpg'
        }
    ];
    
    res.render('products', { products });
});


// Start the server
app.listen(port, () => {
    console.log(`Server is running at http://localhost:${port}`);
});
```

### src/views/index.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Gallery</title>
    <link rel="stylesheet" href="/styles/style.css">
</head>
<body>
    <h1>Image Gallery</h1>
    <ul>
        <% images.forEach(image => { %>
            <li>
                <img src="<%= image.url %>" alt="<%= image.alt %>">
            </li>
        <% }); %>
    </ul>
</body>
</html>
```

### src/views/weather.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather Report</title>
</head>
<body>
    <!-- Header -->
    <header>
        <h1>Weather Report</h1>
    </header>
    <!-- Main content -->
    <main>
        <section>
            <!-- City name -->
            <h2><%= weather.city %></h2>
            <!-- Weather icon and description -->
            <figure>
                <img src="<%= weather.img %>" alt="Weather icon for <%= weather.city %>">
                <figcaption><%= weather.description %></figcaption>
            </figure>
            <!-- Temperature -->
            <p>Temperature: <%= weather.temperature %></p>
        </section>
    </main>
</body>
</html>
```

### src/views/products.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Products</title>
</head>
<body>
    <!-- Heading -->
    <h1>Available Products</h1>
    <ul>
        <!-- Loop through products -->
        <% products.forEach(product => { %>
            <li>
                <!-- Product image -->
                <img src="<%= product.img %>" alt="<%= product.name %>">
                <!-- Product name -->
                <%= product.name %> 
                <!-- Product description -->
                <%= product.description %>
                <!-- Product price -->
                $<%= product.price %>
            </li>
        <% }); %>
    </ul>
</body>
</html>
```