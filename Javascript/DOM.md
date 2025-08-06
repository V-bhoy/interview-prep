### Window Object
- it refers to an open window in the browser and it is automatically created by the browser
- it is a global object that has some defined properties and methods
- JS uses these properties and methods to interact with the browser
- example: console.log(), alert() are part of window object provided by the browser

### What is DOM?
- refers to Document Object Model
- When the web page is loaded, it is created by the browser
- a document object is created inside the window object where we can access all the html elements and other properties in our web page through JS
- its a tree like structure and each node in it, is treated as an object
- so the root node is window followed by document which is follwed by html and then it has 2 child nodes that's head and body etc.
- This is the heirarchy that is followed
- Through the document object, JS can manipulate html elements in response to the user events / after some specific operation dynamically at runtime.
- example: a toggle button changing the dark and light theme for a webpage.
- if we try to log the document object before the document/web page is loaded, it is null.

### How to access HTML elements?
- Through element id --> ```document.getElementById("myId")```
   - returns null if no element is present with given Id
- Through element class name --> ```document.getElementsByClassName("myClass")```
   - returns HTML collection similar to an array.
- Through element tag name  --> ```document.getElementsByTagName("p")```
   - returns HTML collection similar to an array.
- Through query selector -->
``` javascript
  1. document.querySelector("#myId")
  2. document.querySelector(".myClass")
  3. document.querySelector("p")
   - we can pass id / class / tag name in it
   - to pass id, we write # followed by id name
   - to pass class, we write . followed by class name
   - to pass tag name, we write tag name directly
```
   - it automatically detects and returns the first element found.
- Through query selector all -->
``` javascript
  1. document.querySelectorAll("#myId")
  2. document.querySelectorAll(".myClass")
  3. document.querySelectorAll("p")
   - we can pass id / class / tag name in it
   - to pass id, we write # followed by id name
   - to pass class, we write . followed by class name
   - to pass tag name, we write tag name directly
```
   - it automatically detects and returns all the element found in a NodeList similar to array.

### Properties of elements
**1. Tag Name**
     - returns the tag name of the node element
``` javascript
        const element = document.querySelector("#myId");
        console.log(element.tagName)
        o/p ---> 'BUTTON'
```
**2. Inner Text**
     - returns the text content of the element and all its children
``` javascript
       <div>
          <h3>Fruits</h3>
          <ul>
            <li>Mango</li>
            <li>Apple</li>
            <li>Orange</li>
          </ul>
        </div>
        const element = document.querySelector("div");
        console.log(element.innerText)
        o/p ---> 'Fruits\nMango\nApple\nOrange'
```
**3. Inner HTML**
     - returns the html content along with text content / plain text of the element and all its children
``` javascript
       <div>
          <h3>Fruits</h3>
          <ul>
            <li>Mango</li>
            <li>Apple</li>
            <li>Orange</li>
          </ul>
        </div>
        const element = document.querySelector("div");
        console.log(element.innerHTML)
        o/p ---> '\n<h3>Fruits<h3>\n <ul> \n <li>Mango</li>\n<li>Apple</li>\n<li>Orange</li>\n</ul>/n'
```
**4. Text Content**
     - returns the text content even for hidden elements
``` javascript
       <div style="visibility: hidden">
          <h3>Fruits</h3>
        </div>
        const element = document.querySelector("div");
        console.log(element.innerText) o/p ---> ''
        console.log(element.textContent) o/p ---> 'Fruits'
```
**5. First Child**
     - returns the first child node of parent element else return null
``` javascript
       <div>
          <h3>Fruits</h3>
        </div>
        const element = document.querySelector("div");
        console.log(element.firstChild) o/p ---> h3
```
**6. Last Child**
     - returns the last child node of parent element else return null
``` javascript
       <div>
          <h3>Fruits</h3>
        </div>
        const element = document.querySelector("div");
        console.log(element.lastChild) o/p ---> h3
```
**7. Children**
     - returns all child node of parent element in the form of HTML collection similar to array
``` javascript
       <div>
          <h3>Fruits</h3>
        </div>
        const element = document.querySelector("div");
        console.log(element.children) o/p ---> HTMLCollection(1) --> h3
```

