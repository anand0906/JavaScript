# JavaScript Functions - Complete Guide (A to Z)

## Table of Contents
1. [What are Functions?](#what-are-functions)
2. [Why Use Functions?](#why-use-functions)
3. [Function Declaration](#function-declaration)
4. [Function Expression](#function-expression)
5. [Arrow Functions](#arrow-functions)
6. [Parameters and Arguments](#parameters-and-arguments)
7. [Return Values](#return-values)
8. [Function Scope](#function-scope)
9. [Hoisting](#hoisting)
10. [Anonymous Functions](#anonymous-functions)
11. [Callback Functions](#callback-functions)
12. [Higher-Order Functions](#higher-order-functions)
13. [IIFE (Immediately Invoked Function Expression)](#iife-immediately-invoked-function-expression)
14. [Closure](#closure)
15. [Function Methods](#function-methods)
16. [Rest Parameters](#rest-parameters)
17. [Default Parameters](#default-parameters)
18. [Destructuring in Functions](#destructuring-in-functions)
19. [Recursion](#recursion)
20. [Best Practices](#best-practices)

---

## What are Functions?

A **function** is a block of code that performs a specific task. Think of it as a mini-program inside your main program. You write the code once and can use it many times.

### Basic Syntax
```javascript
function functionName() {
    // Code to execute
}
```

### Simple Example
```javascript
function sayHello() {
    console.log("Hello, World!");
}

// Call the function
sayHello(); // Output: Hello, World!
```

---

## Why Use Functions?

1. **Avoid Repetition**: Write code once, use it many times
2. **Organization**: Break big problems into smaller pieces
3. **Reusability**: Use the same function in different parts of your program
4. **Easy to Test**: Test small pieces separately
5. **Easy to Debug**: Find problems more easily

### Example Without Functions (Bad)
```javascript
console.log("Welcome to our website!");
console.log("Please enjoy your stay!");

console.log("Welcome to our website!");
console.log("Please enjoy your stay!");

console.log("Welcome to our website!");
console.log("Please enjoy your stay!");
```

### Example With Functions (Good)
```javascript
function showWelcome() {
    console.log("Welcome to our website!");
    console.log("Please enjoy your stay!");
}

showWelcome();
showWelcome();
showWelcome();
```

---

## Function Declaration

This is the most common way to create a function.

### Syntax
```javascript
function functionName(parameters) {
    // Function body
    return something; // Optional
}
```

### Examples
```javascript
// Simple function
function greet() {
    console.log("Hello there!");
}

// Function with parameters
function greetPerson(name) {
    console.log("Hello, " + name + "!");
}

// Function that returns a value
function addNumbers(a, b) {
    return a + b;
}

// Using the functions
greet(); // Output: Hello there!
greetPerson("Alice"); // Output: Hello, Alice!
let result = addNumbers(5, 3); // result = 8
```

---

## Function Expression

A function expression creates a function and stores it in a variable.

### Syntax
```javascript
const functionName = function(parameters) {
    // Function body
};
```

### Examples
```javascript
// Basic function expression
const sayGoodbye = function() {
    console.log("Goodbye!");
};

// Function expression with parameters
const multiply = function(x, y) {
    return x * y;
};

// Using the functions
sayGoodbye(); // Output: Goodbye!
let product = multiply(4, 5); // product = 20
```

### Named Function Expression
```javascript
const factorial = function fact(n) {
    if (n <= 1) return 1;
    return n * fact(n - 1);
};

console.log(factorial(5)); // Output: 120
```

---

## Arrow Functions

Arrow functions are a shorter way to write functions (introduced in ES6).

### Syntax
```javascript
const functionName = (parameters) => {
    // Function body
};

// For single expressions
const functionName = (parameters) => expression;
```

### Examples
```javascript
// Basic arrow function
const greetArrow = () => {
    console.log("Hello from arrow function!");
};

// Arrow function with parameters
const addArrow = (a, b) => {
    return a + b;
};

// Short form (single expression)
const multiplyArrow = (a, b) => a * b;

// Single parameter (parentheses optional)
const square = x => x * x;

// No parameters
const getCurrentTime = () => new Date();

// Using the functions
greetArrow(); // Output: Hello from arrow function!
console.log(addArrow(3, 4)); // Output: 7
console.log(multiplyArrow(3, 4)); // Output: 12
console.log(square(5)); // Output: 25
```

---

## Parameters and Arguments

**Parameters** are variables listed in the function definition.
**Arguments** are the actual values passed to the function when called.

### Examples
```javascript
// Parameters: name, age
function introduceUser(name, age) {
    console.log(`My name is ${name} and I am ${age} years old.`);
}

// Arguments: "John", 25
introduceUser("John", 25);
// Output: My name is John and I am 25 years old.

// Multiple parameters
function calculateArea(length, width, height) {
    return length * width * height;
}

let volume = calculateArea(10, 5, 3); // volume = 150
```

### Too Many or Too Few Arguments
```javascript
function testParams(a, b, c) {
    console.log("a:", a, "b:", b, "c:", c);
}

testParams(1, 2, 3); // a: 1 b: 2 c: 3
testParams(1, 2); // a: 1 b: 2 c: undefined
testParams(1, 2, 3, 4, 5); // a: 1 b: 2 c: 3 (extra arguments ignored)
```

---

## Return Values

Functions can send back (return) values to where they were called.

### Basic Return
```javascript
function addTwoNumbers(a, b) {
    return a + b; // Send back the result
}

let sum = addTwoNumbers(10, 20);
console.log(sum); // Output: 30
```

### Multiple Return Statements
```javascript
function checkAge(age) {
    if (age >= 18) {
        return "Adult";
    } else {
        return "Minor";
    }
}

console.log(checkAge(25)); // Output: Adult
console.log(checkAge(15)); // Output: Minor
```

### Returning Objects
```javascript
function createUser(name, email) {
    return {
        name: name,
        email: email,
        active: true
    };
}

let user = createUser("Alice", "alice@email.com");
console.log(user); // Output: {name: "Alice", email: "alice@email.com", active: true}
```

### Early Return
```javascript
function processData(data) {
    if (!data) {
        return "No data provided"; // Exit early
    }
    
    // Process the data
    return "Data processed successfully";
}
```

---

## Function Scope

Variables inside functions can't be accessed from outside. This is called **scope**.

### Local Scope
```javascript
function myFunction() {
    let localVariable = "I'm local!";
    console.log(localVariable); // This works
}

myFunction(); // Output: I'm local!
// console.log(localVariable); // Error! localVariable is not defined
```

### Global Scope
```javascript
let globalVariable = "I'm global!";

function accessGlobal() {
    console.log(globalVariable); // Can access global variables
}

accessGlobal(); // Output: I'm global!
console.log(globalVariable); // Output: I'm global!
```

### Scope Example
```javascript
let name = "Global Alice"; // Global variable

function showNames() {
    let name = "Local Bob"; // Local variable
    console.log("Inside function:", name);
}

showNames(); // Output: Inside function: Local Bob
console.log("Outside function:", name); // Output: Outside function: Global Alice
```

---

## Hoisting

Function declarations are "hoisted" - you can call them before they're defined in your code.

### Function Declaration Hoisting (Works)
```javascript
// This works because of hoisting
sayHello(); // Output: Hello!

function sayHello() {
    console.log("Hello!");
}
```

### Function Expression Hoisting (Doesn't Work)
```javascript
// This doesn't work
// sayGoodbye(); // Error! Cannot access 'sayGoodbye' before initialization

const sayGoodbye = function() {
    console.log("Goodbye!");
};
```

### Arrow Function Hoisting (Doesn't Work)
```javascript
// This doesn't work
// greetArrow(); // Error! Cannot access 'greetArrow' before initialization

const greetArrow = () => {
    console.log("Hello from arrow!");
};
```

---

## Anonymous Functions

Functions without names. Usually used as values or arguments.

### Examples
```javascript
// Anonymous function in a variable
const anonymous = function() {
    console.log("I'm anonymous!");
};

// Anonymous function as an argument
setTimeout(function() {
    console.log("This runs after 2 seconds");
}, 2000);

// Anonymous arrow function
setTimeout(() => {
    console.log("Arrow function after 1 second");
}, 1000);

// Anonymous function with array methods
let numbers = [1, 2, 3, 4, 5];
let doubled = numbers.map(function(num) {
    return num * 2;
});
console.log(doubled); // Output: [2, 4, 6, 8, 10]
```

---

## Callback Functions

A callback is a function passed as an argument to another function.

### Basic Example
```javascript
function processUserInput(callback) {
    let name = "Alice";
    callback(name);
}

function greetUser(userName) {
    console.log("Hello, " + userName + "!");
}

processUserInput(greetUser); // Output: Hello, Alice!
```

### Practical Example
```javascript
function calculator(num1, num2, operation) {
    return operation(num1, num2);
}

function add(a, b) {
    return a + b;
}

function multiply(a, b) {
    return a * b;
}

console.log(calculator(5, 3, add)); // Output: 8
console.log(calculator(5, 3, multiply)); // Output: 15

// Using anonymous functions
console.log(calculator(10, 2, function(a, b) {
    return a - b;
})); // Output: 8
```

### Array Callbacks
```javascript
let fruits = ["apple", "banana", "orange"];

// forEach callback
fruits.forEach(function(fruit) {
    console.log("I like " + fruit);
});

// map callback
let upperFruits = fruits.map(function(fruit) {
    return fruit.toUpperCase();
});
console.log(upperFruits); // Output: ["APPLE", "BANANA", "ORANGE"]

// filter callback
let longFruits = fruits.filter(function(fruit) {
    return fruit.length > 5;
});
console.log(longFruits); // Output: ["banana", "orange"]
```

---

## Higher-Order Functions

Functions that take other functions as arguments or return functions.

### Functions that Take Functions
```javascript
function applyOperation(numbers, operation) {
    let result = [];
    for (let num of numbers) {
        result.push(operation(num));
    }
    return result;
}

let numbers = [1, 2, 3, 4, 5];

// Double each number
let doubled = applyOperation(numbers, function(x) {
    return x * 2;
});
console.log(doubled); // Output: [2, 4, 6, 8, 10]

// Square each number
let squared = applyOperation(numbers, x => x * x);
console.log(squared); // Output: [1, 4, 9, 16, 25]
```

### Functions that Return Functions
```javascript
function createMultiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

let double = createMultiplier(2);
let triple = createMultiplier(3);

console.log(double(5)); // Output: 10
console.log(triple(4)); // Output: 12
```

### Practical Example
```javascript
function createValidator(minLength) {
    return function(input) {
        return input.length >= minLength;
    };
}

let validatePassword = createValidator(8);
let validateUsername = createValidator(3);

console.log(validatePassword("abc")); // Output: false
console.log(validatePassword("password123")); // Output: true
console.log(validateUsername("bob")); // Output: true
```

---

## IIFE (Immediately Invoked Function Expression)

A function that runs immediately after it's created.

### Syntax
```javascript
(function() {
    // Code here runs immediately
})();

// Arrow function version
(() => {
    // Code here runs immediately
})();
```

### Examples
```javascript
// Basic IIFE
(function() {
    console.log("This runs immediately!");
})();

// IIFE with parameters
(function(name) {
    console.log("Hello, " + name + "!");
})("Alice");

// IIFE that returns a value
let result = (function(a, b) {
    return a + b;
})(5, 10);
console.log(result); // Output: 15

// Arrow function IIFE
((name) => {
    console.log(`Arrow IIFE says hello to ${name}!`);
})("Bob");
```

### Why Use IIFE?
```javascript
// Avoid polluting global scope
(function() {
    let privateVariable = "I'm private!";
    // This variable won't interfere with other code
})();

// Create modules
let calculator = (function() {
    let result = 0;
    
    return {
        add: function(num) {
            result += num;
            return this;
        },
        multiply: function(num) {
            result *= num;
            return this;
        },
        getResult: function() {
            return result;
        }
    };
})();

calculator.add(5).multiply(3);
console.log(calculator.getResult()); // Output: 15
```

---

## Closure

A closure gives you access to an outer function's variables from an inner function.

### Basic Example
```javascript
function outerFunction(x) {
    // This is the outer function's variable
    
    function innerFunction(y) {
        // Inner function can access outer function's variable
        return x + y;
    }
    
    return innerFunction;
}

let addFive = outerFunction(5);
console.log(addFive(10)); // Output: 15
```

### Practical Examples
```javascript
// Counter using closure
function createCounter() {
    let count = 0;
    
    return function() {
        count++;
        return count;
    };
}

let counter1 = createCounter();
let counter2 = createCounter();

console.log(counter1()); // Output: 1
console.log(counter1()); // Output: 2
console.log(counter2()); // Output: 1 (separate counter)

// Private variables with closure
function bankAccount(initialBalance) {
    let balance = initialBalance;
    
    return {
        deposit: function(amount) {
            balance += amount;
            return balance;
        },
        withdraw: function(amount) {
            if (amount <= balance) {
                balance -= amount;
                return balance;
            } else {
                return "Insufficient funds";
            }
        },
        getBalance: function() {
            return balance;
        }
    };
}

let account = bankAccount(100);
console.log(account.deposit(50)); // Output: 150
console.log(account.withdraw(30)); // Output: 120
console.log(account.getBalance()); // Output: 120
// console.log(account.balance); // Output: undefined (private!)
```

---

## Function Methods

Functions are objects in JavaScript and have built-in methods.

### call() Method
```javascript
function greet(greeting, punctuation) {
    return greeting + " " + this.name + punctuation;
}

let person = { name: "Alice" };

// Using call()
let message = greet.call(person, "Hello", "!");
console.log(message); // Output: Hello Alice!
```

### apply() Method
```javascript
function introduce(age, city) {
    return `Hi, I'm ${this.name}, ${age} years old, from ${city}.`;
}

let person = { name: "Bob" };

// Using apply() (arguments as array)
let introduction = introduce.apply(person, [30, "New York"]);
console.log(introduction); // Output: Hi, I'm Bob, 30 years old, from New York.
```

### bind() Method
```javascript
function sayHello() {
    return "Hello, " + this.name + "!";
}

let person = { name: "Charlie" };

// Using bind() (creates a new function)
let boundGreeting = sayHello.bind(person);
console.log(boundGreeting()); // Output: Hello, Charlie!

// Partial application with bind
function multiply(a, b) {
    return a * b;
}

let double = multiply.bind(null, 2);
console.log(double(5)); // Output: 10
console.log(double(8)); // Output: 16
```

---

## Rest Parameters

Use `...` to accept unlimited number of arguments as an array.

### Syntax
```javascript
function functionName(...restParameter) {
    // restParameter is an array
}
```

### Examples
```javascript
// Basic rest parameters
function addAll(...numbers) {
    let sum = 0;
    for (let num of numbers) {
        sum += num;
    }
    return sum;
}

console.log(addAll(1, 2, 3)); // Output: 6
console.log(addAll(1, 2, 3, 4, 5)); // Output: 15

// Rest parameters with other parameters
function introduce(name, ...hobbies) {
    console.log(`Hi, I'm ${name}.`);
    console.log("My hobbies are:", hobbies.join(", "));
}

introduce("Alice", "reading", "swimming", "coding");
// Output: 
// Hi, I'm Alice.
// My hobbies are: reading, swimming, coding

// Rest parameters in arrow functions
const findMax = (...numbers) => {
    return Math.max(...numbers);
};

console.log(findMax(3, 7, 2, 9, 1)); // Output: 9
```

---

## Default Parameters

Give parameters default values if no argument is provided.

### Syntax
```javascript
function functionName(parameter = defaultValue) {
    // Function body
}
```

### Examples
```javascript
// Basic default parameters
function greet(name = "Guest") {
    console.log("Hello, " + name + "!");
}

greet(); // Output: Hello, Guest!
greet("Alice"); // Output: Hello, Alice!

// Multiple default parameters
function createUser(name = "Anonymous", age = 0, country = "Unknown") {
    return {
        name: name,
        age: age,
        country: country
    };
}

console.log(createUser()); // {name: "Anonymous", age: 0, country: "Unknown"}
console.log(createUser("Bob", 25)); // {name: "Bob", age: 25, country: "Unknown"}

// Default parameters with expressions
function calculatePrice(price, tax = price * 0.1) {
    return price + tax;
}

console.log(calculatePrice(100)); // Output: 110
console.log(calculatePrice(100, 15)); // Output: 115

// Default parameters with functions
function getCurrentTime() {
    return new Date().toLocaleTimeString();
}

function logMessage(message, timestamp = getCurrentTime()) {
    console.log(`[${timestamp}] ${message}`);
}

logMessage("System started");
```

---

## Destructuring in Functions

Extract values from objects or arrays in function parameters.

### Object Destructuring
```javascript
// Without destructuring
function createUserCard(user) {
    return `Name: ${user.name}, Age: ${user.age}, Email: ${user.email}`;
}

// With destructuring
function createUserCardDestruct({name, age, email}) {
    return `Name: ${name}, Age: ${age}, Email: ${email}`;
}

let user = {
    name: "Alice",
    age: 30,
    email: "alice@email.com"
};

console.log(createUserCardDestruct(user));
// Output: Name: Alice, Age: 30, Email: alice@email.com

// With default values
function greetUser({name = "Guest", age = "unknown"} = {}) {
    console.log(`Hello ${name}, you are ${age} years old.`);
}

greetUser({name: "Bob", age: 25}); // Hello Bob, you are 25 years old.
greetUser({name: "Charlie"}); // Hello Charlie, you are unknown years old.
greetUser(); // Hello Guest, you are unknown years old.
```

### Array Destructuring
```javascript
function getFirstTwo([first, second]) {
    return `First: ${first}, Second: ${second}`;
}

let numbers = [10, 20, 30, 40];
console.log(getFirstTwo(numbers)); // Output: First: 10, Second: 20

// With rest parameters
function analyzeNumbers([first, second, ...rest]) {
    return {
        first: first,
        second: second,
        remaining: rest,
        total: rest.length + 2
    };
}

console.log(analyzeNumbers([1, 2, 3, 4, 5]));
// Output: {first: 1, second: 2, remaining: [3, 4, 5], total: 5}
```

---

## Recursion

A function that calls itself. Useful for solving problems that can be broken into smaller similar problems.

### Basic Example
```javascript
function countdown(num) {
    // Base case (stopping condition)
    if (num <= 0) {
        console.log("Done!");
        return;
    }
    
    console.log(num);
    countdown(num - 1); // Function calls itself
}

countdown(5);
// Output: 5, 4, 3, 2, 1, Done!
```

### Practical Examples
```javascript
// Factorial
function factorial(n) {
    // Base case
    if (n <= 1) {
        return 1;
    }
    
    // Recursive case
    return n * factorial(n - 1);
}

console.log(factorial(5)); // Output: 120 (5 * 4 * 3 * 2 * 1)

// Fibonacci sequence
function fibonacci(n) {
    if (n <= 1) {
        return n;
    }
    
    return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(7)); // Output: 13

// Sum of array elements
function sumArray(arr, index = 0) {
    // Base case
    if (index >= arr.length) {
        return 0;
    }
    
    // Recursive case
    return arr[index] + sumArray(arr, index + 1);
}

let numbers = [1, 2, 3, 4, 5];
console.log(sumArray(numbers)); // Output: 15
```

### Tree Traversal Example
```javascript
// Counting properties in nested objects
function countProperties(obj) {
    let count = 0;
    
    for (let key in obj) {
        count++; // Count this property
        
        // If the value is an object, recurse
        if (typeof obj[key] === 'object' && obj[key] !== null) {
            count += countProperties(obj[key]);
        }
    }
    
    return count;
}

let data = {
    name: "Alice",
    address: {
        street: "123 Main St",
        city: "Boston",
        coordinates: {
            lat: 42.3601,
            lng: -71.0589
        }
    },
    age: 30
};

console.log(countProperties(data)); // Output: 7
```

---

## Best Practices

### 1. Use Descriptive Names
```javascript
// Bad
function calc(x, y) {
    return x * y * 0.1;
}

// Good
function calculateTax(price, taxRate) {
    return price * taxRate * 0.1;
}
```

### 2. Keep Functions Small
```javascript
// Bad - function does too many things
function processUser(userData) {
    // validate data
    if (!userData.email) return false;
    if (!userData.name) return false;
    
    // save to database
    database.save(userData);
    
    // send email
    emailService.send(userData.email, "Welcome!");
    
    // log activity
    console.log("User created:", userData.name);
    
    return true;
}

// Good - separate functions for separate tasks
function validateUserData(userData) {
    return userData.email && userData.name;
}

function saveUser(userData) {
    return database.save(userData);
}

function sendWelcomeEmail(email) {
    return emailService.send(email, "Welcome!");
}

function logUserCreation(name) {
    console.log("User created:", name);
}

function processUser(userData) {
    if (!validateUserData(userData)) {
        return false;
    }
    
    saveUser(userData);
    sendWelcomeEmail(userData.email);
    logUserCreation(userData.name);
    
    return true;
}
```

### 3. Use Pure Functions When Possible
```javascript
// Impure function (has side effects)
let total = 0;
function addToTotal(num) {
    total += num; // Modifies external variable
    return total;
}

// Pure function (no side effects)
function add(a, b) {
    return a + b; // Only depends on inputs
}
```

### 4. Handle Errors Properly
```javascript
function divideNumbers(a, b) {
    if (b === 0) {
        throw new Error("Cannot divide by zero");
    }
    
    if (typeof a !== 'number' || typeof b !== 'number') {
        throw new Error("Both arguments must be numbers");
    }
    
    return a / b;
}

// Usage with error handling
try {
    let result = divideNumbers(10, 2);
    console.log(result);
} catch (error) {
    console.error("Error:", error.message);
}
```

### 5. Use Arrow Functions for Short Functions
```javascript
// For simple operations
const numbers = [1, 2, 3, 4, 5];

// Good use of arrow functions
const doubled = numbers.map(x => x * 2);
const evens = numbers.filter(x => x % 2 === 0);
const sum = numbers.reduce((acc, x) => acc + x, 0);

// But use regular functions for complex logic
function processComplexData(data) {
    // Multiple lines of complex logic
    if (!data || !Array.isArray(data)) {
        return null;
    }
    
    return data
        .filter(item => item.active)
        .map(item => ({
            ...item,
            processed: true,
            timestamp: new Date()
        }))
        .sort((a, b) => a.priority - b.priority);
}
```

### 6. Document Your Functions
```javascript
/**
 * Calculates the area of a circle
 * @param {number} radius - The radius of the circle
 * @returns {number} The area of the circle
 * @throws {Error} If radius is negative
 */
function calculateCircleArea(radius) {
    if (radius < 0) {
        throw new Error("Radius cannot be negative");
    }
    
    return Math.PI * radius * radius;
}
```

---

## Summary

Functions are one of the most important concepts in JavaScript. They help you:

- **Organize** your code into reusable pieces
- **Avoid repetition** by writing code once and using it many times
- **Break down** complex problems into smaller, manageable parts
- **Create** more maintainable and readable code

### Key Points to Remember:

1. **Function Declaration**: `function name() {}`
2. **Function Expression**: `const name = function() {}`
3. **Arrow Functions**: `const name = () => {}`
4. **Parameters**: Variables in function definition
5. **Arguments**: Actual values passed to function
6. **Return**: Send values back from functions
7. **Scope**: Variables inside functions are private
8. **Callbacks**: Functions passed to other functions
9. **Closures**: Inner functions accessing outer variables
10. **Best Practices**: Use good names, keep functions small, handle errors

Start with simple functions and gradually work your way up to more complex concepts like closures and higher-order functions. Practice writing functions for everyday tasks, and soon they'll become second nature!

---

*Happy coding! 🚀*
