# JavaScript Cheatsheet

## Table of Contents
1. [Variables and Data Types](#variables-and-data-types)
2. [Operators](#operators)
3. [Control Structures](#control-structures)
4. [Functions](#functions)
5. [Objects and Object-Oriented Programming](#objects-and-object-oriented-programming)
6. [Arrays and Array Methods](#arrays-and-array-methods)
7. [String Methods](#string-methods)
8. [ES6+ Features](#es6-features)
9. [Asynchronous JavaScript](#asynchronous-javascript)
10. [DOM Manipulation](#dom-manipulation)
11. [Error Handling](#error-handling)
12. [Modules](#modules)
13. [Regular Expressions](#regular-expressions)
14. [Best Practices and Tips](#best-practices-and-tips)

## Variables and Data Types

### Variable Declaration
```javascript
var x = 5;         // Function-scoped (avoid using)
let y = 10;        // Block-scoped
const z = 15;      // Block-scoped, cannot be reassigned
```

### Data Types
- Number: `let num = 42;`
- String: `let str = "Hello";`
- Boolean: `let bool = true;`
- Undefined: `let undef;`
- Null: `let empty = null;`
- Symbol: `let sym = Symbol('description');`
- BigInt: `let bigNum = 1234567890123456789012345678901234567890n;`

### Type Checking
```javascript
typeof variable;   // Returns a string indicating the type
```

## Operators

### Arithmetic Operators
```javascript
+   // Addition
-   // Subtraction
*   // Multiplication
/   // Division
%   // Modulus (remainder)
**  // Exponentiation (ES6)
++  // Increment
--  // Decrement
```

### Comparison Operators
```javascript
==  // Equal to (value)
=== // Strict equal to (value and type)
!=  // Not equal to
!== // Strict not equal to
>   // Greater than
<   // Less than
>=  // Greater than or equal to
<=  // Less than or equal to
```

### Logical Operators
```javascript
&&  // Logical AND
||  // Logical OR
!   // Logical NOT
```

### Assignment Operators
```javascript
=   // Simple assignment
+=  // Addition assignment
-=  // Subtraction assignment
*=  // Multiplication assignment
/=  // Division assignment
%=  // Modulus assignment
**= // Exponentiation assignment
```

### Ternary Operator
```javascript
condition ? expressionIfTrue : expressionIfFalse;
```

## Control Structures

### If-Else Statement
```javascript
if (condition) {
    // code block
} else if (anotherCondition) {
    // code block
} else {
    // code block
}
```

### Switch Statement
```javascript
switch (expression) {
    case value1:
        // code block
        break;
    case value2:
        // code block
        break;
    default:
        // code block
}
```

### For Loop
```javascript
for (let i = 0; i < 5; i++) {
    // code block
}
```

### While Loop
```javascript
while (condition) {
    // code block
}
```

### Do-While Loop
```javascript
do {
    // code block
} while (condition);
```

### For...of Loop (ES6)
```javascript
for (let item of iterable) {
    // code block
}
```

### For...in Loop
```javascript
for (let key in object) {
    // code block
}
```

## Functions

### Function Declaration
```javascript
function functionName(parameter1, parameter2) {
    // code block
    return result;
}
```

### Function Expression
```javascript
const functionName = function(parameter1, parameter2) {
    // code block
    return result;
};
```

### Arrow Function (ES6)
```javascript
const functionName = (parameter1, parameter2) => {
    // code block
    return result;
};

// Short syntax for single expression
const square = x => x * x;
```

### Default Parameters (ES6)
```javascript
function greet(name = "Guest") {
    return `Hello, ${name}!`;
}
```

### Rest Parameters (ES6)
```javascript
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}
```

### Callback Functions
```javascript
function doSomething(callback) {
    // code block
    callback();
}

doSomething(() => {
    console.log("Callback executed");
});
```

## Objects and Object-Oriented Programming

### Object Literal
```javascript
const person = {
    name: "John",
    age: 30,
    greet: function() {
        console.log(`Hello, my name is ${this.name}`);
    }
};
```

### Constructor Function
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.greet = function() {
    console.log(`Hello, my name is ${this.name}`);
};

const john = new Person("John", 30);
```

### Class Declaration (ES6)
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        console.log(`Hello, my name is ${this.name}`);
    }
}

const john = new Person("John", 30);
```

### Inheritance (ES6)
```javascript
class Employee extends Person {
    constructor(name, age, job) {
        super(name, age);
        this.job = job;
    }

    work() {
        console.log(`${this.name} is working as a ${this.job}`);
    }
}
```

### Getters and Setters
```javascript
class Circle {
    constructor(radius) {
        this._radius = radius;
    }

    get radius() {
        return this._radius;
    }

    set radius(value) {
        if (value > 0) {
            this._radius = value;
        }
    }

    get area() {
        return Math.PI * this._radius ** 2;
    }
}
```

## Arrays and Array Methods

### Array Creation
```javascript
const arr1 = [1, 2, 3, 4, 5];
const arr2 = new Array(1, 2, 3, 4, 5);
const arr3 = Array.from("Hello");  // ['H', 'e', 'l', 'l', 'o']
```

### Array Methods
```javascript
// Adding/Removing Elements
arr.push(element);       // Add to end
arr.pop();               // Remove from end
arr.unshift(element);    // Add to beginning
arr.shift();             // Remove from beginning
arr.splice(start, deleteCount, item1, item2, ...);  // Add/remove elements

// Iterating
arr.forEach(callback);   // Execute callback for each element
arr.map(callback);       // Create new array with results of callback
arr.filter(callback);    // Create new array with elements that pass test
arr.reduce(callback, initialValue);  // Reduce array to single value

// Searching
arr.indexOf(element);    // Find index of element
arr.find(callback);      // Find first element that satisfies condition
arr.findIndex(callback); // Find index of first element that satisfies condition
arr.includes(element);   // Check if array includes element

// Transforming
arr.slice(start, end);   // Extract a portion of the array
arr.concat(arr2, arr3);  // Merge arrays
arr.join(separator);     // Join elements into string

// Sorting
arr.sort(compareFunction);  // Sort elements in place
arr.reverse();              // Reverse order of elements
```

## String Methods

```javascript
str.length;              // String length
str.charAt(index);       // Character at index
str.charCodeAt(index);   // Unicode of character at index
str.concat(str2, str3);  // Concatenate strings
str.includes(searchString);  // Check if string contains substring
str.indexOf(searchValue);    // Find index of first occurrence
str.lastIndexOf(searchValue);  // Find index of last occurrence
str.match(regexp);       // Match against regular expression
str.replace(searchValue, replaceValue);  // Replace substring
str.slice(start, end);   // Extract a portion of the string
str.split(separator);    // Split string into array
str.toLowerCase();       // Convert to lowercase
str.toUpperCase();       // Convert to uppercase
str.trim();              // Remove whitespace from both ends
```

## ES6+ Features

### Template Literals
```javascript
const name = "John";
console.log(`Hello, ${name}!`);
```

### Destructuring Assignment
```javascript
// Array destructuring
const [a, b] = [1, 2];

// Object destructuring
const { name, age } = person;
```

### Spread Operator
```javascript
const arr1 = [1, 2, 3];
const arr2 = [...arr1, 4, 5];  // [1, 2, 3, 4, 5]

const obj1 = { a: 1, b: 2 };
const obj2 = { ...obj1, c: 3 };  // { a: 1, b: 2, c: 3 }
```

### Object Property Shorthand
```javascript
const name = "John";
const age = 30;
const person = { name, age };  // { name: "John", age: 30 }
```

### Promise
```javascript
const promise = new Promise((resolve, reject) => {
    // Asynchronous operation
    if (/* operation successful */) {
        resolve(result);
    } else {
        reject(error);
    }
});

promise.then(result => {
    // Handle success
}).catch(error => {
    // Handle error
});
```

### Async/Await
```javascript
async function fetchData() {
    try {
        const response = await fetch(url);
        const data = await response.json();
        return data;
    } catch (error) {
        console.error("Error:", error);
    }
}
```

## Asynchronous JavaScript

### Callbacks
```javascript
function fetchData(callback) {
    setTimeout(() => {
        const data = { id: 1, name: "John" };
        callback(null, data);
    }, 1000);
}

fetchData((error, data) => {
    if (error) {
        console.error("Error:", error);
    } else {
        console.log("Data:", data);
    }
});
```

### Promises
```javascript
function fetchData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const data = { id: 1, name: "John" };
            resolve(data);
        }, 1000);
    });
}

fetchData()
    .then(data => console.log("Data:", data))
    .catch(error => console.error("Error:", error));
```

### Async/Await
```javascript
async function fetchData() {
    try {
        const response = await fetch(url);
        const data = await response.json();
        console.log("Data:", data);
    } catch (error) {
        console.error("Error:", error);
    }
}

fetchData();
```

## DOM Manipulation

### Selecting Elements
```javascript
document.getElementById("id");
document.getElementsByClassName("class");
document.getElementsByTagName("tag");
document.querySelector("selector");
document.querySelectorAll("selector");
```

### Modifying Elements
```javascript
element.innerHTML = "New content";
element.textContent = "New text";
element.setAttribute("attribute", "value");
element.style.property = "value";
```

### Creating and Removing Elements
```javascript
const newElement = document.createElement("div");
parentElement.appendChild(newElement);
parentElement.removeChild(childElement);
element.remove();
```

### Event Handling
```javascript
element.addEventListener("click", function(event) {
    // Event handler
});

element.removeEventListener("click", handler);
```

## Error Handling

### Try-Catch Statement
```javascript
try {
    // Code that may throw an error
} catch (error) {
    // Handle the error
} finally {
    // Always executed
}
```

### Throwing Custom Errors
```javascript
throw new Error("Custom error message");
```

## Modules

### Exporting
```javascript
// Named exports
export const name = "John";
export function greet() { /* ... */ }

// Default export
export default function() { /* ... */ }
```

### Importing
```javascript
// Named imports
import { name, greet } from "./module.js";

// Default import
import myFunction from "./module.js";

// Importing everything
import * as myModule from "./module.js";
```

## Regular Expressions

### Creating Regular Expressions
```javascript
const regex1 = /pattern/;
const regex2 = new RegExp("pattern");
```

### Regular Expression Methods
```javascript
regex.test(str);     // Returns true if pattern matches
str.match(regex);    // Returns an array of matches
str.replace(regex, replacement);  // Replace matches with replacement
```

## Best Practices and Tips

1. Use `const` for variables that won't be reassigned, and `let` for those that will.
2. Always use strict equality (`===`) instead of loose equality (`==`).
3. Use meaningful and descriptive names for variables and functions.
4. Keep functions small and focused on a single task.
5. Use arrow functions for short, simple functions and callbacks.
6. Avoid global variables and functions.
7. Use template literals for string interpolation.
8. Use destructuring assignment to extract values from objects and arrays.
9. Use the spread operator for array manipulation and function arguments.
10. Use promises or async/await for asynchronous operations instead of nested callbacks.
11. Always handle errors in asynchronous code.
12. Use modern JavaScript features (ES6+) when possible, but be aware of browser compatibility.
13. Comment your code, but focus on explaining "why" rather than "what".
14. Use consistent code formatting and follow a style guide.
15. Write modular code and use ES6 modules for better organization.
