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
  - [Node.js Built-in Modules](#nodejs-built-in-modules)
    - [`process.env`](#processenv)
  - [Import und Export von Modules in Node](#import-und-export-von-modules-in-node)
  - [File Acces](#file-acces)
    - [Sync](#sync)
    - [Async](#async)

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

const http = require('http');

const requestListener = (req, res) => {
    res.writeHead(200);
    res.end('Hello, Wold!');
}

const server = http.createServer(requestListener);
server.listen(8080, () => console.log('Server is live on Port: 8000'));
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

## [Node.js Built-in Modules](https://www.w3schools.com/nodejs/ref_modules.asp)

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
const http = require('http');
```

- **ES modules**
  - module needs `.mjs` extension
  - or nearest `package.json` needs property set to `"type": "module"`

```javascript
import http from 'http';
```

## File Acces

### Sync

```javascript
import fs from 'fs';

const file = './file.txt';

try {
    const data = fs.readFileSync(file, 'utf-8');
    console.log("file: ",data);
} catch(err) {
    console.error("file: ",data);
}
```

### Async

```javascript
import fs from 'fs';

const file = './file.txt';

try {
    const data = fs.readFile(file, 'utf-8', (err, data)=> {
        if(err) return console.error(`ERROR::read ${file}:`, err);
        
        console.log(`FILE: ${file}:`,data);
        return data;
    });
    console.log("file: ",data);
} catch(err) {
    console.error("file: ",data);
}
```
