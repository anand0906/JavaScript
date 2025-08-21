# JavaScript Execution Context and Hoisting - Complete Guide

## Table of Contents
1. [What is Execution Context?](#what-is-execution-context)
2. [Types of Execution Context](#types-of-execution-context)
3. [How Execution Context Works](#how-execution-context-works)
4. [Call Stack](#call-stack)
5. [Creation Phase vs Execution Phase](#creation-phase-vs-execution-phase)
6. [What is Hoisting?](#what-is-hoisting)
7. [Variable Hoisting](#variable-hoisting)
8. [Function Hoisting](#function-hoisting)
9. [Let and Const Hoisting](#let-and-const-hoisting)
10. [Temporal Dead Zone](#temporal-dead-zone)
11. [Class Hoisting](#class-hoisting)
12. [Best Practices](#best-practices)
13. [Common Mistakes](#common-mistakes)
14. [Practical Examples](#practical-examples)

---

## What is Execution Context?

**Execution Context** is like a "container" or "environment" where JavaScript code is evaluated and executed. Think of it as a box that holds all the information needed to run a piece of code.

### Simple Analogy
Imagine you're a chef cooking in a kitchen:
- The **kitchen** is the execution context
- The **ingredients** are your variables
- The **recipes** are your functions
- The **cooking process** is the code execution

### What's Inside an Execution Context?
Every execution context contains:
1. **Variable Environment** - Where variables are stored
2. **Lexical Environment** - Where variables and their scope are managed
3. **This Binding** - What `this` refers to

### Basic Example
```javascript
// Global Execution Context is created
var name = "Alice";  // Variable stored in context
var age = 25;        // Variable stored in context

function greet() {   // Function stored in context
    // New Function Execution Context is created when called
    console.log("Hello, " + name);
}

greet(); // Function is executed
```

---

## Types of Execution Context

### 1. Global Execution Context (GEC)
The default context where your code starts running.

```javascript
// This all happens in Global Execution Context
var globalVar = "I'm global!";
let globalLet = "Me too!";
const globalConst = "Same here!";

function globalFunction() {
    return "I'm a global function";
}

console.log("This runs in global context");
```

**Characteristics:**
- Created when JavaScript file loads
- Only one per JavaScript program
- Creates global object (`window` in browser, `global` in Node.js)
- Sets `this` to global object

### 2. Function Execution Context (FEC)
Created every time a function is called.

```javascript
function outerFunction() {
    // New Function Execution Context created
    var outerVar = "I'm outer";
    
    function innerFunction() {
        // Another Function Execution Context created
        var innerVar = "I'm inner";
        console.log(outerVar); // Can access outer context
    }
    
    innerFunction();
}

outerFunction();
```

**Characteristics:**
- Created each time function is called
- Can access variables from parent context
- Has its own `this` binding
- Destroyed when function finishes

### 3. Eval Execution Context
Created when code runs inside `eval()` function (rarely used).

```javascript
// Don't use eval() in real code - it's dangerous!
eval("var evalVar = 'Hello from eval'");
console.log(evalVar); // Works but not recommended
```

---

## How Execution Context Works

### Step-by-Step Process

```javascript
var x = 10;

function multiply(a, b) {
    var result = a * b;
    return result;
}

var answer = multiply(5, 3);
console.log(answer);
```

**What happens:**

1. **Global Execution Context Created**
   - `x` is allocated memory
   - `multiply` is stored as function
   - `answer` is allocated memory

2. **Global Code Executes**
   - `x = 10`
   - `multiply(5, 3)` is called

3. **Function Execution Context Created**
   - Parameters `a = 5`, `b = 3`
   - `result` is allocated memory
   - Function code executes

4. **Function Returns**
   - Function context is destroyed
   - Return value assigned to `answer`

5. **Continue Global Execution**
   - `console.log(answer)` executes

---

## Call Stack

The **Call Stack** keeps track of execution contexts. It works like a stack of plates - last in, first out.

### Visualizing Call Stack
```javascript
function first() {
    console.log("First function start");
    second();
    console.log("First function end");
}

function second() {
    console.log("Second function start");
    third();
    console.log("Second function end");
}

function third() {
    console.log("Third function");
}

first();
```

**Call Stack Changes:**
```
Step 1: [Global Context]
Step 2: [Global Context, first()]
Step 3: [Global Context, first(), second()]
Step 4: [Global Context, first(), second(), third()]
Step 5: [Global Context, first(), second()]  // third() finished
Step 6: [Global Context, first()]            // second() finished
Step 7: [Global Context]                     // first() finished
```

### Stack Overflow Example
```javascript
function recursiveFunction() {
    console.log("Calling myself");
    recursiveFunction(); // Calls itself forever
}

// recursiveFunction(); // Don't run this - it causes stack overflow!
```

**Better Recursive Function:**
```javascript
function betterRecursion(count) {
    if (count <= 0) {
        return "Done!"; // Base case prevents infinite recursion
    }
    
    console.log("Count:", count);
    return betterRecursion(count - 1);
}

betterRecursion(3);
// Output: Count: 3, Count: 2, Count: 1, Done!
```

---

## Creation Phase vs Execution Phase

Every execution context is created in two phases:

### Creation Phase
Variables and functions are set up in memory (but not executed yet).

```javascript
console.log(typeof myVar);      // "undefined" (not error!)
console.log(typeof myFunction); // "function"

var myVar = "Hello World";
function myFunction() {
    return "I'm a function";
}
```

**What happens in Creation Phase:**
1. Create Variable Environment
2. Create Lexical Environment  
3. Set up `this` binding
4. Allocate memory for variables (set to `undefined`)
5. Store function declarations

### Execution Phase
Code runs line by line.

```javascript
// Creation phase already happened above
console.log(myVar);      // "Hello World"
console.log(myFunction()); // "I'm a function"
```

### Detailed Example
```javascript
function example() {
    // Creation Phase:
    // - a: undefined
    // - b: undefined  
    // - innerFunc: function object stored
    
    console.log("a:", a); // undefined (not error)
    console.log("b:", b); // undefined (not error)
    console.log("c:", c); // ReferenceError: c is not defined
    
    var a = 1;
    var b = 2;
    
    function innerFunc() {
        return "Inner function";
    }
    
    // Execution Phase:
    console.log("a:", a); // 1
    console.log("b:", b); // 2
    console.log(innerFunc()); // "Inner function"
}

example();
```

---

## What is Hoisting?

**Hoisting** is JavaScript's behavior of moving variable and function declarations to the top of their scope during the creation phase. It's like the declarations are "lifted up" to the top.

### Important Note
- Only **declarations** are hoisted, not **initializations**
- It's not physically moving code - it's how JavaScript's engine works internally

### Basic Example
```javascript
// What you write:
console.log(myVar); // undefined (not error!)
var myVar = 5;

// How JavaScript "sees" it internally:
var myVar; // Declaration hoisted to top
console.log(myVar); // undefined
myVar = 5; // Initialization stays in place
```

---

## Variable Hoisting

### var Hoisting
Variables declared with `var` are hoisted and initialized with `undefined`.

```javascript
console.log("Before declaration:", x); // undefined

var x = 10;

console.log("After declaration:", x); // 10

// This is equivalent to:
// var x;
// console.log("Before declaration:", x); // undefined
// x = 10;
// console.log("After declaration:", x); // 10
```

### Multiple var Declarations
```javascript
console.log(a, b, c); // undefined undefined undefined

var a = 1;
var b = 2;
var c = 3;

console.log(a, b, c); // 1 2 3
```

### var in Functions
```javascript
function varExample() {
    console.log("Start:", myVar); // undefined
    
    if (true) {
        var myVar = "Hello";
        console.log("Inside if:", myVar); // "Hello"
    }
    
    console.log("End:", myVar); // "Hello"
}

// This is how JavaScript sees it:
function varExample() {
    var myVar; // Hoisted to function top
    console.log("Start:", myVar); // undefined
    
    if (true) {
        myVar = "Hello"; // Assignment happens here
        console.log("Inside if:", myVar); // "Hello"
    }
    
    console.log("End:", myVar); // "Hello"
}

varExample();
```

---

## Function Hoisting

### Function Declaration Hoisting
Function declarations are completely hoisted - you can call them before they're defined.

```javascript
// This works!
sayHello(); // "Hello, World!"

function sayHello() {
    console.log("Hello, World!");
}

// Multiple function calls
greet("Alice"); // "Hello, Alice!"
greet("Bob");   // "Hello, Bob!"

function greet(name) {
    console.log("Hello, " + name + "!");
}
```

### Function Expression Hoisting
Function expressions follow `var` hoisting rules.

```javascript
// This doesn't work!
// sayGoodbye(); // TypeError: sayGoodbye is not a function

var sayGoodbye = function() {
    console.log("Goodbye!");
};

// Now it works
sayGoodbye(); // "Goodbye!"

// This is how JavaScript sees it:
var sayGoodbye; // undefined
// sayGoodbye(); // TypeError: undefined is not a function
sayGoodbye = function() {
    console.log("Goodbye!");
};
sayGoodbye(); // "Goodbye!"
```

### Arrow Function Hoisting
Arrow functions also follow `var` hoisting rules (if assigned to `var`).

```javascript
// This doesn't work!
// greetArrow(); // TypeError: greetArrow is not a function

var greetArrow = () => {
    console.log("Hello from arrow!");
};

greetArrow(); // Works now
```

### Function Declaration vs Expression
```javascript
// Declaration - works everywhere in its scope
console.log(add(2, 3)); // 5

function add(a, b) {
    return a + b;
}

// Expression - only works after assignment
// console.log(multiply(2, 3)); // TypeError

var multiply = function(a, b) {
    return a * b;
};

console.log(multiply(2, 3)); // 6
```

---

## Let and Const Hoisting

### The Truth About let and const
`let` and `const` ARE hoisted, but they're not initialized. They exist in a "Temporal Dead Zone."

```javascript
console.log(typeof myVar); // undefined (var)
// console.log(typeof myLet); // ReferenceError!

var myVar = "I'm var";
let myLet = "I'm let";
```

### let Hoisting Example
```javascript
function letExample() {
    // console.log(x); // ReferenceError: Cannot access 'x' before initialization
    
    let x = 10;
    console.log(x); // 10
}

letExample();

// JavaScript sees this as:
function letExample() {
    // let x; // Hoisted but in Temporal Dead Zone
    // console.log(x); // ReferenceError
    
    x = 10; // Initialization
    console.log(x); // 10
}
```

### const Hoisting Example
```javascript
function constExample() {
    // console.log(y); // ReferenceError: Cannot access 'y' before initialization
    
    const y = 20;
    console.log(y); // 20
}

constExample();
```

### Block Scope with let and const
```javascript
function blockScopeExample() {
    console.log("Start");
    
    if (true) {
        // console.log(blockVar); // ReferenceError
        let blockVar = "I'm block scoped";
        console.log(blockVar); // "I'm block scoped"
    }
    
    // console.log(blockVar); // ReferenceError: blockVar is not defined
    console.log("End");
}

blockScopeExample();
```

---

## Temporal Dead Zone

The **Temporal Dead Zone (TDZ)** is the period between the creation of a `let` or `const` variable and its initialization.

### Understanding TDZ
```javascript
function tdzExample() {
    // TDZ starts here for 'x'
    console.log("Before declaration");
    
    // console.log(x); // ReferenceError: Cannot access 'x' before initialization
    
    let x = 10; // TDZ ends here
    console.log(x); // 10 - works fine
}

tdzExample();
```

### TDZ in Different Scopes
```javascript
let globalVar = "Global";

function tdzScopes() {
    // TDZ for localVar starts here
    console.log(globalVar); // "Global" - works fine
    
    // console.log(localVar); // ReferenceError
    
    let localVar = "Local";
    console.log(localVar); // "Local" - works fine
}

tdzScopes();
```

### TDZ with Function Parameters
```javascript
function tdzWithParams(a = b, b = 2) {
    // ReferenceError: Cannot access 'b' before initialization
    return [a, b];
}

// tdzWithParams(); // Error!

// This works:
function fixedParams(a = 1, b = a + 1) {
    return [a, b];
}

console.log(fixedParams()); // [1, 2]
```

### typeof and TDZ
```javascript
// With var
console.log(typeof varVariable); // "undefined"
var varVariable = "Hello";

// With let
// console.log(typeof letVariable); // ReferenceError!
let letVariable = "World";

// Outside of scope
console.log(typeof nonExistent); // "undefined"
```

---

## Class Hoisting

Classes are hoisted but remain in the Temporal Dead Zone like `let` and `const`.

```javascript
// This doesn't work!
// const obj = new MyClass(); // ReferenceError

class MyClass {
    constructor(name) {
        this.name = name;
    }
    
    greet() {
        return `Hello, ${this.name}!`;
    }
}

// Now it works
const obj = new MyClass("Alice");
console.log(obj.greet()); // "Hello, Alice!"
```

### Class Expression Hoisting
```javascript
// This doesn't work either!
// const instance = new MyClassExpression(); // TypeError

var MyClassExpression = class {
    constructor() {
        this.message = "Hello from class expression";
    }
};

// Now it works
const instance = new MyClassExpression();
console.log(instance.message);
```

---

## Best Practices

### 1. Declare Variables at the Top
```javascript
// Good practice
function goodExample() {
    var name, age, email; // Declare all vars at top
    
    name = "Alice";
    age = 25;
    email = "alice@example.com";
    
    return { name, age, email };
}
```

### 2. Use let and const Instead of var
```javascript
// Better - use let and const
function modernExample() {
    const name = "Bob";        // Won't change
    let age = 30;             // Might change
    
    if (age >= 18) {
        let message = "Adult";  // Block scoped
        console.log(message);
    }
    
    return { name, age };
}
```

### 3. Declare Functions Before Use
```javascript
// Good practice - even though hoisting allows it
function calculate() {
    // Declare functions at top of scope
    function add(a, b) {
        return a + b;
    }
    
    function multiply(a, b) {
        return a * b;
    }
    
    // Use functions
    const sum = add(5, 3);
    const product = multiply(sum, 2);
    
    return product;
}
```

### 4. Use Function Expressions for Conditional Functions
```javascript
function conditionalFunctions(useAdvanced) {
    let processor;
    
    if (useAdvanced) {
        processor = function(data) {
            // Advanced processing
            return data.map(item => item * 2).filter(item => item > 10);
        };
    } else {
        processor = function(data) {
            // Simple processing
            return data;
        };
    }
    
    return processor;
}
```

---

## Common Mistakes

### 1. Assuming var is Block Scoped
```javascript
// Mistake
function varMistake() {
    for (var i = 0; i < 3; i++) {
        setTimeout(() => {
            console.log(i); // Prints 3, 3, 3 (not 0, 1, 2)
        }, 100);
    }
}

// Fix with let
function letFix() {
    for (let i = 0; i < 3; i++) {
        setTimeout(() => {
            console.log(i); // Prints 0, 1, 2
        }, 100);
    }
}
```

### 2. Relying on Hoisting
```javascript
// Bad - hard to understand
function confusing() {
    console.log(mystery()); // What does this print?
    
    var x = 10;
    
    function mystery() {
        return x;
    }
}

// Good - clear and obvious
function clear() {
    var x = 10;
    
    function mystery() {
        return x;
    }
    
    console.log(mystery()); // Obviously prints 10
}
```

### 3. Temporal Dead Zone Confusion
```javascript
// Mistake
function tdzMistake() {
    console.log(typeof myVar); // undefined
    console.log(typeof myLet); // ReferenceError!
    
    var myVar = "Hello";
    let myLet = "World";
}

// Better
function tdzFixed() {
    var myVar = "Hello";
    let myLet = "World";
    
    console.log(typeof myVar); // "string"
    console.log(typeof myLet); // "string"
}
```

---

## Practical Examples

### 1. Understanding Variable Hoisting in Loops
```javascript
// Problem with var
function problemExample() {
    var functions = [];
    
    for (var i = 0; i < 3; i++) {
        functions.push(function() {
            return i; // All functions return 3!
        });
    }
    
    return functions;
}

const funcs = problemExample();
console.log(funcs[0]()); // 3
console.log(funcs[1]()); // 3
console.log(funcs[2]()); // 3

// Solution with let
function solutionExample() {
    var functions = [];
    
    for (let i = 0; i < 3; i++) {
        functions.push(function() {
            return i; // Each function captures its own i
        });
    }
    
    return functions;
}

const fixedFuncs = solutionExample();
console.log(fixedFuncs[0]()); // 0
console.log(fixedFuncs[1]()); // 1
console.log(fixedFuncs[2]()); // 2
```

### 2. Function Hoisting in Conditional Blocks
```javascript
// Unexpected behavior
function conditionalHoisting() {
    console.log(typeof myFunc); // "function"
    
    if (false) {
        function myFunc() {
            return "I'm declared in false block";
        }
    }
    
    // myFunc is still hoisted!
}

// Better approach
function betterConditional(condition) {
    let myFunc;
    
    if (condition) {
        myFunc = function() {
            return "I'm conditionally assigned";
        };
    } else {
        myFunc = function() {
            return "I'm the else function";
        };
    }
    
    return myFunc();
}

console.log(betterConditional(true));  // "I'm conditionally assigned"
console.log(betterConditional(false)); // "I'm the else function"
```

### 3. Module Pattern with Hoisting
```javascript
const myModule = (function() {
    // Private variables (hoisted)
    var privateVar = "I'm private";
    var privateCounter = 0;
    
    // Private functions (hoisted)
    function privateFunction() {
        console.log("Private function called");
        privateCounter++;
    }
    
    // Public interface
    return {
        getPrivateVar: function() {
            return privateVar;
        },
        
        callPrivateFunction: function() {
            privateFunction();
            return privateCounter;
        },
        
        reset: function() {
            privateCounter = 0;
        }
    };
})();

console.log(myModule.getPrivateVar()); // "I'm private"
console.log(myModule.callPrivateFunction()); // 1
console.log(myModule.callPrivateFunction()); // 2
myModule.reset();
console.log(myModule.callPrivateFunction()); // 1
```

### 4. Debugging Hoisting Issues
```javascript
function debugExample() {
    console.log("=== Debug Hoisting ===");
    
    // Check what's available at the start
    console.log("typeof varDecl:", typeof varDecl);
    console.log("typeof funcDecl:", typeof funcDecl);
    // console.log("typeof letDecl:", typeof letDecl); // ReferenceError
    
    // Declarations
    var varDecl = "I'm var";
    let letDecl = "I'm let";
    const constDecl = "I'm const";
    
    function funcDecl() {
        return "I'm a function declaration";
    }
    
    var funcExpr = function() {
        return "I'm a function expression";
    };
    
    // Check after declarations
    console.log("varDecl:", varDecl);
    console.log("letDecl:", letDecl);
    console.log("constDecl:", constDecl);
    console.log("funcDecl():", funcDecl());
    console.log("funcExpr():", funcExpr());
}

debugExample();
```

---

## Summary

### Execution Context
- **Container** where JavaScript code runs
- **Types**: Global, Function, Eval
- **Phases**: Creation (setup) and Execution (run code)
- **Call Stack** manages multiple contexts

### Hoisting
- **Declarations** are moved to top of scope during creation phase
- **var**: Hoisted and initialized with `undefined`
- **let/const**: Hoisted but in Temporal Dead Zone
- **Functions**: Declarations fully hoisted, expressions follow variable rules

### Key Takeaways
1. **Understand** how JavaScript engine works internally
2. **Declare** variables at the top of their scope
3. **Use** `let` and `const` instead of `var`
4. **Don't rely** on hoisting - write clear, readable code
5. **Be aware** of Temporal Dead Zone with `let` and `const`

### Mental Model
Think of JavaScript execution as:
1. **Setup Phase** (Creation): Reserve memory for variables and functions
2. **Execution Phase**: Run code line by line using reserved memory
3. **Call Stack**: Keep track of where you are in nested function calls

Understanding these concepts will help you:
- **Debug** confusing behavior
- **Write** more predictable code
- **Avoid** common pitfalls
- **Understand** how JavaScript really works

---

*Happy coding! 🚀*
