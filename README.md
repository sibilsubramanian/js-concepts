# Scope

A scope is a certain region of a program where a defined variable exist and can be recognized. Beyond that it cannot be recognized.
There are three type of scopes:
- Global scope
- Function scope
- Block scope


📢 NOTES: 

> `var` is function scoped

> `let` and `const` are block scoped

### Variable Shadowing

Variable shadowing occurs when a variable declared within a certain scope has the same name as a variable declared in an outer scope.

```javascript
let num = 10;

function printNum() {
  let num = 20;
  console.log(num);
}

console.log(num);
```

While shadowing a variable, it should not cross the boundary of the scope.

```javascript
let num = 10;

if(true) {
  var num = 20;
}
```
This is is known as Illegal Shadowing and it will give the error as ${\textsf{\color{orange}variable\ is\ already\ defined}}$.

### Declaration

- `var` can be declared as many times as we want
- `let` and `const` cannot be redeclared in the same scope
- `var` and `let` can be declared without initialization
- `const` cannot be declared without initialization
- `var` and `let` can be reinitialized
- `const` cannot be updated

### Hoisting

When a variable is declared in JavaScript, it gets hoisted to the top of its scope, meaning the declaration happens first regardless of where the actual code is.

📢 NOTES: 

> `var` variables are hoisted and initialized to `undefined`

>  `let` and `const` variables are hoisted but not initialized until the line they are declared. They are said to be hoisted to temporal dead zone. (i.e, they are in the scope but not yet declared)

# Functions

```javascript
function square(num) {
  return num * num;
}
```

This is known as a function declaration, a function definition or a function statement.

```javascript
const square = function(num) {
  return num * num;
}
```

When you store a function definition inside a variable, it is called a funtion expression.

In languages like JavaScript, functions can be treated as any other variables. Functions can be passed as arguments to other functions, can be returned by another function and can be assigned as values to a variable. Such functions are called first-class functions.


${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
(function (x) {
  return (function (y) {
    console.log(x);
  })(2);
})(1);
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i);
  }, i * 1000);
}
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
for (let i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log(i);
  }, i * 1000);
}
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
var num = 21;
var func = function() {
  console.log(num);
  var num = 11;
}

func();
```


📢 NOTES: 

> Unlike variables, function definitions get hoisted completely

### Parameters vs Arguments

A parameter is a variable that is listed in the function definition. It represents a value that the function expects to receive when it is called. Parameters are placeholders that define the type and name of the value that will be passed into the function.

```javascript
function addNumbers(num1, num2) {
  return num1 + num2;
}
```
In the example above, num1 and num2 are parameters of the addNumbers function.

An argument, on the other hand, is the actual value that is passed into a function when it is called. It is the concrete value that is assigned to a parameter.

```javascript
let result = addNumbers(5, 10);
```
In the example above, 5 and 10 are arguments that are passed as values to the addNumbers function.

### Spread vs Rest operators

- The spread operator, denoted by three consecutive dots (...), is primarily used for expanding iterables like arrays into individual elements. This operator allows us to efficiently merge, copy, or pass array elements to functions without explicitly iterating through them
- Spread Operator Use Cases
  - Combining arrays
  - Passing arguments to functions
  - Copying arrays
- While the spread operator expands elements, the rest operator condenses them into a single entity within function parameters or array destructuring. It collects remaining elements into a designated variable, facilitating flexible function definitions and array manipulation
- Rest Operator Use Cases
  - Handling variable-length function arguments
  - Array destructuring
 
📢 NOTES: 

> A rest parameter must be the last parameter in a function definition. This is because the rest parameter collects all the remaining arguments passed to the function, so it doesn't make sense to have any parameters after it.

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
const printData = (a, ...numbers, x, y) => {
  console.log(x, y);
};

printData(5, 6, 7, 8);
```

### Callback functions

A callback function is a function passed into another function as an argument, which is then invoked inside the outer function to complete some kind of routine or action.

There are two ways in which the callback may be called: synchronous and asynchronous. Synchronous callbacks are called immediately after the invocation of the outer function, with no intervening asynchronous tasks, while asynchronous callbacks are called at some point later, after an asynchronous operation has completed. Examples of synchronous callbacks include the callbacks passed to Array.prototype.map(), Array.prototype.forEach(), etc. Examples of asynchronous callbacks include the callbacks passed to setTimeout() and Promise.prototype.then().

### Arrow function vs Regular function

The ordinary way of declaring functions in JavaScript is to use the function keyword. 

```javascript
function sayHello(name) {
  return `Hello ${name}`;
}
```

Arrow functions were introduced with ECMAScript 6 (ES6). They give you a more concise way of defining functions in JavaScript.

```javascript
const sayHello = (name) => {
  return `Hello ${name}`;
};
```

