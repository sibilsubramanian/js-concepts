# Scopes

A scope is a certain region of a program where a defined variable exist and can be recognized. Beyond that it cannot be recognized.
There are three type of scopes:
- Global scope
- Function scope
- Block scope


📢 NOTES: 

1. `var` is function scoped
2. `let` and `const` are block scoped

### Variable Shadowing

Variable shadowing occues when a variable declared within a certain scope has the same name as a variable declared in an outer scope.

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
This is is known as Illegal Shadowing and it will give the error as ${\color{orange}variable\ is\ already\ defined}$.

### Declaration

- `var` can be declared as many times as we want
- `let` and `const` cannot be redeclared in the same scope
- `var` and `let` can be declared without initialization
- `const` cannot be declared without initialization
- `var` and `let` can be reinitialized
- `const` cannot be updated

### Hoisting

When a variable is declared in Javascript, it gets hoisted to the top of its scope, meaning the declaration happens first regardless of where the actual code is.

📢 NOTES: 

1. `var` variables are hoisted and initialized to `undefined`
2. `let` and `const` variables are hoisted but not initialized until the line they are declared. They are said to be hoisted to temporal dead zone. (i.e, they are in the scope but not yet declared)
