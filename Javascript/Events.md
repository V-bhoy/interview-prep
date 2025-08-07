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
```
**3.  addEventListener() (Best Practice)**
``` javascript
btn.addEventListener("click", () => {
  alert("Clicked with addEventListener");
});
```
### NOTE:
- JavaScript automatically passes an event object to the event handler:
``` javascript
button.addEventListener("click", function(event) {
  console.log(event);         // Info about the click
  console.log(event.target);  // Element that was clicked
});
```
-  Removing an Event
``` javascript
function greet() {
  console.log("Hi!");
  button.removeEventListener("click", greet);
}
button.addEventListener("click", greet);
```

