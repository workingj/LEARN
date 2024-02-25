# react

- [react](#react)
  - [Best Practice](#best-practice)
  - [Create new Project](#create-new-project)
  - [Modules](#modules)
    - [exports and imports (`named`, `default`, `named default`)](#exports-and-imports-named-default-named-default)
  - [UI](#ui)
    - [Components](#components)
    - [JSX](#jsx)
      - [JavaScript in JSX](#javascript-in-jsx)
  - [Probs](#probs)
  - [State](#state)
    - [react state preservation behavior](#react-state-preservation-behavior)
  - [How to pass a parameter to an event handler or callback?](#how-to-pass-a-parameter-to-an-event-handler-or-callback)
  - [UseEffect](#useeffect)
  - [Routing](#routing)
    - [React Router Dom](#react-router-dom)
      - [required Package](#required-package)
      - [in main.jsx](#in-mainjsx)
      - [in app.jsx](#in-appjsx)
    - [NavLinks with active status](#navlinks-with-active-status)
      - [404 Error Pages](#404-error-pages)
  - [Fetching](#fetching)

## Best Practice

- It's good practice to put everything that can go outside of a component outside of it

## Create new Project

**using Vite**

1. `npm create vite@latest`
2. `< enter project settings >`
3. `cd` in to project folder
4. `npm i / npm install`
5. `npm run dev`

**LAN dev server**

- `http://<YOUR_COMPUTER'S_IP>:<YOUR_DEV_SERVER_PORT_NUMBER>`
- Linux: `hostname -I | awk '{print $1}'`
- Windows: `ipconfig | findstr IPv4`
- Start Vite with host option:`npm run dev -- --host`
- or package.json: `"dev" : "vite --host"`

## Modules

### exports and imports (`named`, `default`, `named default`)

- How you export your component dictates how you must import it.
- use **named** exports if it exports **multiple components** and values.
- use **default** exports if the file exports **only one component**
- When you write a default import, you can put any name you want after import it would still provide you with the same default export.
- In contrast, with named imports, the name has to match on both sides.
- The default bindings must come first during importing.
- The non-default (named) binding must be surrounded by curly braces {…}
- avoid mixing between default and named exports in a single file

| Syntax        | Export statement                       | Import statement                                  |
| ------------- | -------------------------------------- | ------------------------------------------------- |
| Default       | `export default function Button() {}`  | `import Button from './Button.js';`               |
| Named         | `export function Button() {}`          | `import { Button } from './Button.js';`           |
| Named Default | `export default function Gallery() {}` | `import Gallery from './Gallery.js';`             |
|               | `export function Profile() {}`         | `import { Profile } from './Gallery.js';`         |
|               |                                        | `import Gallery, {Profile} from “./Gallery.jsx”;` |

**Binding Aliasing**

```javascript
import AdminLayout from "layouts/Admin/Admin.js";
// is a shorhand for
import { default as AdminLayout } from "layouts/Admin/Admin.js";
export { Admin as AdminDashboard };
```

## UI

### Components

- React applications are built from isolated pieces of UI called components.
- A React component is a JavaScript function that you can sprinkle with markup
- You can declare many components in one file
- React components use a syntax extension called JSX and can display dynamic information
- JSX lets you write HTML-like markup inside a JavaScript file, keeping rendering logic and content in the same place
- you can **use curly braces** in your JSX to “open a window” to JavaScript, **to add a logic** or reference a dynamic property inside
- Every parent component can **pass some information to its child** components by giving them **props**, you can pass any JavaScript value through them, including objects, arrays, functions, and even JSX
- you can **conditionally** render JSX using JavaScript syntax like if statements, &&, and ? : operators
- You can use JavaScript’s filter() and map() to filter and transform your array of data into an array of components. For each array item, you will need to specify a unique key.
- **Keys** let React keep track of each item’s place in the list even if the list changes
- **React components names must start with a capital letter**
- **to return multy line markup it must be wraped in parentheses**
- PERFORMANCE: **never nest Component definitions**, alway define them in the top level

### JSX

JSX is a syntax extension for JavaScript that lets you write HTML-like markup inside a JavaScript file

**Rules**

1. Return a single root element, wrap all Elements in a single parent tag.
   - **[Fragment](https://react.dev/reference/react/Fragment)** let you group elements without an effect on the resulting DOM; it is the same as if the elements were not grouped `<><Child /><Child /></>`
   - If you want to pass key to a Fragment, you have to explicitly import Fragment from 'react' and render `<Fragment key={yourKey}>...</Fragment>`.
2. Close all the tags
3. **camelCase**, many HTML and SVG attributes are written in camelCase, because attributes in JSX become keys of JavaScript objects, `stroke-width -> strokeWidth`
   - [List of DOM component Prperties and Events](https://react.dev/reference/react-dom/components/common)

#### JavaScript in JSX

- JSX attributes inside single or double quotes are passed as **strings**
- **Curly braces** let you bring JavaScript logic and variables into your markup, inside the JSX tag content or immediately after = in attributes
- **double curlies** `{{` and `}}` is a JavaScript object inside JSX curly braces, used for CSS and other objects

```Javascript
const avatar = 'https://i.imgur.com/7vQD0fPs.jpg';
const name = 'Gregorio Y. Zara';
return (
  <>
    <h1 className="avatar">{name}'s To Do List</h1>// reference to a variable
    <img
      className="avatar" // String
      src={avatar}       // reference to a variable
    />
    <b>{Date.now()}</b>
  <ul style={{ // Object for CSS
    backgroundColor: 'black',
    color: 'pink'
  }}>
    <li>Improve the videophone</li>
   </ul>
  </>
);
```

## Probs

- components use props to communicate with each other
- you can pass any JavaScript value through them, including objects, arrays, and functions
- add them to the JSX, just like you would with HTML attributes
- you can pass any props to your own components
- use the destructuring syntax `function Avatar({ person, size })` to read them
-

## State

### [react state preservation behavior](https://gist.github.com/clemmy/b3ef00f9507909429d8aa0d3ee4f986b)

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
