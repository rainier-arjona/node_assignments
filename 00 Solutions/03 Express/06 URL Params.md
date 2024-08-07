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
 * Retrieves the color from the request parameters.
 *
 * @param {string} color - The color value from the request parameters.
 * @returns {void}
 */
app.get('/color/:color', (req: Request, res: Response) => {
    const color = req.params.color;

    res.render('color', { color });
});

/**
 * Converts the given parameter to a number.
 *
 * @param {string} number - The parameter to be converted to a number.
 * @returns {number} The converted number.
 */
app.get('/number/:number', (req: Request, res: Response) => {
    let number = Number(req.params.number);

    number = number * 2;

    res.render('number', { number });
});

// Start the server
app.listen(port, () => {
    console.log(`Server is running at http://localhost:${port}`);
});
```

### color.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>URL Params</title>
</head>
<body>
    <h1 style="color: <%= color %>;"><%= color.charAt(0).toUpperCase() + color.slice(1).toLowerCase() %></h1>
    <h2 style="color: <%= color %>;">This text font color changes based on the url</h2>
    <h3>Try changing the color</h3>
</body>
</html>
```

### number.ejs
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>URL Params</title>
</head>
<body>
    <h1><%= number %></h1>
    <h2>Double the number passed in the URL</h2>
</body>
</html>
```