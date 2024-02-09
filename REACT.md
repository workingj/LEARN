# react

- [react](#react)
  - [Best Practice](#best-practice)
  - [Create new Project](#create-new-project)
  - [Modules](#modules)
  - [How to pass a parameter to an event handler or callback?](#how-to-pass-a-parameter-to-an-event-handler-or-callback)
  - [UseEffect](#useeffect)
  - [Routing](#routing)
  - [Fetching](#fetching)

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
import { useState } from "react";
import { Routes, Route, NavLink } from "react-router-dom";
import Axios from "./components/Axios"; // default exports dont need {}
import Quote from "./components/Quote";
import "./App.css";
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
import { Axios, Quote } from ".(NetData";
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
import { default as AdminLayout } from "layouts/Admin/Admin.js";
```

**or**

```javascript
// Admin.js
export { Admin as AdminLayout };
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
  console.log("Hello, your ticket number is", id);
};
```

## UseEffect

```javascript
//Runs only on the first render
useEffect(() => {}, []);
```

```javascript
//Runs on every render
useEffect(() => {});
```

```javascript
//Runs on the first render and any time any dependency value changes
useEffect(() => {}, [prop, state]);
```

## Routing

[YT-React Router in Depth]([https://www.youtube.com/playlist?list=PL4cUxeGkcC9iVKmtNuCeIswnQ97in2GGf)

### React Router Dom

#### required Package

`npm i react-router-dom`

#### in main.jsx

```javascript
import { BrowserRouter } from "react-router-dom";

ReactDOM.createRoot(document.getElementById("root")).render(
  // Wraps the Complete Application
  <BrowserRouter>
    <React.StrictMode>
      <App />
    </React.StrictMode>
  </BrowserRouter>
);
```

#### in app.jsx

- `Link` and `NavLink` keep the browser from sending requests to the server

```javascript
import { Routes, Route, NavLink } from "react-router-dom";

return (
  <>
    <nav>
      // NavLinks
      <Link>Home</Link> // has no active class
      <NavLink to="products">Product Table</NavLink>
      <NavLink to="quotes">Quotes</NavLink>
    </nav>
    // Routs for Page Structure
    <Routes>
      // Parent for n Route-Coponents
      <Route path="/" element={<Home />} />
      
      //  Can also be
       <Route index element={<Home />} />
      
      <Route path="quotes" element={<Quote />} />
      <Route path="axios" element={<Axios />} />
      <Route
        path="products"
        element={<FilterableProductTable products={PRODUCTS} />}
      />
      // For invalid routs
      <Route path="*" element={<NotFound />} />
    </Routes>
  </>
```

### NavLinks with active status

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
```

- CSS

```CSS
a.active {
  ...
}
```

#### 404 Error Pages

```javascript
<Route path="*" element={<NotFound />} />
```

## Fetching

- This is a very common pattern when fetching data in a useEffect that might be triggered several times.
- If `param` changes value, fetchData will be called twice. If this happens quickly, it's possible to have a race condition where the first call resolves after the second one, and thus the state will hold the older value.
- The way to solve that issue is to have a variable which controls wether to update the state or not.

```javascript
useEffect(() => {
  let isSubscribed = true;

  // declare the async data fetching function
  const fetchData = async () => {
    // get the data from the api
    const data = await fetch(`https://yourapi.com?param=${param}`);
    // convert the data to json
    const json = await response.json();

    // set state with the result if `isSubscribed` is true
    if (isSubscribed) {
      setData(json);
    }
  };

  // call the function
  fetchData()
    // make sure to catch any error
    .catch(console.error);

  // cancel any future `setData`
  return () => (isSubscribed = false);
}, [param]);
```