- We can access all the arguments passed to a regular function using the `arguments` object. To access the arguments passed to an arrow function, we can use the rest parameter syntax (`...`).
- When a regular function has duplicate names in the parameters, the last parameter with the duplicate name will take precedence. But in "strict mode", using a duplicate named parameter will result in a syntax error. Arrow functions don't allow for the same parameter name to be used more than once in the parameter list. Doing so will result in a syntax error.
- Regular functions are hoisted to the top. And you can access and call them even before they are declared. Arrow functions, on the other hand, cannot be accessed before they are initialised.
- Regular functions have their own `this` context. And this is determined dynamically depending on how you call or execute the function. Arrow functions, on the other hand, do not have their own `this` context. Instead, they capture the `this` value from the surrounding lexical context in which the arrow function was created.
- For regular functions, you can create a new instance using the `new` keyword. And this sets the `this` value to the new instance you've created. For arrow functions, you cannot use them as constructors. This is because the value of `this` in arrow functions is lexically scoped – that is, determined by the surrounding execution context. This behaviour does not make them suitable to be used as constructors.

It's recommended to use regular function in any of the following cases:
1. when you need to use a constructor with the `new` keyword
2. when you need the `this` binding to be dynamically scoped
3. when you want to use the `arguments` object

And you can use arrow functions in any of the following cases:
1. when you want a more concise syntax for the function
2. when you need to maintain the lexical scope of `this`
3. for non-method functions (in most cases)

📢 NOTES: 

> In programming, a function is a block of reusable code that performs a certain task. Functions can take input arguments and return output values. On the other hand, a method is a function that is associated with an object in object-oriented programming. Methods are functions that are called on objects and can modify or access the object's properties.

# Closures

A closure is a JavaScript feature that allows a function to remember and access its lexical scope even when the function is executed outside that scope.

```javascript
function init() {
  var name = "Mozilla"; // name is a local variable created by init
  function displayName() {
    // displayName() is the inner function, that forms the closure
    console.log(name); // use variable declared in the parent function
  }
  displayName();
}

init();
```

📢 NOTES: 

> In JavaScript, a closure is created every time a function is created, at the function creation time.

### Lexical Scope

Lexical scoping describes how a parser resolves variable names when functions are nested. The word lexical refers to the fact that lexical scoping uses the location where a variable is declared within the source code to determine where that variable is available. Nested functions have access to variables declared in their outer scope.

### Why do we need closures?

- Closures makes it possible for functions to have private variables
- JavaScript closures are used to control what is and what isn't in the scope of a particular function
- Control which variables are shared with sibling functions
- Closures can be used for optimizing the runtime of a function

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
for (var i = 0; i < 5; i++) {
  function print(index) {
    setTimeout(function log() {
      console.log(index);
    }, index * 1000);
  }
  print(i);
}
```

### Creating a private counter using closure

```javascript
function counter() {
  let counter = 0;

  function add(increment) {
    counter += increment;
  }

  function get() {
    return `Counter = ${counter}`;
  }

  return { add, get };
}
```

### Module pattern

The module pattern uses an IIFE to encapsulate private variables and functions, exposing only a public interface. The module pattern is a design pattern used for improving the maintainability and reusability of the code by creating public and private access levels. The module pattern keeps the privacy of the state and organizes using closures. It protects the pieces from the global scope, avoiding possible errors and conflicts.

```javascript
const createSupplier = (function () {
  const name = "General Motors";
  const field = "automobile";

  return {
    name,
    field,
  };
})();

createSupplier.name;
createSupplier.field;
```

### Closures vs Scopes

- Closure refers to the ability of a function to retain access to variables from its lexical scope even after the scope has been closed
- Scope refers to the visibility and accessbility of variables within a specified context, such as global scope, function scope or block scope

# Objects

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
const result = (function (num) {
  delete num;
  return num;
})(5);

console.log(result);
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
const obj = {
  a: "one",
  b: "two",
  a: "three",
};

console.log(obj);
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
const a = {};

const b = {
  key: "b",
};

const c = {
  key: "c",
};

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
console.log([..."Akshai"]);
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
const user = {
  name: "Akshai",
  age: 28,
};

const admin = {
  admin: true,
  ...user,
};

console.log(admin);
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
const settings = {
  username: "Akshai",
  level: 19,
  health: 90,
};

const data = JSON.stringify(settings, ["level", "health"]);

console.log(data);
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => {
    return 2 * Math.PI * this.radius;
  },
};

console.log(shape.diameter());
console.log(shape.perimeter());
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
function getItems(fruitList, ...args, favouriteFruit) {
  return [...fruitList, ...args, favouriteFruit];
}

getItems(["banana", "apple"], "pear", "orange");
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
let welcome = {
  greeting: "Hello",
};

let temp;

temp = welcome;

welcome.greeting = "Hey you!";

console.log(temp.greeting);
```

${\textsf{\color{khaki}Guess\ the\ output}}$
```javascript
let person = {
  name: "Akshai",
};

const members = [person];

person = null;

console.log(members);
```
