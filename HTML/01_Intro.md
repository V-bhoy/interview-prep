## What is HTML?
- stands for HyperText Markup Language, foundation of web.
- standardized by W3C ensuring that browsers can interpret html consistently.
- Defines the structure of content on the webpage.
- works as a skeleton of the webpage using html elements
- follows tree-like hierarchy

## What is a web page?
- A web page is a document written primarily in HTML (HyperText Markup Language).
- To look good and be interactive, HTML is often combined with CSS and JS.

## How is a webpage executed?
- Browsers (Chrome, Firefox, Safari, Edge, etc.) are software programs that know how to interpret HTML, CSS, and JS.
- When you type a URL in the browser, it asks DNS to find the IP address of the domain.
- Browser sends a (http/https) request to that server for index.html. Server responds with the HTML file.
- Browser parses HTML line by line:
   - Builds the DOM (Document Object Model) → a tree-like structure of all elements.
   - If it sees a <link> → fetch CSS and apply styles (CSSOM).
   - If it sees a <script> → fetch and run JS (which can modify DOM or make network requests).
   - Combines DOM + CSSOM → Render Tree.
   - Browser’s rendering engine then paints pixels on your screen.
 
## What is a Website?
- A website = a collection of related web pages under the same domain.
- Usually static (just informational, less interactivity).
- Example: a company’s site with “About Us,” “Contact,” “Products” pages.

## What is a web application?
- A web application = a website that behaves like software with heavy interactivity.
- Runs in browser but feels like an application.
- Involves:
     - Backend (server, database, APIs).
	   - Frontend (HTML, CSS, JS, frameworks like React, Angular).
	   - Example: Gmail, Facebook, Amazon.
- The main difference is website is highly static while web application is highly dynamic in nature

## What is the importance of index.html?
- default name of website's homepage
- first page that user's see when visiting a website
- it is important for SEO
- serves as a fallback when no file is specified in url
- 

