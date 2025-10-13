## What are hooks?
- special functions provided by React that allow functional components to manage its own state, lifecycle and other features.
- Before hooks, the functional components were stateless and were only used for rendering.

## What is useState hook?
- it allows functional components to manage state by declaring state variables, and provide a function to update them.
```
const [stateVariable, setStateFunction] = useState(initialValue);
•	stateVariable → holds the current value of the state.
•	setStateFunction → updates that value.
•	initialValue → the starting value of your state (can be number, string, object, array, etc.).
```
- Even when a component re-renders, React keeps the state value internally.
- Every time you call setState, React re-renders the component with the new value.
- Do not mutate state directly
```
count = count + 1;  // won’t re-render
setCount(count + 1);  // triggers re-render
```
- You can have multiple useState hooks in one component.
```
function Form() {
  const [name, setName] = useState("");
  const [age, setAge] = useState(0);

  return (
    <div>
      <input onChange={e => setName(e.target.value)} placeholder="Name" />
      <input onChange={e => setAge(e.target.value)} placeholder="Age" />
      <p>Hello {name}, you are {age} years old.</p>
    </div>
  );
}
```
- If your new state depends on the previous one, update the state using a callback function in the setState as it always points to the latest value of the state variable to avoid any race conditions
```
setCount(prevCount => prevCount + 1);
```
## What is use effect hook?
- it is used to perform side effects in functional components like -
   - fetching data from API.
   - subscribing to events.
   - setting up timers
   - manually manipulating the DOM.
- Before hooks, these were handled by lifecycle methods in class components (componentDidMount, componentDidUpdate, componentWillUnmount).
useEffect unifies all of these in functional components.
```
useEffect(() => {
  // Side effect logic
  return () => {
    // Cleanup (optional)
  };
}, [dependencies]);
Effect function → first argument, runs after first render
Cleanup function → optional, runs before unmounting or before the next effect
Dependency array → second argument, controls when the effect runs
no array → run after every render (not recommended)
```
- Component Did Mount (Run once)
```
import React, { useEffect } from "react";

function App() {
  useEffect(() => {
    console.log("Component mounted");
  }, []); // empty array → runs only once

  return <h1>Hello, Vaishali 👋</h1>;
}
```
- Component Did Update (Run on state/prop change)
```
import React, { useState, useEffect } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    console.log("Count changed:", count);
  }, [count]); // runs every time 'count' changes

  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```
- Example 3: Cleanup (like componentWillUnmount)
```
useEffect(() => {
  const timer = setInterval(() => {
    console.log("Tick");
  }, 1000);

  return () => clearInterval(timer); // cleanup on unmount
}, []);
```
