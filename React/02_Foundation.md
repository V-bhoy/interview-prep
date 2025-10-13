## What is React ?
- it is an open-source JS library
- used to build frontend web applications
- allows developers to build complex UI by breaking them down into smaller reusable pieces called components.
- used mainly for single page applications and is known for its efficiency, flexibility & reusability in creating interactive UI components.
- founded by facebook & current version is 19.

## Why React is used?
## What is Virtual DOM?
## What is Rexconciliation vs Rendering?
## What is the Diff Algorithm?
## What is React Fibre?

## What is JSX & Why is it used?
- JSX --> Javascript XML (syntax extenstion for javascript)
- it allows us to write html like code directly within javascript files.
- JSX makes the UI structure easier to read, write, and maintain with syntax highlighting and compile-time error checking.
- it defines the structure & layout of the react components that we build.
- Browsers don’t understand JSX directly. During the build process, JSX is transpiled by Babel into standard JavaScript calls like:
```
React.createElement('div', { className: 'header' }, 'Hello World');
```
- it is a solution over creating components using React.createElement, which becomes hard to read, maintain and debug in case of complex components.

## What is a React Element ?
- A React Element is the smallest building block of the Virtual DOM tree.
- It is a plain JavaScript object that describes what you want to see on the screen.
- It is a light-weight description of the DOM node React should eventually create and render.
```
const element = <h1 className="greet">Hello, world!</h1>;
React converts it (via Babel) into:
const element = React.createElement('h1', { className: 'greet' }, 'Hello, world!');
{
  type: 'h1',
  props: {
    className: 'greet',
    children: 'Hello, world!'
  }
}
```
- Once created, a React element cannot be changed. If the UI needs to update, React creates a new element and compares it to the previous one using the Virtual DOM diffing algorithm.

## What is React Component?
- it is a function or class that returns a piece of JSX which is then transpiled into React elements.
- it is reusable, independent piece of UI that React uses to build the whole application.
- Each component handles its own logic, UI, and state.
- It is easy to build complex UIs by combining smaller components and focuses more towards what should be seen on the UI while react looks at the updation part of the DOM by itself (declarative in nature).
- Each time it’s used, React calls that function to produce React Elements, which are then rendered into the Virtual DOM and finally into the real DOM.
- It is of 2 types --> functional component & class component.

## What do you mean by the state of a component?
- it refers to the current data of the component.
- this data that can change over time and affects how the component is rendered on the screen.
- When the state changes, React re-renders the component to update the UI.
- State should be immutable → never modify it directly (always use setter functions).
- In class components, state is managed using this.state and updated using this.setState().
- In functional component, useState() hook is used.

## What are props?
- read-only data that is passed from a parent component to a child component in React.
- You can pass values, functions, or even entire components as props.
- Props are immutable → A child component cannot modify props.
- Props make components reusable → You can use the same component with different data.
- Data flow is unidirectional → from parent → to child (never the opposite).
- We access props like a single object parameter in afunction component called props.
- In a class component, we use this.props to access the props in child component.
```
function Button({ onClick, label }) {
  return <button onClick={onClick}>{label}</button>;
}

function App() {
  const handleClick = () => alert("Button clicked!");
  return <Button label="Click Me" onClick={handleClick} />;
}
```
## What is the difference between state & props ?
- The state is owned & controlled by the component itself while props are controlled by the parent component.
- The state is mutable & managed within the component itself while props are immutable
- State is used to manage internal, changeable data of a  component while props are used to pass data from parent to child component.

## What is a class component in React?
- A Class Component is an ES6 class that:
   - Extends React.Component.
	 - Must have a render() method.
	 - Can hold state and lifecycle methods (like componentDidMount, componentDidUpdate, etc.).
   - Manages internal state via this.state.
   - Uses built-in methods like componentDidMount(), componentWillUnmount() called lifecycle methods.
   - More boilerplate and harder to read for small components.

```
import React from 'react';

class Welcome extends React.Component {
  constructor(props) {
    super(props);
    this.state = { message: "Hello Vaishali 👋" };
  }

  render() {
    return <h1>{this.state.message}</h1>;
  }
}

export default Welcome;
```


## What is a functional component in React?
- A Functional Component is a plain JavaScript function that returns JSX (React elements).
- It’s simpler, more readable, and easier to test.
- Uses React Hooks (useState, useEffect, etc.) to manage state and lifecycle.
- Originally stateless, but Hooks (React 16.8+) gave them state and side-effects.
- Cleaner and more declarative.
- Fully supported since React 16.8 (Hooks).
```
function App() { return <h1>Hello</h1>; }
```
## What is prop drilling?
- The process of passing props through multiple level of nested components is called prop drilling.
- This is just because a deeply nested component can access that data — even though the intermediate components don’t need it.
- Makes code hard to maintain and less readable.
- Causes unnecessary re-renders if props change.
- Makes component reusability difficult (since every component in the chain depends on certain props), increases complexity.

## What is a React Fragment & Why is it used?
- it is used to group multiple elements together without adding an extra HTML node in the DOM.
```
<React.Fragment>...</React.Fragment>
<>...</>
```
## What are propTypes?
- it defines the type of props a child component is expecting to receive from its parent component.

## In how many ways can you export/import resources from a JS module?
- Default import/export:
   - use it when you want to export something by default
   - only single export default can be done from a module
   - we can refer it by anything when importing it by default.
- Named import/export
   - used when multiple things needs to be exported from a JS module
   - named exports must be referred by exact same names while importing them.







