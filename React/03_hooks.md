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
