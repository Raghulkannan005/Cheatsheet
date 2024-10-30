# JavaScript Revision

```javascript

- Number: `let num = 42;`
- String: `let str = "Hello";`
- Boolean: `let bool = true;`
- Undefined: `let undef;`
- Null: `let empty = null;`
- Symbol: `let sym = Symbol('description');`
- BigInt: `let bigNum = 1234567890123456789012345678901234567890n;`
```

## Arithmetic Operators

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

```javascript
&&  // Logical AND
||  // Logical OR
!   // Logical NOT
```

```javascript
=   // Simple assignment
+=  // Addition assignment
-=  // Subtraction assignment
*=  // Multiplication assignment
/=  // Division assignment
%=  // Modulus assignment
**= // Exponentiation assignment
```

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
