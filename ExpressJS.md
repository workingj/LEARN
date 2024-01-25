# ExpressJS

- zum schnellen und einfachen erstellen von API's
- light weight, MVC architecture
- `npm install express`

## Basic Server with Express/CommonJS

```javascript
const express = require('express');
const app = express();
const PORT = prorcess.env.PORT || 8000;
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

app.listen(PORT, () =>> console.log(`Server is listening on Port: ${PORT}`));

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
app.json(data);
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



```javascript

apt .get('/users/:id', (req res) => {
    console.log(req.params.id));
    console.log(req.query.sort));
    res.send('Check your server console!');
    
    });
```