### Type of nodes 
**1. Parent Node** - a node having at least one child 
**2. Child Node** - a node having a parent node
**3. Sibling Node** - nodes having same parent in the document object are sibling to each other
``` javascript
       <div>
          <h3>Fruits</h3>
          <ul>
            <li>Mango</li>
            <li>Apple</li>
            <li>Orange</li>
          </ul>
        </div>
       1. div --> parent node
          <h3>, <ul> --> child nodes for div element
          h3 and ul are sibling nodes to each other
       2. ul --> parent node
         <li> --> child nodes for ul element
          3 <li> nodes --> sibling to each other
```

### How to access attributes of an element ?
- using these methods on element.

**1. getAttribute(attributeName)** - fetches the attribute value
``` javascript
        <div id="box">
          <h3>Fruits</h3>
        </div>
        const element = document.querySelector("div");
        console.log(element.getAttribute("id") o/p ---> "box"
```
**2. setAttribute(attributeName, value)** - set/update the attribute value
``` javascript
        <div id="box">
          <h3>Fruits</h3>
        </div>
        const element = document.querySelector("div");
        element.setAttribute("id", "container"); 
```
**3. To access style attribute** - we use style attribute directly on element 
``` javascript
        <div id="box">
          <h3>Fruits</h3>
        </div>
        const div = document.querySelector("div");
        div.style.backgroundColor = "blue" // this applies on inline style that has highest priority
```
### How to create an element?
- using document.createElement(tagName) method.
- example: document.createElement("p")

### How to insert an element?
- using the following methods on node element.
- **1. node.append(element)**
   - adds at the end of the node
- **2. node.prepend(element)**
   - adds at the start of the node
- **3. node.before(element)**
   - adds before the node (outside)
- **4. node.after(element)**
   - adds after the node (outside)

### How to remove an element?
- using node.remove() method.
example: p.remove() --> the p node is removed that was a paragraph element

### What is appendChild()? What is the difference between append() and appendChild()?
- Adds a node (element) as the last child of a specified parent node.
- Syntax: parentNode.appendChild(childNode);
- append can included multiple nodes along with text, separated by comma
- appenChild allows only single node object as the argument
``` javascript
const container = document.getElementById('container');

const div1 = document.createElement('div');
div1.textContent = 'First';

const div2 = document.createElement('div');
div2.textContent = 'Second';

container.append(div1, " some text ", div2); // ✅ works

// ❌ This will throw error: container.appendChild(div1, div2);
// ✅ This is valid: container.appendChild(div1); (only one node at a time)
```
- append() returns undefined while appendChild returns the appended child node.
- NOTE: appendChild() moves the node if it’s already in the DOM.

### What is removeChild()? What is the difference between remove() and removeChild()?
- Removes a child node from the DOM. You must specify the exact node to remove.
- Syntax: parentNode.removeChild(childNode);
``` javascript
const container = document.getElementById("container");
const para = document.getElementById("para");
container.removeChild(para);
```
- NOTE: removeChild() will throw an error if the node is not a child of the parent.
- remove() is called on the node itself and returns undefined
- removeChild() is called on the parent node and returns the removed node

### What is classList? Why do we use it?
- it is a read-only property of an element that returns a live DOMTokenList of the class attributes of that element.
- It provides convenient methods to add, remove, toggle, and check for class names on an element.
``` javascript
<div id="myDiv" class="box red"></div>
const div = document.getElementById('myDiv');
console.log(div.classList); // 👉 DOMTokenList ["box", "red"]
1. div.classList.add('visible') - Adds one or more class names
2. div.classList.remove('red') - Removes one or more class names
3. div.classList.toggle('active') - Toggles a class on/off
4. div.classList.contains('box') → true - Checks if a class exists
5. div.classList.replace('red', 'blue') - div.classList.replace('red', 'blue')
6. div.classList.length → 2 - Returns number of classes
7. div.classList[0] → 'box' - Access individual class name by index
```
- toggle example
``` javascript
const button = document.querySelector("button");

button.addEventListener("click", () => {
  button.classList.toggle("active");
});
// This will add active class if it’s not present, and remove it if it is.
```
### Why Use classList Instead of className?
- ✅ classList is safe, efficient, and modular.
- ❌ className requires you to manipulate the whole string manually:
```
div.className += " new-class";  // Old way
```


  
