# NODE JS

- [NODE JS](#node-js)
  - [Overview](#overview)
  - [Node-Specific Functionality](#node-specific-functionality)
    - [Globals](#globals)
    - [INSTALL](#install)
      - [`install -D`](#install--d)
      - [`install -g`](#install--g)
  - [Simple Server](#simple-server)
  - [nodemon / npm -watch](#nodemon--npm--watch)
    - [nodemon](#nodemon)
    - [npm --watch](#npm---watch)
    - [Module](#module)
  - [Node.js Built-in Core-Modules](#nodejs-built-in-core-modules)
    - [`process.env`](#processenv)
  - [Import und Export von Modules in Node](#import-und-export-von-modules-in-node)
  - [File Access](#file-access)
    - [Sync](#sync)
      - [Reading](#reading)
    - [Async](#async)
      - [Reading](#reading-1)
      - [Writing](#writing)
      - [Deleting](#deleting)
    - [Directorys](#directorys)
    - [Streams](#streams)
      - [reading from streams](#reading-from-streams)
      - [writing to streams](#writing-to-streams)
      - [piping](#piping)
  - [Events](#events)
  - [Global Oject](#global-oject)

## Overview

- nvm node version manager
- npm node package manager (yarn)
- npx execute modules
- `npm init` creates a note package
- `npm init -y` creates a note package skips configuration

## Node-Specific Functionality

### Globals

- each file is treated as a module
- require() is a function used to import modules from other files or Node packages
- -process is an object referencing the actual computer process running a Node program and allows for access to command-line arguments and more

### INSTALL

[A friendly guide to `npm install` flags](https://7.dev/npm-install-flags/)

#### `install -D`

- only add the package to your “dev dependencies"
- `npm install --save-dev`
- `npm i -D`

#### `install -g`

- `-g`, `--global`: If you want to use a package in lots of projects, you might install it globally, meaning it gets installed in a special place that all your Node.js projects can reach.

## Simple Server

```javascript
// server.js
console.log(process.env.PWD);
console.log(process.memoryUsage());
console.log(process.argv);

const http = require("http");

const requestListener = (req, res) => {
  res.writeHead(200);
  res.end("Hello, Wold!");
};

const server = http.createServer(requestListener);
server.listen(8080, () => console.log("Server is live on Port: 8000"));
```

**Run** `server.js`with `node server.js`

## nodemon / npm -watch

### nodemon

- enables hot reloade
- `npm i nodemon -d //dev dependencie`

```json
{
  "sripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "alias": "nodemon filename.js"
  }
}
```

### npm --watch

```json
{
  "sripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "alias": "node --watch filename.js"
  }
}
```

### Module

- [Node Modules Documentation](https://nodejs.org/dist/latest/docs/api/)

## [Node.js Built-in Core-Modules](https://www.w3schools.com/nodejs/ref_modules.asp)

### [`process.env`](https://nodejs.org/api/process.html)

- property is an object which stores and controls information about the environment in which the process is currently running

```javascript
console.log(process.env.PWD);
console.log(process.memoryUsage());
console.log(process.argv);
```

## Import und Export von Modules in Node

- `.gitignore` node_modules eintragen
- **Common JS**
  - **import:** `require()`
  - **export:** `module.export`

```javascript
const http = require("http");
```

- **ES modules**
  - module needs `.mjs` extension
  - or nearest `package.json` needs property set to `"type": "module"`

```javascript
import http from "http";
import fs from "fs";
import os from "os";
```

## File Access

- [NODEJS DOCS: Node Filesystem Module](https://nodejs.org/api/fs.html)
- [W3 Node.js File System Module](https://www.w3schools.com/nodejs/ref_fs.asp)

### Sync

#### Reading

```javascript
try {
  const data = fs.readFileSync("./file.txt", "utf8");
  console.log("file: ", data);
} catch (err) {
  console.error("file: ", data);
}
```

### Async

#### Reading

```javascript
import fs from "fs";

try {
  const data = fs.readFile("./file.txt", "utf-8", (err, data) => {
    if (err) return console.error(`ERROR::read ${file}:`, err);

    console.log(`FILE: ${file}:`, data);
    return data;
  });
  console.log("file: ", data);
} catch (err) {
  console.error("file: ", data);
}
```

#### Writing

```javascript
// writing files
fs.writeFile("./docs/blog.txt", "hello, world", () => {
  console.log("file was written");
});
```

#### Deleting

```javascript
// deleting files
if (fs.existsSync("./docs/deleteme.txt")) {
  fs.unlink("./docs/deleteme.txt", (err) => {
    if (err) {
      console.error(err);
    }
    console.log("file deleted");
  });
}
```

### Directorys

```javascript
// directories
if (!fs.existsSync("./assets")) {
  fs.mkdir("./assets", (err) => {
    if (err) {
      console.error(err);
    }
    console.log("folder created");
  });
} else {
  fs.rmdir("./assets", (err) => {
    if (err) {
      console.error(err);
    }
    console.log("folder deleted");
  });
}
```

### Streams

#### reading from streams

```javascript
const fs = require('fs');
const readStream = fs.createReadStream('./docs/blog3.txt', { encoding: 'utf8'});

readStream.on('data', chunk => {
  console.log(c'----- new chunk -----');
  console.log(chunck);
});
```

#### writing to streams

```javascript
const readStream = fs.createReadStream("./docs/blog3.txt", {encoding: "utf8",});
const writeStream = fs.createWriteStream("./docs/blog4.txt");

readStream.on("data", (chunk) => {
  writeStream.write("\nNEW CHUNK:\n");
  writeStream.write(chunk);
});
```

#### piping

```javascript
const readStream = fs.createReadStream("./docs/blog3.txt", {encoding: "utf8",});
const writeStream = fs.createWriteStream("./docs/blog4.txt");
readStream.pipe(writeStream);
```

## Events

```javascript
// Require in the 'events' core module
let events = require("events");

// Create an instance of the EventEmitter class
let myEmitter = new events.EventEmitter();

let newUserListener = (data) => {
  console.log(`We have a new user: ${data}.`);
};

// Assign the newUserListener function as the listener callback for 'new user' events
myEmitter.on("new user", newUserListener);

// Emit a 'new user' event
myEmitter.emit("new user", "Lily Pad"); //newUserListener will be invoked with 'Lily Pad'
```

## [Global Oject](https://nodejs.org/api/globals.html)

- A global object is an object that always exists in the global scope.
- like the `window`-Object in the browse, is implied, no need to be called

```javascript
// The directory name of the current module This is the same as the path.dirname(__filename)
console.log(__dirname);
// Prints: /Users/mjr

// The file name of the current module, the current module file's absolute path with symlinks resolved.
console.log(__filename);
// Prints: /Users/mjr/example.js
```
