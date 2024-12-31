# Javascript

- [Javascript](#javascript)
  - [Link to external JavaScript file `<script>`-Tag](#link-to-external-javascript-file-script-tag)
  - [Keywords](#keywords)
  - [Modules](#modules)
  - [Operants](#operants)
    - [`== & ===`](#--)
  - [Objects](#objects)
    - [Function Borrowing with `bind()`](#function-borrowing-with-bind)
  - [Loops](#loops)
    - [for...of](#forof)
  - [Export - Import, exposing to other files](#export---import-exposing-to-other-files)
  - [Date and Time](#date-and-time)
  - [URL'S](#urls)
  - [Functions](#functions)
    - [Arrow functions](#arrow-functions)
    - [Anonymous Functions](#anonymous-functions)
    - [Higher Order Functions](#higher-order-functions)
  - [Explicit Function Binding](#explicit-function-binding)
  - [Scheduling Functions with setTimeout and setInterval](#scheduling-functions-with-settimeout-and-setinterval)
  - [Zero delay setTimeout](#zero-delay-settimeout)
  - [Array Functions](#array-functions)
    - [Sort strings in objects](#sort-strings-in-objects)
  - [Async/Await](#asyncawait)
    - [Async Syntax](#async-syntax)
    - [Await Syntax](#await-syntax)
    - [Promises](#promises)
      - [Creating your own Promis](#creating-your-own-promis)
  - [Fetch API](#fetch-api)
    - [Fetch Sending](#fetch-sending)
  - [Date \& Time](#date--time)

## Link to external JavaScript file [`<script>`-Tag](https://www.w3schools.com/tags/tag_script.asp)

- `defer` ensures that the entire HTML file has been parsed before the script is executed

  ```javascript
  <script src="example.js" defer></script>
  ```

- `async` will allow the HTML parser to continue parsing as the script is being downloaded, but will execute immediately after it has been downloaded, optimizes page loading time, usfull for indipendend scripts

  ```javascript
  <script src="example.js" async></script>
  ```

## Keywords

- `var` erstell immer globale variablen
- `let` lässt sich immer wieder neu zuweisen
- `const` lässt sich nur einmal zuweisen
- `this`
  - In an object method, `this` refers to the object.
  - Alone, `this` refers to the global object.
  - In a function, `this` refers to the global object.
  - In a function, in strict mode, `this` is `undefined`.
  - In an event, `this` refers to the element that received the event.
  - Methods like `call()`, `apply()`, and `bind()` can refer `this` to any object.

## [Modules](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules)

- Modules are automatically interpreted in strict mode.
- Use of native JavaScript modules is dependent on the [import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import) and [export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export) statements
- **`export`** is used to export values from a JavaScript module
  - In order to use the export declaration in a source file, the file must be interpreted by the runtime as a module. In HTML, this is done by adding `type="module"` to the `<script>` tag, or by being imported by another module
  - works only on top-level items
  - use a single export statement at the end of your module file

    ```javascript
    export { name, draw, reportArea, reportPerimeter };
    ```

- **`import`**s is used to import read-only live bindings which are exported by another module

    ```javascript
    import {name,draw,reportArea,reportPerimeter } from "./modules/square.js";
    statement {  comma-separated list }            keyword  "module specifier";
    ```

  - **Binding** is an association of an identifier with a value
- [dynamic import](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/import)
  - dynamic imports are only evaluated when needed, and permit greater syntactic flexibility
  - `import(moduleName)` is a function-like expression that allows loading an ECMAScript module asynchronously and dynamically into a potentially non-module environment

## Operants

### `== & ===`

```javascript
const num = 10;
const str = "10";

console.log(num == str); // true - The values are the same after type conversion
console.log(num === str); // false - The values are different types and not equal
```

## Objects

```javascript
console.log(Object.keys(data));
console.log(Object.getOwnPropertyNames(Object.getPrototypeOf(data)));
```

### Function Borrowing with `bind()`

- With the `bind()` method, an object can borrow a method from another object.

## Loops

### [for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of?retiredLocale=de)

- most performant for collections

```javascript
const array1 = ["a", "b", "c"];

for (const value of iterable) {
  console.log(value);
}
```

## Export - Import, exposing to other files

```javascript
// file.js
export const MY_VALUE = 10;

export function add(num1, num2) {
  return num1 + num2;
}

// file.spec.js
import { MY_VALUE, add } from "./file";

add(MY_VALUE, 5);
// => 15
```

## Date and Time

```javascript
// Get Time
let now = new Date();

console.log(now.getHours() + ":" + now.getMinutes());
console.log(now.getDate() + "." + now.getMonth());

// Date
var date = new Date();
console.log(date);
console.log(`${date.getFullYear()}-${date.getMonth()}-${date.getDate()}`);
console.log(`${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`);

// UNIX Timestamp
Date.now(); // 1735499959142
Math.floor(Date.now() / 1000); // 173549995
```

## URL'S

```javascript
const url = new URL('https://example.com/');

for (field in url) {
  console.log(field);
}

const plainObject = {
  hash:         url.hash,
  host:         url.host,
  hostname:     url.hostname,
  href:         url.href,
  origin:       url.origin,
  password:     url.password,
  pathname:     url.pathname,
  port:         url.port,
  protocol:     url.protocol,
  search:       url.search,
  searchParams: url.searchParams,
  username:     url.username
}
```

## Functions

- Functions parameter can have default values
- Functions are treated as objects in javascript
- **Function Call: `myFunction()`**
- **Functiom Reference: `myFunciton`**

### Arrow functions

- Arrow functions implicitly `return` the expression right after `=>`, so you didn’t need a return statemen
- However, you must write `return` explicitly if your `=>` is followed by a `{` curly brace!

### Anonymous Functions

- anonymous functions only for one single call
- anonymous functions can be stored in variables

### Higher Order Functions

- funcitons that take or return other functions are called higher order functions
- Functions as Arguments are commonly refered as Callback functions
- functions can be createt at runtime and returnd from an other function

## Explicit Function Binding

- The `call()` and `apply()` methods are predefined JavaScript methods.
- They can both be used to call an object method with another object as argument.

## [Scheduling Functions with setTimeout and setInterval](https://javascript.info/settimeout-setinterval)

- **setTimeout()**: run a function once after the interval of time
- 1000 ms = 1 second
- Returns a “timer identifier” `timerId` that we can use to cancel the execution.
- There’s a side effect. A function references the outer lexical environment, so, while it lives, outer variables live too. They may take much more memory than the function itself. So when we don’t need the scheduled function anymore, it’s better to cancel it, even if it’s very small.
- The browser limits the minimal delay for five or more nested calls of setTimeout or for setInterval (after 5th call) to 4ms. That’s for historical reasons.

  ```javascript
  // SIGNATURE
  let timerId = setTimeout(func|code, [delay], [arg1], [arg2], ...)

  function sayHi(phrase, who) {
    alert( phrase + ', ' + who );
  }

  setTimeout(sayHi, 1000, "Hello", "John"); // Hello, John
  setTimeout(sayHi, 1000);

  let timerId = setTimeout(...); //returns timer identifyer
  clearTimeout(timerId); // doesn't become null after canceling
  ```

- **setInterval()**: run a function repeatedly, starting after the interval of time, then repeating continuously at that interval
- Nested setTimeout calls are a more flexible alternative to setInterval, allowing us to set the time between executions more precisely.

  ```javascript
  // SIGNATURE
  let timerId = setInterval(func|code, [delay], [arg1], [arg2], ...)

  function sayHi(phrase, who) {
    alert( phrase + ', ' + who );
  }

  setTimeout(sayHi, 1000, "Hello", "John"); // Hello, John
  setTimeout(sayHi, 1000);
  ```

## Zero delay setTimeout

- This schedules the execution as soon as possible. But the scheduler will invoke it only after the currently executing script is complete.

  ```javascript
  setTimeout(() => alert("World"));
  ```

## Array Functions

- [**`.forEach()`**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) is used to execute the same code on every element in an array but does not change the array and returns undefined.
- [**`.map()`**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) executes the same code on every element in an array and returns a new array with the updated elements.
- [**`.filter()`**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter) checks every element in an array to see if it meets certain criteria and returns a new array with the elements that return truthy for the criteria.
- [**`.findIndex()`**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex) returns the index of the first element of an array that satisfies a condition in the callback function. It returns -1 if none of the elements in the array satisfies the condition.
- [**`.reduce()`**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) iterates through an array and takes the values of the elements and returns a single value.

### Sort strings in objects

```javascript
const data = {
    "id": 1,
    "name": "Russian Federation (the)",
 },
 {
     "id": 2,
     "name": "Bhutan",
 },

const sdata = data.sort((a, b) => {
    if (a.name < b.name) { return -1; }
    if (a.name > b.name) { return 1; }
    return 0;
});

```

## Async/Await

- async and await make promises easier to write
- `async` keyword makes a function return a Promise
- `await` keyword makes a function wait for a Promise

### Async Syntax

```javascript
async function myFunction() {
  return "Hello";
}
myFunction().then(
  function(value) {myDisplayer(value);},
  function(error) {myDisplayer(error);}
);
```

### Await Syntax

- The await keyword can only be used inside an async function.
- The await keyword makes the function pause the execution and wait for a resolved promise before it continues
- Is used to handel resolved promise objects like the then() method
- errors are not handled, use try/catch-blocks

```Javascript
async function gamingTime() {
  try {
    // stores the Promise's resolve value
    const canIGame = await isThereTimeToGameFunction();
    console.log(canIGame);
  } catch (error) {
    // We get here if the Promise rejects
    console.error(error);
  }
}

gamingTime();
```

### Promises

- A Promise is an object, that placeholds the eventual completion of an asynchronous operation

```Javascript
async function myDisplay() {
  let myPromise = new Promise(function(resolve, reject) {
    resolve("I love You !!");
  });
  document.getElementById("demo").innerHTML = await myPromise;
}

myDisplay();
```

#### Creating your own Promis

```javascript
// This is a plain promise
const isThereTimeToGame = new Promise((resolve, reject) => {
  Math.random() > 0.5
    ? resolve("There is still time for another quest!")
    : reject("You got to go to bed now :( ");
});

isThereTimeToGame 
  .then((success) => console.log(success))
  .catch((reason) => console.log(reason));
```

## [Fetch API](https://www.w3schools.com/js/js_api_fetch.asp)

- XMLHTTPRequest-object used before fetch
- [Using the fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)
- fetch response is a Respons-Object with a readable stream in the body
- fetch does not see HTTP ERROR CODES as errors, response must be checked

```Javascript
// Fetch with Promise method chaining
const myFetchFunction = () => {
  fetch("https://geek-jokes.sameerkumar.website/api")
    .then((response) => {
      console.log(response);
      if (response.ok) return response.json();
      throw new Error(`The fetch failed with a status of ${response.status}`);
    })
    .then((finalResult) => console.log(finalResult))
    .catch((error) => console.log(error));
};
```

```javascript
// Fetch with async and await (now returns a promise)
const myFetchFunctionAsync = async () => {
  try {
    const myFetch = await fetch("https://geek-jokes.sameerkumar.website/api");
    if (!myFetch.ok)
      throw new Error(`The fetch failed with a status of ${myFetch.status}`);
    const parsedData = await myFetch.json();
    console.log(parsedData);
  } catch (error) {
    console.log(error);
  }
};
```

### Fetch Sending


