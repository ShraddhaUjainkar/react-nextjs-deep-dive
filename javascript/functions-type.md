# JavaScript Functions Reference Guide

This document outlines the primary ways to define and use functions in modern JavaScript, covering syntax, hoisting, and scope.

---

## 1. Function Declaration
A named function that is **hoisted**. This means the JavaScript engine "lifts" the definition to the top of the scope before execution.

```javascript
greet("Alice"); // Works due to hoisting

function greet(name) {
  console.log(`Hello, ${name}!`);
}
---
## 2.Function Expression
A function assigned to a variable. These are not hoisted, so they cannot be called before they are defined in the code.

JavaScript
const multiply = function(a, b) {
  return a * b;
};

console.log(multiply(5, 2)); // 10



Gemini said
I have updated the Markdown file to include the ES version for each type (ES5 vs. ES6+) and added a section for Async/Await, as that's the modern standard for handling asynchronous functions.

You can copy the code block below, paste it into a text editor, and save it as javascript_functions_guide.md.

Markdown
# JavaScript Functions: Modern Reference Guide

A comprehensive breakdown of function types, their ECMAScript (ES) versions, and behavioral differences.

---

## 1. Function Declaration
**Version:** ES1 (Standard since the beginning)  
**Hoisted:** Yes  
A named function that is loaded into memory before the code runs.

```javascript
greet("Gemini"); // Works!

function greet(name) {
  return `Hello, ${name}!`;
}
2. Function Expression
Version: ES1

Hoisted: No

A function assigned to a variable. It follows the same hoisting rules as the variable type used (var, let, or const).

JavaScript
const add = function(a, b) {
  return a + b;
};
3. Anonymous Function
Version: ES1

Hoisted: No

A function without a name. Often used as a one-time value for callbacks or event listeners.

JavaScript
setTimeout(function() {
  console.log("Executed after 1 second");
}, 1000);
4. Arrow Function
Version: ES6 (2015) Hoisted: No

Modern, concise syntax. Key difference: It does not have its own this context; it inherits this from the parent scope (Lexical Scoping).

JavaScript
const multiply = (a, b) => a * b;
5. IIFE (Immediately Invoked Function Expression)
Version: ES1 (Pattern-based)

Hoisted: No

A function that runs as soon as it is defined. Commonly used to create a private scope.

JavaScript
(function() {
  console.log("I run immediately!");
})();
6. Callback Function
Version: ES1 (Functional Programming Concept)

Hoisted: Depends on definition

A function passed into another function as an argument.

JavaScript
function finalTask(data) {
  console.log("Finished with: " + data);
}

function startTask(callback) {
  callback("Task Data");
}

startTask(finalTask);
7. Async/Await Functions
Version: ES8 (2017) Hoisted: No

Built on top of Promises to make asynchronous code look and behave like synchronous code.

JavaScript
async function fetchUser() {
  try {
    const response = await fetch('[https://api.example.com/user](https://api.example.com/user)');
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}
Cheat Sheet Table
Function Type	Version	Hoisted	this Binding
Declaration	ES1	Yes	Own this
Expression	ES1	No	Own this
Arrow	ES6	No	Lexical (Parent)
Async	ES8	No	Depends on type
