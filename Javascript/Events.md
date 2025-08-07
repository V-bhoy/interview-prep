### What are events?
- Events are actions or occurrences that happen in the browser like button clicl
- Events are fired to trigger some important operations in our code of execution which can arise from user interactions.
- Each event is represented an object which JS can listen and execute function in response through event listeners.
Example: mouse events, keyboard events, form events, print events etc.

### Common types of events 
1. click - User clicks an element
2. dblclick - User double-clicks an element
3. mouseover - Mouse hovers over an element
4. mouseout - Mouse leaves the element
5. keydown - Key is pressed down
6. keyup - Key is released
7. submit - Form is submitted
8. change - Input element changes (e.g. select)
9. input - Input content changes in real-time
10. load - Page or image finishes loading
11. scroll - Page or element is scrolled

###  Ways to Attach Event Listeners
**1. Inline HTML**
``` javascript
<button onclick="sayHello()">Click Me</button>
```
**2. Using DOM in JS**
``` javascript
const btn = document.querySelector("button");

btn.onclick = function () {
  alert("Button clicked!");
};
// JS handling has more priority than inline handling
```
**3.  addEventListener() (Best Practice)**
- it takes type of event and a callback function which is an event handler
``` javascript
btn.addEventListener("click", () => {
  alert("Clicked with addEventListener");
});
```
### NOTE:
- JavaScript automatically passes an event object to the event handler which has all the metadata about the event:
``` javascript
button.addEventListener("click", function(event) {
  console.log(event);         // Info about the click
  console.log(event.target);  // Element that was clicked
});
```
-  Removing an Event
-  the callback reference should be same to remove
``` javascript
function greet() {
  console.log("Hi!");
  button.removeEventListener("click", greet);
}
button.addEventListener("click", greet);
```
### Why is it important to remove an event listener
- ```btn.addEventListener("click", handleClick)```
- The function handleClick becomes a closure, which closes over the btn element and any variables in its lexical scope.
- Even if you remove the DOM element (btn.remove()), the event listener still holds a reference to it through the closure.
- This prevents garbage collection of btn and its scope variables, causing a memory leak.
- In Single Page Applications (SPA), components and elements are frequently added/removed without full page reloads.
- If event listeners are not properly cleaned up:
    - Memory keeps growing.
    - Performance degrades.
    - Unexpected bugs or duplicate event triggers may occur.
- Correct cleanup:
``` javascript
btn.removeEventListener("click", handleClick);
btn.remove();
```


