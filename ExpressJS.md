# ExpressJS

- [ExpressJS](#expressjs)
  - [Basic Server with Express/CommonJS](#basic-server-with-expresscommonjs)
    - [Routing](#routing)
  - [Set HTTP STATUS CODE for a Response](#set-http-status-code-for-a-response)
  - [GET](#get)
    - [Respons Type: String](#respons-type-string)
    - [Respons Type: JSON](#respons-type-json)
    - [Respons Type: HTML](#respons-type-html)
    - [Respons Type: Download](#respons-type-download)
    - [Respons Type: Redirect](#respons-type-redirect)
  - [Get Elements from an URL (parmas \& querys)](#get-elements-from-an-url-parmas--querys)
  - [View Engines](#view-engines)

## Basic Server with Express/CommonJS

```javascript
const express = require('express');
const app = express();
const PORT = prorcess.env.PORT || 8000;

app.listen(PORT, (err) => {
    if (err) return console.error(err);
    console.log(`Server is listening on Port: ${PORT} http://localhost:${PORT}`)
});
```

### Routing

- listening to HTTP verbs
- GET, POST, PUT, PATHCH, DELETE, HEAD

```javascript
app.get('/',(req, res) => res.send('Request a resource'));
app.post('/',(req, res) => res.send('We Create a resource !'));
app.put('/',(req, res) => res.send('Replace a resource !')); // repllace
app.patch('/',(req, res) => res.send('Update a resource !')); //update
app.delete('/',(req, res) => res.send('Delete a resource !'));
```

**or with cleaner code for the same route**

```javascript
app.route('/')
.get((req, res) => res.send('Request a resource'))
.post((req, res) => res.send('We Create a resource !'))
.put((req, res) => res.send('Replace a resource !'))
.patch((req, res) => res.send('Update a resource !'))
.delete((req, res) => res.send('Delete a resource !'));

app.listen(PORT, () =>> console.log(`Server is listening on Port: ${PORT}`));
```

## Set HTTP [STATUS CODE](https://http-status-code.de/) for a Response

- [https://developer.mozilla.org/en-US/docs/Web/HTTP/Status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

```javascript
app.get('/status',(req, res) => res.status(418).send('No Coffee here!'));
```

## GET

### Respons Type: String

```javascript
.get((req, res) => res.send('Request a resource'));
```

### Respons Type: JSON

```javascript
app.get((req, res) => {
    const data = {
        name: 'john',
        age: 30,
        mail: 'joe@mail.com'
    }
    res.json(data);
});
```

### Respons Type: HTML

```javascript
app.get((req, res) => {
    res.sendfile('index.html');
});
```

### Respons Type: Download

```javascript
app.get('/download',(req, res) => {
    const file = 'path/to/file.pdf';
    res.download(file);
});
```

### Respons Type: Redirect

```javascript
app.get((req, res) => {
    res.redirect('/new-location');
});
```

## Get Elements from an URL (parmas & querys)

```javascript
apt.get('/users/:id', (req res) => {
    console.log(req.params.id));
    console.log(req.query.sort));

    res.send('Check your server console!');
});
```

## View Engines

```javascript
app.set('view engine', 'pug');
app.set('view engine', 'ejs');

app.get('/pug', (req, res) => res.render('index'));
app.get('/ejs', (req, res) => res.render('index'));
```

```javascript
// ./views/index.ejs
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>EXPRESS JS</title>
  </head>
  <body>
    <h1>To Learn</h1>
    <ul>
      <li>RESPONSE TYPES</li>
      <li>VIEW ENGINES</li>
    </ul>
  </body>
</html>
```

```javascript
// ./views/index.pug
html
    head
        title COOL PUG TITLE
    body
        h1 PUG ENGINE
        p SOMETHING
```
