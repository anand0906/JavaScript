# JavaScript Scope, this, and use strict - Complete Guide

## Table of Contents

### Scope
1. [What is Scope?](#what-is-scope)
2. [Types of Scope](#types-of-scope)
3. [Global Scope](#global-scope)
4. [Function Scope](#function-scope)
5. [Block Scope](#block-scope)
6. [Lexical Scope](#lexical-scope)
7. [Scope Chain](#scope-chain)

### The `this` Keyword
8. [What is `this`?](#what-is-this)
9. [Global Context `this`](#global-context-this)
10. [Function Context `this`](#function-context-this)
11. [Object Method `this`](#object-method-this)
12. [Arrow Functions and `this`](#arrow-functions-and-this)
13. [Binding `this`](#binding-this)
14. [Event Handlers and `this`](#event-handlers-and-this)

### Use Strict
15. [What is `use strict`?](#what-is-use-strict)
16. [How to Enable Strict Mode](#how-to-enable-strict-mode)
17. [Benefits of Strict Mode](#benefits-of-strict-mode)
18. [Strict Mode Restrictions](#strict-mode-restrictions)
19. [Strict Mode and `this`](#strict-mode-and-this)

### Practical Examples
20. [Real-world Examples](#real-world-examples)
21. [Common Mistakes](#common-mistakes)
22. [Best Practices](#best-practices)

---

## What is Scope?

**Scope** determines where variables can be accessed in your code. Think of scope like rooms in a house - you can access things in your current room and shared areas, but not private things in other rooms.

### Simple Analogy
Imagine a house with different rooms:
- **Global scope** = Living room (everyone can access)
- **Function scope** = Private bedroom (only you can access)
- **Block scope** = Walk-in closet (only accessible from the bedroom)

### Basic Example
```javascript
// Global scope - everyone can see this
var globalVariable = "I'm global!";

function myFunction() {
    // Function scope - only this function can see this
    var functionVariable = "I'm local to this function!";
    
    console.log(globalVariable);    // ✅ Can access global
    console.log(functionVariable); // ✅ Can access local
}

myFunction();
console.log(globalVariable);    // ✅ Can access global
// console.log(functionVariable); // ❌ Error! Can't access function scope
```

---

## Types of Scope

JavaScript has several types of scope:

1. **Global Scope** - Accessible everywhere
2. **Function Scope** - Accessible only within the function
3. **Block Scope** - Accessible only within the block (with `let` and `const`)
4. **Module Scope** - Accessible within the module

### Scope Hierarchy
```javascript
var global = "Global scope";

function outer() {
    var outerVar = "Outer function scope";
    
    function inner() {
        var innerVar = "Inner function scope";
        
        if (true) {
            let blockVar = "Block scope";
            
            // Can access all scopes from here
            console.log(global);    // ✅ Global
            console.log(outerVar);  // ✅ Outer function
            console.log(innerVar);  // ✅ Inner function
            console.log(blockVar);  // ✅ Block scope
        }
        
        // console.log(blockVar); // ❌ Error! Block scope not accessible
    }
    
    inner();
    // console.log(innerVar); // ❌ Error! Inner function scope not accessible
}

outer();
```

---

## Global Scope

Variables declared outside any function or block have global scope.

### Creating Global Variables
```javascript
// These are all global variables
var globalVar1 = "I'm global with var";
let globalVar2 = "I'm global with let";  
const globalVar3 = "I'm global with const";

// Functions are also global by default
function globalFunction() {
    return "I'm a global function";
}

// Accessing from anywhere
function testAccess() {
    console.log(globalVar1);     // Works
    console.log(globalVar2);     // Works  
    console.log(globalVar3);     // Works
    console.log(globalFunction()); // Works
}
```

### Global Object
In browsers, global variables become properties of `window` object:

```javascript
var browserGlobal = "Hello Browser";
console.log(window.browserGlobal); // "Hello Browser"

// But let and const don't!
let modernGlobal = "Modern Global";
console.log(window.modernGlobal); // undefined
```

### Avoiding Global Pollution
```javascript
// Bad - pollutes global scope
var userName = "Alice";
var userAge = 25;
var userEmail = "alice@example.com";

function processUser() {
    // Uses global variables
}

// Good - use namespacing
var UserApp = {
    data: {
        name: "Alice",
        age: 25,
        email: "alice@example.com"
    },
    
    processUser: function() {
        // Uses namespaced data
        console.log(this.data.name);
    }
};
```

---

## Function Scope

Variables declared inside a function are only accessible within that function.

### var Function Scope
```javascript
function functionScopeExample() {
    var functionScoped = "I'm function scoped";
    
    if (true) {
        var alsoFunctionScoped = "I'm also function scoped!";
        console.log(functionScoped); // ✅ Works
    }
    
    console.log(alsoFunctionScoped); // ✅ Works (var ignores block)
}

functionScopeExample();
// console.log(functionScoped); // ❌ Error! Not accessible outside
```

### Parameters are Function Scoped
```javascript
function greet(name, age) {
    // name and age are function scoped
    var greeting = `Hello ${name}, you are ${age} years old`;
    return greeting;
}

console.log(greet("Bob", 30)); // Works
// console.log(name); // ❌ Error! name is not accessible outside
```

### Nested Function Scope
```javascript
function outer(x) {
    var outerVar = "Outer";
    
    function inner(y) {
        var innerVar = "Inner";
        // Can access both outer and inner scope
        return outerVar + " " + innerVar + " " + x + " " + y;
    }
    
    return inner("World");
    // return innerVar; // ❌ Error! Can't access inner scope
}

console.log(outer("Hello")); // "Outer Inner Hello World"
```

---

## Block Scope

With `let` and `const`, variables can be scoped to blocks (anything between `{}`).

### let and const Block Scope
```javascript
function blockScopeExample() {
    var functionScoped = "Function scoped";
    
    if (true) {
        let blockScoped = "Block scoped with let";
        const alsoBlockScoped = "Block scoped with const";
        
        console.log(functionScoped);    // ✅ Can access function scope
        console.log(blockScoped);       // ✅ Can access current block
        console.log(alsoBlockScoped);   // ✅ Can access current block
    }
    
    console.log(functionScoped);        // ✅ Still accessible
    // console.log(blockScoped);        // ❌ Error! Block scope ended
    // console.log(alsoBlockScoped);    // ❌ Error! Block scope ended
}

blockScopeExample();
```

### Loop Block Scope
```javascript
// Problem with var
function varLoopProblem() {
    for (var i = 0; i < 3; i++) {
        setTimeout(function() {
            console.log("var i:", i); // Prints: 3, 3, 3
        }, 100);
    }
}

// Solution with let
function letLoopSolution() {
    for (let i = 0; i < 3; i++) {
        setTimeout(function() {
            console.log("let i:", i); // Prints: 0, 1, 2
        }, 100);
    }
}

varLoopProblem();
letLoopSolution();
```

### Different Block Types
```javascript
function differentBlocks() {
    // if block
    if (true) {
        let ifBlock = "If block variable";
        console.log(ifBlock); // ✅ Works
    }
    
    // for block
    for (let forBlock = 0; forBlock < 1; forBlock++) {
        console.log("For block:", forBlock); // ✅ Works
    }
    
    // while block
    {
        let standaloneBlock = "Standalone block";
        console.log(standaloneBlock); // ✅ Works
    }
    
    // Try to access outside blocks
    // console.log(ifBlock);         // ❌ Error!
    // console.log(forBlock);        // ❌ Error!
    // console.log(standaloneBlock); // ❌ Error!
}

differentBlocks();
```

---

## Lexical Scope

**Lexical scope** means inner functions have access to variables in their outer scope, determined by where they are written in the code.

### Basic Lexical Scope
```javascript
function outer() {
    var outerVariable = "I'm from outer function";
    
    function inner() {
        // Can access outer function's variables
        console.log(outerVariable); // "I'm from outer function"
    }
    
    inner();
}

outer();
```

### Nested Lexical Scope
```javascript
function grandparent() {
    var grandparentVar = "Grandparent";
    
    function parent() {
        var parentVar = "Parent";
        
        function child() {
            var childVar = "Child";
            
            // Child can access all ancestor scopes
            console.log(childVar);      // "Child"
            console.log(parentVar);     // "Parent"  
            console.log(grandparentVar); // "Grandparent"
        }
        
        child();
    }
    
    parent();
}

grandparent();
```

### Lexical Scope with Closures
```javascript
function createCounter() {
    let count = 0; // This variable is "closed over"
    
    return function() {
        count++; // Inner function remembers outer variable
        return count;
    };
}

const counter1 = createCounter();
const counter2 = createCounter();

console.log(counter1()); // 1
console.log(counter1()); // 2
console.log(counter2()); // 1 (separate closure)
console.log(counter1()); // 3
```

---

## Scope Chain

When JavaScript looks for a variable, it searches through the **scope chain** from innermost to outermost scope.

### How Scope Chain Works
```javascript
var global = "Global variable";

function level1() {
    var level1Var = "Level 1 variable";
    
    function level2() {
        var level2Var = "Level 2 variable";
        
        function level3() {
            var level3Var = "Level 3 variable";
            
            // JavaScript searches in this order:
            // 1. level3 scope
            // 2. level2 scope  
            // 3. level1 scope
            // 4. global scope
            
            console.log(level3Var); // Found in step 1
            console.log(level2Var); // Found in step 2
            console.log(level1Var); // Found in step 3
            console.log(global);    // Found in step 4
        }
        
        level3();
    }
    
    level2();
}

level1();
```

### Variable Shadowing
```javascript
var name = "Global Alice";

function outer() {
    var name = "Outer Bob"; // Shadows global name
    
    function inner() {
        var name = "Inner Charlie"; // Shadows outer name
        console.log(name); // "Inner Charlie"
    }
    
    inner();
    console.log(name); // "Outer Bob"
}

outer();
console.log(name); // "Global Alice"
```

### Scope Chain Example
```javascript
function scopeChainDemo() {
    var a = "Function a";
    
    if (true) {
        let a = "Block a"; // Shadows function a
        let b = "Block b";
        
        function innerFunc() {
            let c = "Inner c";
            
            // Scope chain lookup:
            console.log(c); // innerFunc scope
            console.log(b); // block scope
            console.log(a); // block scope (shadows function a)
        }
        
        innerFunc();
    }
    
    console.log(a); // "Function a" (block shadow doesn't affect this)
}

scopeChainDemo();
```

---

## What is `this`?

The `this` keyword refers to the object that is currently executing the function. Think of `this` as "who is calling this function right now?"

### Simple Analogy
Imagine you're at a party and someone asks "What's your name?" 
- If **you** are asked, `this` refers to **you**
- If **your friend** is asked, `this` refers to **your friend**
- The same question, but `this` changes based on who's being asked

### Basic Example
```javascript
const person = {
    name: "Alice",
    age: 30,
    
    introduce: function() {
        // 'this' refers to the person object
        console.log(`Hi, I'm ${this.name} and I'm ${this.age} years old.`);
    }
};

person.introduce(); // "Hi, I'm Alice and I'm 30 years old."
```

---

## Global Context `this`

In the global context, `this` refers to the global object.

### Browser Global `this`
```javascript
console.log(this); // Window object in browser

var globalVar = "I'm global";
this.anotherGlobal = "Me too!";

console.log(window.globalVar);     // "I'm global"
console.log(window.anotherGlobal); // "Me too!"
```

### Node.js Global `this`
```javascript
// In Node.js, global 'this' is different
console.log(this); // {} (empty object in Node.js modules)
console.log(global); // Global object in Node.js
```

### Global Function `this`
```javascript
function globalFunction() {
    console.log(this); // Window object (or global in Node.js)
}

globalFunction();

// Same as:
window.globalFunction(); // In browser
```

---

## Function Context `this`

In regular functions, `this` depends on how the function is called.

### Function Declaration `this`
```javascript
function regularFunction() {
    console.log("this in regular function:", this);
}

regularFunction(); // 'this' is global object (Window in browser)
```

### Method vs Function Call
```javascript
const obj = {
    name: "Alice",
    
    method: function() {
        console.log("In method, this.name is:", this.name);
    }
};

// Method call - 'this' is obj
obj.method(); // "In method, this.name is: Alice"

// Function call - 'this' is global object
const functionRef = obj.method;
functionRef(); // "In method, this.name is: undefined"
```

### Lost `this` Context
```javascript
const user = {
    name: "Bob",
    
    greet: function() {
        console.log(`Hello, I'm ${this.name}`);
    }
};

user.greet(); // "Hello, I'm Bob"

// Lost context!
const greetFunction = user.greet;
greetFunction(); // "Hello, I'm undefined" (this.name is undefined)

// Fix with bind
const boundGreet = user.greet.bind(user);
boundGreet(); // "Hello, I'm Bob"
```

---

## Object Method `this`

When a function is called as an object method, `this` refers to that object.

### Simple Object Method
```javascript
const calculator = {
    value: 0,
    
    add: function(num) {
        this.value += num;
        return this; // Return this for chaining
    },
    
    multiply: function(num) {
        this.value *= num;
        return this;
    },
    
    getValue: function() {
        return this.value;
    }
};

calculator.add(5).multiply(2);
console.log(calculator.getValue()); // 10
```

### Nested Objects
```javascript
const company = {
    name: "TechCorp",
    
    employee: {
        name: "Alice",
        
        introduce: function() {
            console.log(`I'm ${this.name}`); // 'this' refers to employee object
        }
    },
    
    introduce: function() {
        console.log(`Welcome to ${this.name}`); // 'this' refers to company object
    }
};

company.introduce();          // "Welcome to TechCorp"
company.employee.introduce(); // "I'm Alice"
```

### Constructor Functions
```javascript
function Person(name, age) {
    // 'this' refers to the new instance being created
    this.name = name;
    this.age = age;
    
    this.introduce = function() {
        console.log(`Hi, I'm ${this.name}, ${this.age} years old.`);
    };
}

const person1 = new Person("Alice", 30);
const person2 = new Person("Bob", 25);

person1.introduce(); // "Hi, I'm Alice, 30 years old."
person2.introduce(); // "Hi, I'm Bob, 25 years old."
```

---

## Arrow Functions and `this`

Arrow functions don't have their own `this` - they inherit `this` from the enclosing scope.

### Arrow Function `this` Behavior
```javascript
const obj = {
    name: "Alice",
    
    regularMethod: function() {
        console.log("Regular method this.name:", this.name);
        
        // Arrow function inherits 'this' from regularMethod
        const arrowFunction = () => {
            console.log("Arrow function this.name:", this.name);
        };
        
        arrowFunction();
    },
    
    arrowMethod: () => {
        // Arrow function as method - 'this' is global object!
        console.log("Arrow method this.name:", this.name); // undefined
    }
};

obj.regularMethod();
// Output:
// Regular method this.name: Alice
// Arrow function this.name: Alice

obj.arrowMethod();
// Output: Arrow method this.name: undefined
```

### Practical Arrow Function Example
```javascript
class Timer {
    constructor() {
        this.seconds = 0;
    }
    
    start() {
        // Arrow function preserves 'this' context
        setInterval(() => {
            this.seconds++;
            console.log(`Timer: ${this.seconds} seconds`);
        }, 1000);
    }
    
    startBroken() {
        // Regular function - 'this' context is lost!
        setInterval(function() {
            this.seconds++; // 'this' is not the Timer instance!
            console.log(`Broken timer: ${this.seconds} seconds`);
        }, 1000);
    }
}

const timer = new Timer();
timer.start(); // Works correctly

// const brokenTimer = new Timer();  
// brokenTimer.startBroken(); // Doesn't work as expected
```

### Event Handlers with Arrow Functions
```javascript
class ButtonHandler {
    constructor(element) {
        this.element = element;
        this.clickCount = 0;
        
        // Arrow function preserves 'this'
        this.element.addEventListener('click', () => {
            this.clickCount++;
            console.log(`Button clicked ${this.clickCount} times`);
        });
    }
    
    // Alternative with regular function and bind
    setupWithBind() {
        this.element.addEventListener('click', function() {
            this.clickCount++;
            console.log(`Button clicked ${this.clickCount} times`);
        }.bind(this));
    }
}
```

---

## Binding `this`

You can explicitly set what `this` refers to using `call`, `apply`, or `bind`.

### Using `call()`
```javascript
function introduce(greeting, punctuation) {
    console.log(`${greeting}, I'm ${this.name}${punctuation}`);
}

const person = { name: "Alice" };

// call(thisArg, arg1, arg2, ...)
introduce.call(person, "Hello", "!"); // "Hello, I'm Alice!"
introduce.call(person, "Hi", "."); // "Hi, I'm Alice."
```

### Using `apply()`
```javascript
function fullIntroduction(greeting, age, city) {
    console.log(`${greeting}, I'm ${this.name}, ${age} years old, from ${city}.`);
}

const person = { name: "Bob" };

// apply(thisArg, [arg1, arg2, ...])
fullIntroduction.apply(person, ["Hello", 30, "New York"]);
// "Hello, I'm Bob, 30 years old, from New York."
```

### Using `bind()`
```javascript
function greet() {
    console.log(`Hello, ${this.name}!`);
}

const person = { name: "Charlie" };

// bind() creates a new function with 'this' permanently bound
const boundGreet = greet.bind(person);
boundGreet(); // "Hello, Charlie!"

// bind() with arguments
function multiply(a, b) {
    return a * b;
}

const double = multiply.bind(null, 2); // First argument is always 2
console.log(double(5)); // 10
console.log(double(8)); // 16
```

### Partial Application with `bind()`
```javascript
function calculate(operation, a, b) {
    switch(operation) {
        case 'add': return a + b;
        case 'multiply': return a * b;
        case 'subtract': return a - b;
    }
}

// Create specialized functions
const add = calculate.bind(null, 'add');
const multiply = calculate.bind(null, 'multiply');

console.log(add(5, 3)); // 8
console.log(multiply(4, 6)); // 24

// Partial application of more arguments
const addFive = calculate.bind(null, 'add', 5);
console.log(addFive(10)); // 15
```

---

## Event Handlers and `this`

In event handlers, `this` usually refers to the element that triggered the event.

### DOM Event Handler `this`
```javascript
// HTML: <button id="myButton">Click me</button>

document.getElementById('myButton').addEventListener('click', function() {
    console.log(this); // The button element
    console.log(this.textContent); // "Click me"
    this.style.backgroundColor = 'blue';
});
```

### Object Method as Event Handler
```javascript
class ButtonController {
    constructor(buttonElement) {
        this.button = buttonElement;
        this.clickCount = 0;
        
        // Problem: 'this' will refer to button, not ButtonController
        this.button.addEventListener('click', this.handleClick);
        
        // Solution: bind the method
        this.button.addEventListener('click', this.handleClick.bind(this));
    }
    
    handleClick() {
        this.clickCount++; // 'this' refers to ButtonController
        console.log(`Button clicked ${this.clickCount} times`);
    }
}
```

### Arrow Functions in Event Handlers
```javascript
class ModernButtonController {
    constructor(buttonElement) {
        this.button = buttonElement;
        this.clickCount = 0;
        
        // Arrow function preserves 'this' context
        this.button.addEventListener('click', () => {
            this.clickCount++;
            console.log(`Modern button clicked ${this.clickCount} times`);
        });
    }
}
```

---

## What is `use strict`?

**Strict mode** is a way to opt into a restricted variant of JavaScript. It makes JavaScript more secure and helps catch common coding mistakes.

### Simple Analogy
Think of strict mode like driving with a strict instructor:
- **Normal mode**: Instructor lets you make mistakes
- **Strict mode**: Instructor stops you immediately when you do something wrong

### Basic Example
```javascript
"use strict";

// This would normally create a global variable
// In strict mode, it throws an error
// myVariable = "Hello"; // ReferenceError: myVariable is not defined

// Must declare variables properly
var myVariable = "Hello"; // ✅ This works
let anotherVariable = "World"; // ✅ This works too
```

---

## How to Enable Strict Mode

### Global Strict Mode
```javascript
"use strict";

// Entire file is in strict mode
function myFunction() {
    // This function is also in strict mode
    console.log("Strict mode enabled globally");
}

myFunction();
```

### Function-Level Strict Mode
```javascript
function normalFunction() {
    // This function is in normal mode
    myVar = "I can create globals!"; // Works (but bad practice)
}

function strictFunction() {
    "use strict";
    // Only this function is in strict mode
    // myVar = "No globals allowed!"; // Error!
    let myVar = "Proper declaration required";
}

normalFunction();
strictFunction();
```

### Module Strict Mode
```javascript
// ES6 modules are automatically in strict mode
export function moduleFunction() {
    // No need to declare "use strict" - it's automatic
    // myVar = "This would cause an error"; // Error!
    let myVar = "Proper declaration";
}
```

---

## Benefits of Strict Mode

### 1. Prevents Accidental Globals
```javascript
"use strict";

function createUser() {
    // Typo in variable name
    // userName = "Alice"; // Error! userName is not declared
    var userName = "Alice"; // ✅ Must declare properly
}
```

### 2. Eliminates Silent Errors
```javascript
"use strict";

// Deleting variables throws error
var myVar = "test";
// delete myVar; // SyntaxError: Delete of an unqualified identifier

// Assignment to non-writable property throws error
var obj = {};
Object.defineProperty(obj, "prop", { value: 10, writable: false });
// obj.prop = 20; // TypeError: Cannot assign to read only property
```

### 3. Prevents Duplicate Parameters
```javascript
"use strict";

// This would cause a syntax error in strict mode
/*
function duplicateParams(a, a, b) {
    return a + b; // SyntaxError: Duplicate parameter name
}
*/

function properParams(a, b, c) {
    return a + b + c; // ✅ Works fine
}
```

### 4. Secures `eval()`
```javascript
"use strict";

eval("var evalVar = 'Hello'");
// console.log(evalVar); // ReferenceError: evalVar is not defined

// In non-strict mode, evalVar would be accessible here
```

---

## Strict Mode Restrictions

### 1. Variables Must Be Declared
```javascript
"use strict";

// These cause errors:
// undeclaredVar = "Error!";
// for (undeclaredLoop = 0; undeclaredLoop < 5; undeclaredLoop++) {}

// Must do this instead:
var declaredVar = "Good!";
for (let declaredLoop = 0; declaredLoop < 5; declaredLoop++) {
    // Loop body
}
```

### 2. Cannot Delete Variables, Functions, or Arguments
```javascript
"use strict";

var myVar = "test";
function myFunc() {}

// These cause errors:
// delete myVar;  // SyntaxError
// delete myFunc; // SyntaxError

function testArgs(a) {
    // delete a; // SyntaxError: Delete of an unqualified identifier
}
```

### 3. Octal Literals Not Allowed
```javascript
"use strict";

// var octalNum = 077; // SyntaxError: Octal literals are not allowed
var decimalNum = 63;   // ✅ Use decimal instead
var hexNum = 0x3F;     // ✅ Hex is still allowed
```

### 4. Reserved Words Cannot Be Used as Variables
```javascript
"use strict";

// These cause errors:
// var implements = "error";
// var interface = "error";
// var package = "error";
// var private = "error";
// var protected = "error";
// var public = "error";
// var static = "error";

var myVariable = "good"; // ✅ Use proper identifiers
```

---

## Strict Mode and `this`

### Global Function `this` in Strict Mode
```javascript
function normalMode() {
    console.log(this); // Window object (or global)
}

function strictMode() {
    "use strict";
    console.log(this); // undefined
}

normalMode();  // Window {...}
strictMode();  // undefined
```

### Method Call `this` Behavior
```javascript
"use strict";

const obj = {
    name: "Alice",
    
    method: function() {
        console.log(this); // Still refers to obj
        console.log(this.name); // "Alice"
    }
};

obj.method(); // Works the same in strict mode

// But calling as function:
const methodRef = obj.method;
methodRef(); // this is undefined (not global object)
```

### Constructor Without `new`
```javascript
"use strict";

function Person(name) {
    this.name = name; // TypeError if called without 'new'
}

// These work:
const person1 = new Person("Alice"); // ✅ Correct usage

// This causes error in strict mode:
// const person2 = Person("Bob"); // TypeError: Cannot set property 'name' of undefined
```

---

