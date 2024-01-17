# react

- React ist fpr SPA's gedacht
- ein Modul gibt immer ein Element zurück
- daten in react fließen immer von oben anch unten

## Best Practice

- It's good practice to put everything that can go outside of a component outside of it

## Create new Project

### using Vite

1. `npm create vite@latest`
2. `< enter project settings >`
3. `cd` in to project folder
4. `npm i / npm install`
5. `npm run dev`

- JSX hat replacement Keywords

## Modules

### exports and imports (`named`, `default`, `named default`)

- A default export can be only one in a file or module.
- But a module can have more than one Named export

```javascript
import { useState } from 'react'
import {Routes, Route, NavLink} from 'react-router-dom'
import Axios from "./components/Axios"; // default exports dont need {}
import Quote from './components/Quote'
import './App.css'
```

#### Named exports

- Once we define a component with the export keyword, we can access and import those exported functions using the import keyword.

```javascript
//NetData.jsx
export function Axios() {
  return <h1>I’m Axios.</h1>;
}

// or

function Quotes() { ...}
function Axios() { ...}

export { Quotes, Axios }; 
```

#### Named imports

```javascript
import {Axios, Quote} from ".(NetData";
```

#### Default exports

- only one element can be exported to another component at a time as a default export. In other words, a file can have only one default export.

```javascript
// Axios.jsx
// the function will have the name of the file
export default function () {
  return <h1>I’m sending Net Data .</h1>;
}
```

#### Default imports

- We do not need to wrap the binding inside the curly braces.
- Can be given any name as the name of that exported binding.

```javascript
import MyNAme from “./Axios.jsx”; 
import { Quots, Axios} from “./America.js”; 
```

#### Combined named and default imports

- The default bindings must come first during importing.
- The non-default (named) binding must be surrounded by curly braces {…}

```javascript
import MyNAme, {Quots, Axios} from “./Axios.jsx”; 
```

#### Binding Aiasing

```javascript
import AdminLayout from "layouts/Admin/Admin.js";
// is a shorhand for
import {default as AdminLayout} from "layouts/Admin/Admin.js";
```

**or**

```javascript
// Admin.js
export {Admin as AdminLayout}

```

## How to pass a parameter to an event handler or callback?

  You can use an arrow function to wrap around an event handler and pass parameters:

```jsx
<button onClick={() => this.handleClick(id)} />
```

This is an equivalent to calling .bind:

```jsx
<button onClick={this.handleClick.bind(this, id)} />
```

Apart from these two approaches, you can also pass arguments to a function which is defined as arrow function

```jsx
<button onClick={this.handleClick(id)} />;
handleClick = (id) => () => {
  console.log('Hello, your ticket number is', id);
};
```

## UseEffect

```javascript
useEffect(() => {
  //Runs only on the first render
}, []);
```

```javascript
useEffect(() => {
  //Runs on every render
});
```

```javascript
useEffect(() => {
  //Runs on the first render
  //And any time any dependency value changes
}, [prop, state]);
```

## Routing

### React Router Dom

#### required Package

`npm i react-router-dom`

#### in main.jsx

```javascript
  <BrowserRouter>
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </BrowserRouter>
```

#### imports

```javascript
import {Routes, Route, NavLink, Link} from 'react-router-dom'
```

#### NavLinks

```javascript
import { NavLink } from "react-router-dom";

<NavLink
  to="/messages"
  className={({ isActive, isPending }) =>
    isPending ? "pending" : isActive ? "active" : ""
  }
>
  Messages
</NavLink>;

//CSS
a.active {
  ...
}
```

#### 404

```javascript
<Route path='*' element={<NotFound />} />
```
