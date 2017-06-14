
# Front-end Job Interview Questions

This file contains a number of front-end interview questions that can be used when vetting potential candidates. It is by no means recommended to use every single question here on the same candidate (that would take hours). Choosing a few items from this list should help you vet the intended skills you require.

**Note:** Keep in mind that many of these questions are open-ended and could lead to interesting discussions that tell you more about the person's capabilities than a straight answer would.

## Table of Contents

  1. [JS Questions](#js-questions)
  2. [General Questions](#general-questions)
  3. [HTML Questions](#html-questions)
  4. [CSS Questions](#css-questions)
  5. [Testing Questions](#testing-questions)
  6. [Performance Questions](#performance-questions)
  7. [Network Questions](#network-questions)
  8. [Coding Questions](#coding-questions)
  9. [Fun Questions](#fun-questions)

## JS Questions:
---
### ----- Explain event delegation: ----- 
> DOM event delegation is a mechanism of responding to ui-events via a single common parent rather than each child, through the magic of event "bubbling" (aka event propagation).

```javascript
document.getElementById("parent-list").addEventListener("click", function(e) {
	// e.target is the clicked element!
	// If it was a list item
	if(e.target && e.target.nodeName == "LI") {
		// List item found!  Output the ID!
		console.log("List item ", e.target.id.replace("post-", ""), " was clicked!");
	}
});
```
* Regarding HTML, add an event listener (such as a click) to the parent element of similar children
* The event will "Bubble UP" when event (clicking) is triggered by the child element
* e.target will indicate which child element has been triggered, thus use an if/else if perform that specific task

[Blog Post about What is event Delegation](https://davidwalsh.name/event-delegate)

---
### ----- Explain how `this` works in JavaScript: ----- 
  * "This" refers to the **execution context**, or where (the scope) the code is currently executing
  * Four types of "this":
    * **Calling an Objects method**: when executing an objects method, the "this" keyword provides useful
    * **Constructor**: when using the NEW keyword, an object can set its own properties using "this"
    * **Function call or Global**: when refering to "this" it will reference the most global object, usually window
    * **Event Handler**:
      * An inline event handler will refer to the **window** object
      ```javascript
      <script type="text/javascript"> 
        function click_handler() { 
          alert(this); // alerts the window object 
        } 
      </script>
      <button id='thebutton' onclick='click_handler()'>Click me!</button>
      ```
      * However, adding an event with javascript "this" refers to the DOM element
      ```javascript
      <script type="text/javascript"> 
        function click_handler() { 
          alert(this); // alerts the button DOM node 
        } 
        
        function addhandler() { 
          document.getElementById('thebutton').onclick = click_handler; 
        } 
        
        window.onload = addhandler; 
      </script>
      <button id='thebutton'>Click me!</button>
      ```

  >In typical object-oriented programming, we need a way of identifying and referring to the object that we’re currently working with. "this" serves the purpose admirably, providing our objects the ability to examine themselves, and point at their own properties.
  
  [Article: What is scope and how does "this" work?](http://www.digital-web.com/articles/scope_in_javascript/)

---
### ----- Explain how prototypal inheritance works: -----
* Every object has a property called **prototype**
  * this is a pointer to another object
  * when setting a method protoype on an object, it puts that method on the pointer object
  * when invoking that method, it looks up the prototype chain, if it is not an object's property, it will look to the prototype object and invoke it with the context of "this" of the object
* **Regarding inheritance**
  * If an object is created, it inherits its protype methods from its parent. That way each new object does not need to have its own method. It can look up the prototype chain to the parent and use that method. It is VERY performant.


[Funfunfunction Video Series: The best explanation of prototypes](https://www.youtube.com/watch?v=GhbhD1HR5vk&index=1&list=PL0zVEGEvSaeHBZFy6Q8731rcwk0Gtuxub)

[Article explaining Prototypes](http://yehudakatz.com/2011/08/12/understanding-prototypes-in-javascript/)

---
### ----- What do you think of AMD vs CommonJS? -----

###### Common.js
```javascript
// Exporting --> note: no default export, will break
exports.myMethod = (word) => console.log(word)

// Now import the above into another folder
const importedMethods = require('./filename.js')
importedMethods.myMethod('Hello, World!') 
```
###### AMD - Asynchronous Module Defenition
```javascript
define(['dep1', 'dep2'], function (dep1, dep2) {

  //Define the module value by returning a value.
  return function () {};
});
```
* Simplicity: CommonJS
* Async: RequireJS (AMD) and Node (Better loading times)
* Note: Both seem to be on their way out, Node is now asynchronous and with SPA's becoming more popular webpack is on the rise opening the door for **ES6 modules**
* SystemJS? All-in-one

[Article: Common.js vs Require.js vs Node Modules vs SystemJS?](https://auth0.com/blog/javascript-module-systems-showdown/)

[Reddit: Is AMD dying?](https://www.reddit.com/r/javascript/comments/46sbd2/is_amd_requirejs_dying/)

---
### Explain why the following doesn't work as an IIFE: `function foo(){ }();`, What needs to be changed to properly make it an IIFE?
```javascript
function () {}; // just a declaration, so it cant be invoked
(function() {}); // expression, returns a function, so it can be invoked
(function() {})();
```

[Great answer and other ways to IIFE](https://stackoverflow.com/a/31911000/3109222)

---
### What's the difference between a variable that is: `null`, `undefined` or undeclared? How would you go about checking for any of these states?
--- **undeclared** ---
* doesn't use var keyword
* gets created on the window, operates in different space than declared
* find it, use strict mode

--- **undefined** ---
* variable that has not been defined yet, may have been defined
* when attempting to use a variable that is undefined it will throw an error; also use (typeof varname === "undefined")

-- **null** --
* variable has been declared, and set to null. points to location in memory, but there is nothing there

[Blog: Null vs Undefined vs undeclared](http://lucybain.com/blog/2014/null-undefined-undeclared/)



---
* What is a closure, and how/why would you use one?
* What's a typical use case for anonymous functions?
* How do you organize your code? (module pattern, classical inheritance?)
* What's the difference between host objects and native objects?
* Difference between: `function Person(){}`, `var person = Person()`, and `var person = new Person()`?
* What's the difference between `.call` and `.apply`?
* Explain `Function.prototype.bind`.
* When would you use `document.write()`?
* What's the difference between feature detection, feature inference, and using the UA string?
* Explain Ajax in as much detail as possible.
* What are the advantages and disadvantages of using Ajax?
* Explain how JSONP works (and how it's not really Ajax).
* Have you ever used JavaScript templating?
  * If so, what libraries have you used?
* Explain "hoisting".
* Describe event bubbling.
* What's the difference between an "attribute" and a "property"?
* Why is extending built-in JavaScript objects not a good idea?
* Difference between document load event and document DOMContentLoaded event?
* What is the difference between `==` and `===`?
* Explain the same-origin policy with regards to JavaScript.
* Make this work:
```javascript
duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]
```
* Why is it called a Ternary expression, what does the word "Ternary" indicate?
* What is `"use strict";`? what are the advantages and disadvantages to using it?
* Create a for loop that iterates up to `100` while outputting **"fizz"** at multiples of `3`, **"buzz"** at multiples of `5` and **"fizzbuzz"** at multiples of `3` and `5`
* Why is it, in general, a good idea to leave the global scope of a website as-is and never touch it?
* Why would you use something like the `load` event? Does this event have disadvantages? Do you know any alternatives, and why would you use those?
* Explain what a single page app is and how to make one SEO-friendly.
* What is the extent of your experience with Promises and/or their polyfills?
* What are the pros and cons of using Promises instead of callbacks?
* What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?
* What tools and techniques do you use debugging JavaScript code?
* What language constructions do you use for iterating over object properties and array items?
* Explain the difference between mutable and immutable objects.
  * What is an example of an immutable object in JavaScript?
  * What are the pros and cons of immutability?
  * How can you achieve immutability in your own code?
* Explain the difference between synchronous and asynchronous functions.
* What is event loop?
  * What is the difference between call stack and task queue?
* Explain the differences on the usage of `foo` between `function foo() {}` and `var foo = function() {}`


#### General Questions:

* What did you learn yesterday/this week?
* What excites or interests you about coding?
* What is a recent technical challenge you experienced and how did you solve it?
* What UI, Security, Performance, SEO, Maintainability or Technology considerations do you make while building a web application or site?
* Talk about your preferred development environment.
* Which version control systems are you familiar with?
* Can you describe your workflow when you create a web page?
* If you have 5 different stylesheets, how would you best integrate them into the site?
* Can you describe the difference between progressive enhancement and graceful degradation?
* How would you optimize a website's assets/resources?
* How many resources will a browser download from a given domain at a time?
  * What are the exceptions?
* Name 3 ways to decrease page load (perceived or actual load time).
* If you jumped on a project and they used tabs and you used spaces, what would you do?
* Describe how you would create a simple slideshow page.
* If you could master one technology this year, what would it be?
* Explain the importance of standards and standards bodies.
* What is Flash of Unstyled Content? How do you avoid FOUC?
* Explain what ARIA and screenreaders are, and how to make a website accessible.
* Explain some of the pros and cons for CSS animations versus JavaScript animations.
* What does CORS stand for and what issue does it address?

#### HTML Questions:

* What does a `doctype` do?
* What's the difference between full standards mode, almost standards mode and quirks mode?
* What's the difference between HTML and XHTML?
* Are there any problems with serving pages as `application/xhtml+xml`?
* How do you serve a page with content in multiple languages?
* What kind of things must you be wary of when design or developing for multilingual sites?
* What are `data-` attributes good for?
* Consider HTML5 as an open web platform. What are the building blocks of HTML5?
* Describe the difference between a `cookie`, `sessionStorage` and `localStorage`.
* Describe the difference between `<script>`, `<script async>` and `<script defer>`.
* Why is it generally a good idea to position CSS `<link>`s between `<head></head>` and JS `<script>`s just before `</body>`? Do you know any exceptions?
* What is progressive rendering?
* Have you used different HTML templating languages before?

#### CSS Questions:

* What is the difference between classes and IDs in CSS?
* What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?
* Describe Floats and how they work.
* Describe z-index and how stacking context is formed.
* Describe BFC(Block Formatting Context) and how it works.
* What are the various clearing techniques and which is appropriate for what context?
* Explain CSS sprites, and how you would implement them on a page or site.
* What are your favourite image replacement techniques and which do you use when?
* How would you approach fixing browser-specific styling issues?
* How do you serve your pages for feature-constrained browsers?
  * What techniques/processes do you use?
* What are the different ways to visually hide content (and make it available only for screen readers)?
* Have you ever used a grid system, and if so, what do you prefer?
* Have you used or implemented media queries or mobile specific layouts/CSS?
* Are you familiar with styling SVG?
* How do you optimize your webpages for print?
* What are some of the "gotchas" for writing efficient CSS?
* What are the advantages/disadvantages of using CSS preprocessors?
  * Describe what you like and dislike about the CSS preprocessors you have used.
* How would you implement a web design comp that uses non-standard fonts?
* Explain how a browser determines what elements match a CSS selector.
* Describe pseudo-elements and discuss what they are used for.
* Explain your understanding of the box model and how you would tell the browser in CSS to render your layout in different box models.
* What does ```* { box-sizing: border-box; }``` do? What are its advantages?
* List as many values for the display property that you can remember.
* What's the difference between inline and inline-block?
* What's the difference between a relative, fixed, absolute and statically positioned element?
* The 'C' in CSS stands for Cascading.  How is priority determined in assigning styles (a few examples)?  How can you use this system to your advantage?
* What existing CSS frameworks have you used locally, or in production? How would you change/improve them?
* Have you played around with the new CSS Flexbox or Grid specs?
* How is responsive design different from adaptive design?
* Have you ever worked with retina graphics? If so, when and what techniques did you use?
* Is there any reason you'd want to use `translate()` instead of *absolute positioning*, or vice-versa? And why?

#### Testing Questions:

* What are some advantages/disadvantages to testing your code?
* What tools would you use to test your code's functionality?
* What is the difference between a unit test and a functional/integration test?
* What is the purpose of a code style linting tool?

#### Performance Questions:

* What tools would you use to find a performance bug in your code?
* What are some ways you may improve your website's scrolling performance?
* Explain the difference between layout, painting and compositing.

#### Network Questions:

* Traditionally, why has it been better to serve site assets from multiple domains?
* Do your best to describe the process from the time you type in a website's URL to it finishing loading on your screen.
* What are the differences between Long-Polling, Websockets and Server-Sent Events?
* Explain the following request and response headers:
  * Diff. between Expires, Date, Age and If-Modified-...
  * Do Not Track
  * Cache-Control
  * Transfer-Encoding
  * ETag
  * X-Frame-Options
* What are HTTP methods? List all HTTP methods that you know, and explain them.

#### Coding Questions:

*Question: What is the value of `foo`?*
```javascript
var foo = 10 + '20';
```

*Question: How would you make this work?*
```javascript
add(2, 5); // 7
add(2)(5); // 7
```

*Question: What value is returned from the following statement?*
```javascript
"i'm a lasagna hog".split("").reverse().join("");
```

*Question: What is the value of `window.foo`?*
```javascript
( window.foo || ( window.foo = "bar" ) );
```

*Question: What is the outcome of the two alerts below?*
```javascript
var foo = "Hello";
(function() {
  var bar = " World";
  alert(foo + bar);
})();
alert(foo + bar);
```

*Question: What is the value of `foo.length`?*
```javascript
var foo = [];
foo.push(1);
foo.push(2);
```

*Question: What is the value of `foo.x`?*
```javascript
var foo = {n: 1};
var bar = foo;
foo.x = foo = {n: 2};
```

*Question: What does the following code print?*
```javascript
console.log('one');
setTimeout(function() {
  console.log('two');
}, 0);
console.log('three');
```

#### Fun Questions:

* What's a cool project that you've recently worked on?
* What are some things you like about the developer tools you use?
* Who inspires you in the front-end community?
* Do you have any pet projects? What kind?
* What's your favorite feature of Internet Explorer?
* How do you like your coffee?


#### Contributors:

This document started in 2009 as a collaboration of [@paul_irish](https://twitter.com/paul_irish) [@bentruyman](https://twitter.com/bentruyman) [@cowboy](https://twitter.com/cowboy) [@ajpiano](https://twitter.com/ajpiano)  [@SlexAxton](https://twitter.com/slexaxton) [@boazsender](https://twitter.com/boazsender) [@miketaylr](https://twitter.com/miketaylr) [@vladikoff](https://twitter.com/vladikoff) [@gf3](https://twitter.com/gf3) [@jon_neal](https://twitter.com/jon_neal) [@sambreed](https://twitter.com/sambreed) and [@iansym](https://twitter.com/iansym).

It has since received contributions from over [100 developers](https://github.com/h5bp/Front-end-Developer-Interview-Questions/graphs/contributors).
