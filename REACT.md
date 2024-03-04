# react

Version: `react-dom@18.2.0`

- [react](#react)
  - [Create new Project](#create-new-project)
  - [Modules](#modules)
  - [UI](#ui)
    - [Components](#components)
    - [JSX](#jsx)
    - [Probs](#probs)
    - [Conditional Rendering](#conditional-rendering)
    - [Rendering Lists](#rendering-lists)
  - [Event Handlers and Interactivity](#event-handlers-and-interactivity)
  - [State and the **`useState`** Hook](#state-and-the-usestate-hook)
  - [UseEffect](#useeffect)
  - [Routing](#routing)
    - [React Router Dom](#react-router-dom)
      - [required Package](#required-package)
      - [in main.jsx](#in-mainjsx)
      - [in app.jsx](#in-appjsx)
    - [NavLinks with active status](#navlinks-with-active-status)
      - [404 Error Pages](#404-error-pages)
  - [Fetching](#fetching)
  - [Best Practice \& Tipps](#best-practice--tipps)
  - [How To's](#how-tos)
    - [Importing Images](#importing-images)
    - [How to pass a parameter to an event handler or callback?](#how-to-pass-a-parameter-to-an-event-handler-or-callback)
    - [Using Array in State](#using-array-in-state)
    - [Storing information from previous renders](#storing-information-from-previous-renders)

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
- Or package.json: `"dev" : "vite --host"`

## Modules

**exports and imports (`named`, `default`, `named default`)**

- How you export your component dictates how you must import it.
- Use **named** exports if it exports **multiple components** and values.
- Use **default** exports if the file exports **only one component**
- When you write a default import, you can put any name you want after import it would still provide you with the same default export.
- In contrast, with named imports, the name has to match on both sides.
- The default bindings must come first during importing.
- The non-default (named) binding must be surrounded by curly braces {…}
- Avoid mixing between default and named exports in a single file

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
- You can **use curly braces** in your JSX to “open a window” to JavaScript, **to add a logic** or reference a dynamic property inside
- Every parent component can **pass some information to its child** components by giving them **props**, you can pass any JavaScript value through them, including objects, arrays, functions, and even JSX
- You can **conditionally** render JSX using JavaScript syntax like if statements, &&, and ? : operators
- You can use JavaScript’s filter() and map() to filter and transform your array of data into an array of components. For each array item, you will need to specify a unique key.
- **Keys** let React keep track of each item’s place in the list even if the list changes
- **React components names must start with a capital letter**
- **to return multy line markup it must be wraped in parentheses**
- **PERFORMANCE**: **never nest Component definitions**, alway define them in the top level

### JSX

JSX is a syntax extension for JavaScript that lets you write HTML-like markup inside a JavaScript file

**Rules**

1. Return a single root element, wrap all Elements in a single parent tag.
   - **[Fragment](https://react.dev/reference/react/Fragment)** let you group elements without an effect on the resulting DOM; it is the same as if the elements were not grouped `<><Child /><Child /></>`
   - If you want to pass key to a Fragment, you have to explicitly import Fragment from 'react' and render `<Fragment key={yourKey}>...</Fragment>`.
2. Close all the tags
3. **camelCase**, many HTML and SVG attributes are written in camelCase, because attributes in JSX become keys of JavaScript objects, `stroke-width -> strokeWidth`
   - [List of DOM component Prperties and Events](https://react.dev/reference/react-dom/components/common)

**JavaScript in JSX**

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

### Probs

- Components use props to communicate with each other
- They serve the same role as arguments serve for functions
- They are read-only snapshots in time: every render receives a new version of props
- You can **pass any JavaScript** value through them to your own components, including objects, arrays, and functions
- Add them to the **JSX**, just **like** you would with **HTML attributes** `size={value}`
- Use the **destructuring** syntax `function Avatar({ person, size })` to read them
- Nested components are received in the parent via the children prob `<Card><Avatar /></Card>`
- You can specify a default/fallback value for missing and undefined props `function Avatar({ person, size = 100 })`
- You can’t change props, for interactivity, you’ll need to set state

**passing pobs**

```javascript
// Parent Component
<Avatar
  person={{ name: 'Lin Lanying', imageId: '1bX5QH6' }}
  size={100}
/>
// With spread syntax
<Avatar {...props} />
// Nested components
<Avatar>
  <Card />
</Avatar>
```

**receiving pobs**

```javascript
// Avatar.jsx
function Avatar({ person, size = 100 }) {
  // with default value for size
  // person and size are available here
}
// or
function Avatar(props) {
  let person = props.person;
  let size = props.size;
  // ...
}
// using nested children
function Card({ children }) {
  return <>{children}</>;
}
```

### Conditional Rendering

**Conditionally returning JSX with if...else**

```javascript
if (isPacked) {
  return <li className="item">{name} ✔</li>;
}
return <li className="item">{name}</li>;
```

**Conditionally including JSX with (ternary) operator (`? :`)**

- {`cond ? <A /> : <B />`} means “if cond is true, render `<A />`, otherwise `<B />`”.

```javascript
return <li className="item">{isPacked ? name + " ✔" : name}</li>;
```

**Conditionally including JSX with Logical AND operator (`&&`)**

- Returns the value of its right side if the left side is true
- Evaluating to `false` are: `false` ,`null` ,`NaN` ,`0`, `undefined` and empty string (`""` or `''` or `` )
- **PITFALL** Don’t put numbers on the left side of `&&`

```javascript
return (
  <li className="item">
    {name} {isPacked && "✔"}
  </li>
);
```

**Conditionally returning nothing with `null`**

```javascript
if (isPacked) {
  return null;
}
return <li className="item">{name}</li>;
```

**Conditionally including JSX**

```javascript
if (isPacked) {
  return null;
}
return <li className="item">{name}</li>;
```

### Rendering Lists

- You can use the **JavaScript array methods** to manipulate an array of data

**Rendering data from arrays**

```javascript
export default function List({ people }) {
  const listItems = people.map((person) => <li>{person}</li>);
  return <ul>{listItems}</ul>;
}
// or
const listItems = chemists.map((person) => (
  <li>
    <img src={getImageUrl(person)} alt={person.name} />
    <p>
      <b>{person.name}:</b>
      {" " + person.profession + " "}
      known for {person.accomplishment}
    </p>
  </li>
));
```

**Filtering arrays of items**

```javascript
const chemists = people.filter((person) => person.profession === "chemist");
```

**Keeping list items in order with key**

- JSX elements directly **inside** a `map()` call **always** need keys
- `key` — a string or a number that **uniquely** identifies it among other items in that array
- Keys tell React which **array item** each component **corresponds** to, to make the **correct updates** to **the DOM tree** throughout its lifetime
- Important if array items get sorted, inserted, or deleted
- Generate Keys with [`let uuid = self.crypto.randomUUID();` method](https://developer.mozilla.org/en-US/docs/Web/API/Crypto/randomUUID) or [uuid](https://www.npmjs.com/package/uuid) npm package
- Keys must be unique among siblings.
- Can be the same keys for JSX nodes in different arrays.
- Dont change the keys
- **PERFORMANCE**: Don’t generate keys while rendering
- **PITFALL**: Array index as a key often leads to subtle and confusing bugs, default behavior if no key is specified
- **PITFALL**, **PERFORMANCE**: do not generate keys on the fly, e.g. with `key={Math.random()}` causes keys to never match up between renders, leading to all your components and DOM being recreated every time and loss of user input

## Event Handlers and Interactivity

- Event handlers are the best place for side effects

**Adding event handlers**

- You can add functions that will be **triggered in response to interactions** like clicking, hovering, focusing form inputs etc
- They are usually **defined inside** your components. `function handleClick() {alert('You clicked me!');}`
- If they are declared **inside** your component, they have **access** to your component’s **props**
- **Names** should that **start with handle**, followed by the name of the event. `onClick={handleClick}, onMouseEnter={handleMouseEnter}`

**Passing event handlers as props**

- They can be **passed as probs** `<button onClick={handleClick}>Click me</button>`
  - or inline `<button onClick={() => {alert('You clicked me!');}}>`
- **PITFALL**: Dont call the function `<button onClick={handleClick()}>` this will execute the function on every Render

**Naming event handler props**

- Built-in components like `<button>` and `<div>` only support **[browser event names](https://react.dev/reference/react-dom/components/common#common-props)**
- Your own components event handler props can be named any way that you like, by convention, props **should start with on**, followed by a capital letter. In case of multiple interactions name them for app-specific concepts like `onPlayMovie` and `onUploadImage` that gives flexibility how to trigger them

**Event propagation**

- Events bubble up the DOM from childeren to parents
- Event handlers will catch events from any children your component might have, the childrens will run first, followed by the parents handlers
- `<button onClick={(e) => alert(e.target.value)}>`
- **PITFALL**: All events propagate in React except onScroll, which only works on the JSX tag you attach it to.
- Use `e.stopPropagation();` to prevent an event from reaching parent components and firing their event handlers

**Stopping propagation**

```html
<button
  onClick={(e) => {
    e.stopPropagation();
    onClick();
  }}
>
  {children}
</button>
```

- In rare cases, you might need to catch all events on child elements, you can do this by adding `onClickCapture={() => {...}}>` to the parent (usefull for click analytics)
- **Preventing default behavior**

- For example some browser events have default behavior when a button inside a `<form>` is clicked, they will reload the whole page. You can call `e.preventDefault()` on the event object to stop this from happening:

## State and the **[`useState`](https://react.dev/reference/react/useState#setstate)** Hook

- State is private to the component. If you render it in two places, each copy gets its own state.
- Local variables and event handlers don’t persist re-renders. **Every render has its own event handlers and local variables** and changes to local variables won’t trigger re-renders
- **React keeps the state values “fixed” within one render’s event handlers**
- Use a state variable when a component needs to “remember” information between renders.
- [react state preservation behavior](https://gist.github.com/clemmy/b3ef00f9507909429d8aa0d3ee4f986b)

---

- State variables are declared by calling the useState Hook.`import { useState } from 'react';`
- The returns a pair of values: the current state and the function to update it: `const [index, setIndex] = useState(0);` (Array destructuring)
- **Convention** is to name this pair like const `[something, setSomething]`
- Hooks are special functions that start with use. They let you “hook into” React features like state.
- **PITFALL**: Hooks can **only be called at the top level** of your components or your own Hooks, need to be called unconditionally
- You can have more than one state variable. Internally, React matches them up by their order (stored in an array).

---

- The `set` function only updates the state variable for the next render. If you read the state variable after calling the set function, you will still get the old value that was on the screen before your call.
- **PITFALL** Calling the `set` function does not change the current state in the currently executing code
- If you do multiple updates within the same event, an updater function can be helpful `setAge(a => a + 1);`
- **Convention**: It’s common to name the updater function argument by the first letters of the corresponding state variable
- If the new value you provide is identical to the current `state` React will skip re-rendering the component and its children.
- In React, state is considered **read-only**, so you should **replace** it **rather** than **mutate** your existing objects `setForm({...form,firstName: 'Taylor'});`
- **React batches state updates**. It updates the screen after all the event handlers have run and have called their `set` functions. Use `flushSync` to force rerender
- Calling the `set` function during rendering is only allowed from within the currently rendering component.
- **NOTE**: If you call a set function while rendering, it must be inside a condition -
  ```javascript
  if (prevCount !== count) setPrevCount(count);
  ```

**Storing a Function**

```javascript
const [fn, setFn] = useState(() => someFunction);
const [index, setIndex] = useState(0); // Storing Data
```

**Initializer function**

```javascript
const [todos, setTodos] = useState(createInitialTodos);
```

**Setter functions**

```javascript
const [todos, setTodos] = useState(createInitialTodos());

// 🚩 Mistake: mutating state
setTodos((prevTodos) => {
  prevTodos.push(createTodo());
});

// ✅ Correct: replacing with new state
setTodos((prevTodos) => {
  return [...prevTodos, createTodo()];
});
```

## UseEffect

- a React Hook that lets you synchronize a component with an external system.

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

## Best Practice & Tipps

- It's good practice to put everything that can go outside of a component outside of it
- When possible, try to express your logic with rendering alone
- You should not mutate any of the inputs that your components (props, state, and context) use for rendering. To update the screen, “set” state instead of mutating preexisting objects.
- Make sure that you use the appropriate HTML tags for your event handlers. or example, to handle clicks, use `<button onClick={handleClick}>` instead of `<div onClick={handleClick}>` this enables built-in browser behaviors like keyboard navigation a different look can be achieved with CSS

**Keeping Components Pure**

- React assumes that every component you write is a pure function
- Keep components pure by **keeping changes out of the render phase**
- Components you write must always **return the same JSX given the same inputs**
- Components should only return their JSX, and **not change any objects** or variables that existed before rendering
- Each component should calculate JSX on their own and **not** attempt to coordinate with or depend upon others **during rendering**
- Use **Strict Mode** in which React calls each component’s function twice during development. to find mistakes in your components, it has has no effect in production
- React will never call your event handlers twice they are the best place for side effects
- Strive to express your component’s logic in the JSX you return. When you need to “change things”, you’ll usually want side effects in an event handler thats defined inside your component, but does not run during rendering. As a last resort, you can `useEffect`

**Performance with pure functions**

- improve performance by skipping rendering components whose inputs have not changed
  - `memo` lets you skip re-rendering a component when its props are unchanged. If the sam e inpute produces the same output
- Rendering can happen at any time, so components should not depend on each others’ rendering sequence. If there are no Sideeffects React can restart rendering without wasting time to finish the outdated render

**Render and Commit**

- Any screen update in a React app happens in three steps:
  - Trigger
  - Render
  - Commit
- You can use Strict Mode to find mistakes in your components
- React does not touch the DOM if the rendering result is the same as last time

## How To's

### Importing Images

An option would be to first import the image as such: `import logo from './logo.jpeg';` or `const logo = require('./logo.jpeg'); // with require` then plug it in: `<img src={logo} />`

```javascript
import defaultAvatar from "../../assets/defaultAvatar.svg";

export default function ContactCard() {
  return (
    <div className="ContactCard">
      <img src={defaultAvatar} alt="" />
    </div>
  );
}
```

### How to pass a parameter to an event handler or callback?

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

### Using Array in State

```javascript
import { useState } from "react";
import AddTodo from "./AddTodo.js";
import TaskList from "./TaskList.js";

let nextId = 3;
const initialTodos = [
  { id: 0, title: "Buy milk", done: true },
  { id: 1, title: "Eat tacos", done: false },
  { id: 2, title: "Brew tea", done: false },
];

export default function TaskApp() {
  const [todos, setTodos] = useState(initialTodos);

  function handleAddTodo(title) {
    setTodos([
      ...todos,
      {
        id: nextId++,
        title: title,
        done: false,
      },
    ]);
  }

  function handleChangeTodo(nextTodo) {
    setTodos(
      todos.map((t) => {
        if (t.id === nextTodo.id) {
          return nextTodo;
        } else {
          return t;
        }
      })
    );
  }

  function handleDeleteTodo(todoId) {
    setTodos(todos.filter((t) => t.id !== todoId));
  }

  return (
    <>
      <AddTodo onAddTodo={handleAddTodo} />
      <TaskList
        todos={todos}
        onChangeTodo={handleChangeTodo}
        onDeleteTodo={handleDeleteTodo}
      />
    </>
  );
}
``;
```

### [Storing information from previous renders](https://react.dev/reference/react/useState#storing-information-from-previous-renders)

```javascript
import { useState } from "react";
import CountLabel from "./CountLabel.js";

export default function App() {
  const [count, setCount] = useState(0);
  return (
    <>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
      <CountLabel count={count} />
    </>
  );
}

function CountLabel({ count }) {
  const [prevCount, setPrevCount] = useState(count);
  const [trend, setTrend] = useState(null);
  if (prevCount !== count) {
    setPrevCount(count);
    setTrend(count > prevCount ? "increasing" : "decreasing");
  }
  return (
    <>
      <h1>{count}</h1>
      {trend && <p>The count is {trend}</p>}
    </>
  );
}
```
