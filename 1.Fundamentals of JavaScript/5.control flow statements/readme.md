# JavaScript Control Flow Statements - Complete Guide

## Table of Contents
- [What are Control Flow Statements?](#what-are-control-flow-statements)
- [Conditional Statements](#conditional-statements)
  - [if Statement](#if-statement)
  - [if...else Statement](#ifelse-statement)
  - [if...else if...else Statement](#ifelse-ifelse-statement)
  - [switch Statement](#switch-statement)
- [Loop Statements](#loop-statements)
  - [for Loop](#for-loop)
  - [while Loop](#while-loop)
  - [do...while Loop](#dowhile-loop)
  - [for...in Loop](#forin-loop)
  - [for...of Loop](#forof-loop)
- [Jump Statements](#jump-statements)
  - [break Statement](#break-statement)
  - [continue Statement](#continue-statement)
  - [return Statement](#return-statement)
  - [throw Statement](#throw-statement)

---

## What are Control Flow Statements?

Control flow statements are instructions that determine the order in which code executes. Think of them as traffic signals for your code - they decide which path the program should take based on conditions or how many times to repeat certain actions.

**Example:**
```javascript
let weather = "sunny";

if (weather === "sunny") {
    console.log("Let's go to the beach!"); // This runs
} else {
    console.log("Let's stay inside.");     // This doesn't run
}
```

---

## Conditional Statements

These statements execute different code blocks based on whether conditions are true or false.

### if Statement

The `if` statement runs code only when a condition is true.

**Syntax:**
```javascript
if (condition) {
    // Code to run if condition is true
}
```

**Examples:**
```javascript
// Simple condition
let age = 18;
if (age >= 18) {
    console.log("You can vote!"); // This will run
}

// With variables
let hasTicket = true;
if (hasTicket) {
    console.log("Welcome to the movie!");
}

// With expressions
let score = 85;
if (score > 80) {
    console.log("Great job!"); // This runs because 85 > 80
}

// With function calls
function isWeekend() {
    let today = new Date().getDay();
    return today === 0 || today === 6; // Sunday = 0, Saturday = 6
}

if (isWeekend()) {
    console.log("Time to relax!");
}

// Multiple conditions using logical operators
let temperature = 75;
let isRaining = false;

if (temperature > 70 && !isRaining) {
    console.log("Perfect weather for a walk!");
}
```

### if...else Statement

The `if...else` statement runs one block of code if the condition is true, and another block if it's false.

**Syntax:**
```javascript
if (condition) {
    // Code if condition is true
} else {
    // Code if condition is false
}
```

**Examples:**
```javascript
// Basic if...else
let password = "12345";
if (password.length >= 8) {
    console.log("Password is strong");
} else {
    console.log("Password is too short"); // This runs
}

// With user input simulation
let userAge = 16;
if (userAge >= 18) {
    console.log("You can enter the club");
} else {
    console.log("Sorry, you must be 18 or older"); // This runs
}

// With calculations
let bankBalance = 500;
let purchaseAmount = 750;

if (bankBalance >= purchaseAmount) {
    console.log("Purchase approved");
    bankBalance -= purchaseAmount;
} else {
    console.log("Insufficient funds"); // This runs
    console.log(`You need $${purchaseAmount - bankBalance} more`);
}

// Ternary operator (shorthand for if...else)
let mood = "happy";
let message = mood === "happy" ? "Have a great day!" : "Hope things get better";
console.log(message); // "Have a great day!"
```

### if...else if...else Statement

This allows you to test multiple conditions in sequence.

**Syntax:**
```javascript
if (condition1) {
    // Code if condition1 is true
} else if (condition2) {
    // Code if condition2 is true
} else if (condition3) {
    // Code if condition3 is true
} else {
    // Code if none of the conditions are true
}
```

**Examples:**
```javascript
// Grade calculator
let score = 87;
let grade;

if (score >= 90) {
    grade = "A";
} else if (score >= 80) {
    grade = "B"; // This runs because score is 87
} else if (score >= 70) {
    grade = "C";
} else if (score >= 60) {
    grade = "D";
} else {
    grade = "F";
}

console.log(`Your grade is: ${grade}`); // "Your grade is: B"

// Weather-based clothing suggestions
let temperature = 45;
let clothing;

if (temperature > 80) {
    clothing = "shorts and t-shirt";
} else if (temperature > 60) {
    clothing = "light jacket";
} else if (temperature > 40) {
    clothing = "warm coat"; // This runs
} else {
    clothing = "heavy winter coat";
}

console.log(`Wear: ${clothing}`); // "Wear: warm coat"

// Time-based greetings
let hour = 14; // 2 PM in 24-hour format

if (hour < 12) {
    console.log("Good morning!");
} else if (hour < 18) {
    console.log("Good afternoon!"); // This runs
} else {
    console.log("Good evening!");
}

// Multiple conditions in each if
let day = "Saturday";
let weather = "sunny";

if (day === "Saturday" && weather === "sunny") {
    console.log("Perfect day for outdoor activities!"); // This runs
} else if (day === "Saturday" && weather === "rainy") {
    console.log("Great day for indoor activities!");
} else if (day === "Sunday") {
    console.log("Relaxing Sunday!");
} else {
    console.log("Regular weekday");
}
```

### switch Statement

The `switch` statement compares a value against multiple cases and executes the matching case.

**Syntax:**
```javascript
switch (expression) {
    case value1:
        // Code to run if expression === value1
        break;
    case value2:
        // Code to run if expression === value2
        break;
    default:
        // Code to run if no cases match
        break;
}
```

**Examples:**
```javascript
// Basic switch
let dayOfWeek = 3;
let dayName;

switch (dayOfWeek) {
    case 1:
        dayName = "Monday";
        break;
    case 2:
        dayName = "Tuesday";
        break;
    case 3:
        dayName = "Wednesday"; // This case runs
        break;
    case 4:
        dayName = "Thursday";
        break;
    case 5:
        dayName = "Friday";
        break;
    case 6:
        dayName = "Saturday";
        break;
    case 7:
        dayName = "Sunday";
        break;
    default:
        dayName = "Invalid day";
        break;
}

console.log(dayName); // "Wednesday"

// Switch with strings
let fruit = "apple";
let color;

switch (fruit) {
    case "apple":
        color = "red or green"; // This runs
        break;
    case "banana":
        color = "yellow";
        break;
    case "orange":
        color = "orange";
        break;
    case "grape":
        color = "purple";
        break;
    default:
        color = "unknown";
        break;
}

console.log(`${fruit} is ${color}`); // "apple is red or green"

// Multiple cases for same action (fall-through)
let month = "December";
let season;

switch (month) {
    case "December":
    case "January":
    case "February":
        season = "Winter"; // This runs
        break;
    case "March":
    case "April":
    case "May":
        season = "Spring";
        break;
    case "June":
    case "July":
    case "August":
        season = "Summer";
        break;
    case "September":
    case "October":
    case "November":
        season = "Fall";
        break;
    default:
        season = "Unknown";
        break;
}

console.log(`${month} is in ${season}`); // "December is in Winter"

// Switch with calculations
let operation = "+";
let a = 10;
let b = 5;
let result;

switch (operation) {
    case "+":
        result = a + b; // This runs: 10 + 5 = 15
        break;
    case "-":
        result = a - b;
        break;
    case "*":
        result = a * b;
        break;
    case "/":
        result = b !== 0 ? a / b : "Cannot divide by zero";
        break;
    default:
        result = "Invalid operation";
        break;
}

console.log(`${a} ${operation} ${b} = ${result}`); // "10 + 5 = 15"
```

---

## Loop Statements

Loops repeat code blocks multiple times based on conditions.

### for Loop

The `for` loop repeats code a specific number of times.

**Syntax:**
```javascript
for (initialization; condition; increment/decrement) {
    // Code to repeat
}
```

**Examples:**
```javascript
// Basic counting
for (let i = 1; i <= 5; i++) {
    console.log(`Count: ${i}`);
}
// Output: Count: 1, Count: 2, Count: 3, Count: 4, Count: 5

// Counting backwards
for (let i = 5; i >= 1; i--) {
    console.log(`Countdown: ${i}`);
}
// Output: Countdown: 5, Countdown: 4, Countdown: 3, Countdown: 2, Countdown: 1

// Looping through arrays
let fruits = ["apple", "banana", "orange", "grape"];
for (let i = 0; i < fruits.length; i++) {
    console.log(`Fruit ${i + 1}: ${fruits[i]}`);
}
// Output: Fruit 1: apple, Fruit 2: banana, etc.

// Step by different amounts
for (let i = 0; i <= 20; i += 5) {
    console.log(`Step: ${i}`);
}
// Output: Step: 0, Step: 5, Step: 10, Step: 15, Step: 20

// Nested loops (multiplication table)
for (let i = 1; i <= 3; i++) {
    for (let j = 1; j <= 3; j++) {
        console.log(`${i} × ${j} = ${i * j}`);
    }
}

// Loop with conditions inside
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evenNumbers = [];

for (let i = 0; i < numbers.length; i++) {
    if (numbers[i] % 2 === 0) {
        evenNumbers.push(numbers[i]);
    }
}
console.log("Even numbers:", evenNumbers); // [2, 4, 6, 8, 10]
```

### while Loop

The `while` loop repeats code as long as a condition is true.

**Syntax:**
```javascript
while (condition) {
    // Code to repeat
    // Don't forget to update the condition!
}
```

**Examples:**
```javascript
// Basic counting with while
let count = 1;
while (count <= 5) {
    console.log(`Count: ${count}`);
    count++; // Very important! Without this, infinite loop
}

// User input simulation (keep asking until valid)
let password = "";
let attempts = 0;

while (password !== "secret" && attempts < 3) {
    // Simulate getting user input
    password = attempts === 0 ? "wrong1" : 
               attempts === 1 ? "wrong2" : "secret";
    attempts++;
    
    if (password !== "secret") {
        console.log(`Wrong password. Attempt ${attempts}`);
    }
}

if (password === "secret") {
    console.log("Access granted!");
} else {
    console.log("Too many attempts!");
}

// Processing until a condition is met
let randomNumbers = [];
let sum = 0;

while (sum < 50) {
    let randomNum = Math.floor(Math.random() * 10) + 1; // 1-10
    randomNumbers.push(randomNum);
    sum += randomNum;
    console.log(`Added ${randomNum}, sum is now ${sum}`);
}

console.log(`Final numbers: ${randomNumbers}`);
console.log(`Final sum: ${sum}`);

// Reading from an array until empty
let tasks = ["wash dishes", "do laundry", "clean room"];

while (tasks.length > 0) {
    let currentTask = tasks.shift(); // Remove first item
    console.log(`Completed: ${currentTask}`);
}
console.log("All tasks completed!");
```

### do...while Loop

The `do...while` loop runs code at least once, then repeats as long as a condition is true.

**Syntax:**
```javascript
do {
    // Code to run at least once
} while (condition);
```

**Examples:**
```javascript
// Basic do...while (runs at least once)
let number = 10;
do {
    console.log(`Number: ${number}`);
    number++;
} while (number <= 5);
// Output: "Number: 10" (runs once even though 10 > 5)

// Menu system simulation
let choice;
do {
    console.log("\n--- Menu ---");
    console.log("1. Play Game");
    console.log("2. View Settings");
    console.log("3. Exit");
    
    // Simulate user choice
    choice = Math.floor(Math.random() * 4); // 0-3
    
    switch (choice) {
        case 1:
            console.log("Starting game...");
            break;
        case 2:
            console.log("Opening settings...");
            break;
        case 3:
            console.log("Goodbye!");
            break;
        default:
            console.log("Invalid choice, try again.");
            break;
    }
} while (choice !== 3);

// Input validation
let userAge;
do {
    // Simulate getting user input
    userAge = Math.floor(Math.random() * 150); // 0-149
    
    if (userAge < 1 || userAge > 120) {
        console.log(`${userAge} is not a valid age. Please try again.`);
    }
} while (userAge < 1 || userAge > 120);

console.log(`Thank you! Your age is ${userAge}`);

// Game loop example
let playerHealth = 100;
let round = 1;

do {
    console.log(`\nRound ${round}: Health = ${playerHealth}`);
    
    // Simulate taking damage
    let damage = Math.floor(Math.random() * 20) + 5; // 5-24 damage
    playerHealth -= damage;
    console.log(`You took ${damage} damage!`);
    
    if (playerHealth > 0) {
        console.log(`You survived with ${playerHealth} health!`);
    }
    
    round++;
} while (playerHealth > 0);

console.log(`Game Over! You survived ${round - 1} rounds.`);
```

### for...in Loop

The `for...in` loop iterates over the properties of an object.

**Syntax:**
```javascript
for (let key in object) {
    // Code to run for each property
}
```

**Examples:**
```javascript
// Basic object iteration
let person = {
    name: "Alice",
    age: 30,
    city: "New York",
    occupation: "Engineer"
};

for (let key in person) {
    console.log(`${key}: ${person[key]}`);
}
// Output: name: Alice, age: 30, city: New York, occupation: Engineer

// Array iteration (gets indices)
let colors = ["red", "green", "blue"];
for (let index in colors) {
    console.log(`Index ${index}: ${colors[index]}`);
}
// Output: Index 0: red, Index 1: green, Index 2: blue

// Counting properties
let student = {
    firstName: "John",
    lastName: "Doe",
    grade: "A",
    subjects: ["Math", "Science", "English"]
};

let propertyCount = 0;
for (let prop in student) {
    propertyCount++;
    console.log(`Property ${propertyCount}: ${prop} = ${student[prop]}`);
}

// Filtering properties
let car = {
    make: "Toyota",
    model: "Camry",
    year: 2020,
    color: "blue",
    mileage: 15000
};

console.log("String properties:");
for (let key in car) {
    if (typeof car[key] === "string") {
        console.log(`${key}: ${car[key]}`);
    }
}
// Output: make: Toyota, model: Camry, color: blue

// Creating a copy of an object
let original = { a: 1, b: 2, c: 3 };
let copy = {};

for (let key in original) {
    copy[key] = original[key];
}

console.log("Original:", original); // { a: 1, b: 2, c: 3 }
console.log("Copy:", copy);         // { a: 1, b: 2, c: 3 }
```

### for...of Loop

The `for...of` loop iterates over the values of iterable objects (arrays, strings, etc.).

**Syntax:**
```javascript
for (let value of iterable) {
    // Code to run for each value
}
```

**Examples:**
```javascript
// Array iteration
let fruits = ["apple", "banana", "cherry"];
for (let fruit of fruits) {
    console.log(`I like ${fruit}`);
}
// Output: I like apple, I like banana, I like cherry

// String iteration (each character)
let word = "Hello";
for (let letter of word) {
    console.log(`Letter: ${letter}`);
}
// Output: Letter: H, Letter: e, Letter: l, Letter: l, Letter: o

// With index using entries()
let animals = ["cat", "dog", "bird"];
for (let [index, animal] of animals.entries()) {
    console.log(`${index + 1}. ${animal}`);
}
// Output: 1. cat, 2. dog, 3. bird

// Set iteration
let uniqueNumbers = new Set([1, 2, 3, 4, 5]);
for (let number of uniqueNumbers) {
    console.log(`Number: ${number}`);
}

// Map iteration
let scores = new Map([
    ["Alice", 95],
    ["Bob", 87],
    ["Charlie", 92]
]);

for (let [name, score] of scores) {
    console.log(`${name}: ${score} points`);
}

// Processing array elements
let prices = [19.99, 25.50, 12.75, 8.00];
let total = 0;

for (let price of prices) {
    total += price;
    console.log(`Added $${price}, running total: $${total.toFixed(2)}`);
}

console.log(`Final total: $${total.toFixed(2)}`);

// Filtering with for...of
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evenNumbers = [];

for (let num of numbers) {
    if (num % 2 === 0) {
        evenNumbers.push(num);
    }
}

console.log("Even numbers:", evenNumbers); // [2, 4, 6, 8, 10]
```

---

## Jump Statements

Jump statements change the normal flow of program execution.

### break Statement

The `break` statement exits from loops or switch statements.

**Examples:**
```javascript
// Breaking out of a for loop
console.log("Finding first even number:");
for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) {
        console.log(`Found first even number: ${i}`);
        break; // Exit the loop
    }
    console.log(`${i} is odd, continuing...`);
}
// Output: 1 is odd, continuing... Found first even number: 2

// Breaking out of while loop
let attempts = 0;
let found = false;

while (attempts < 10) {
    attempts++;
    let randomNumber = Math.floor(Math.random() * 10) + 1;
    console.log(`Attempt ${attempts}: Got ${randomNumber}`);
    
    if (randomNumber === 7) {
        console.log("Found lucky number 7!");
        found = true;
        break; // Exit the loop early
    }
}

if (!found) {
    console.log("Didn't find lucky number 7 in 10 attempts");
}

// Break in nested loops (only breaks inner loop)
console.log("Break in nested loops:");
for (let i = 1; i <= 3; i++) {
    console.log(`Outer loop: ${i}`);
    for (let j = 1; j <= 3; j++) {
        if (j === 2) {
            console.log(`Breaking inner loop at j=${j}`);
            break; // Only breaks the inner loop
        }
        console.log(`  Inner loop: ${j}`);
    }
}

// Switch statement break
let grade = "B";
let message;

switch (grade) {
    case "A":
        message = "Excellent!";
        break;
    case "B":
        message = "Good job!"; // This runs
        break; // Prevents fall-through
    case "C":
        message = "Not bad";
        break;
    default:
        message = "Keep trying";
        break;
}

console.log(message); // "Good job!"

// Search example with break
let students = ["Alice", "Bob", "Charlie", "Diana", "Eve"];
let searchName = "Charlie";
let foundIndex = -1;

for (let i = 0; i < students.length; i++) {
    if (students[i] === searchName) {
        foundIndex = i;
        console.log(`Found ${searchName} at index ${i}`);
        break; // Stop searching once found
    }
}

if (foundIndex === -1) {
    console.log(`${searchName} not found`);
}
```

### continue Statement

The `continue` statement skips the rest of the current loop iteration and moves to the next one.

**Examples:**
```javascript
// Skip even numbers
console.log("Odd numbers from 1 to 10:");
for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) {
        continue; // Skip even numbers
    }
    console.log(i); // Only odd numbers are printed
}
// Output: 1, 3, 5, 7, 9

// Processing array with continue
let numbers = [1, -2, 3, -4, 5, -6, 7];
let positiveSum = 0;

for (let num of numbers) {
    if (num < 0) {
        console.log(`Skipping negative number: ${num}`);
        continue; // Skip negative numbers
    }
    positiveSum += num;
    console.log(`Added ${num}, sum is now ${positiveSum}`);
}

console.log(`Final sum of positive numbers: ${positiveSum}`); // 16

// Form validation example
let userInputs = ["alice@email.com", "", "bob@email", "charlie@email.com", "   "];

console.log("Valid emails:");
for (let input of userInputs) {
    // Skip empty or whitespace-only inputs
    if (!input.trim()) {
        console.log("Skipping empty input");
        continue;
    }
    
    // Skip invalid email format
    if (!input.includes("@") || !input.includes(".")) {
        console.log(`Skipping invalid email: ${input}`);
        continue;
    }
    
    console.log(`Valid email: ${input}`);
}

// Continue in while loop
let count = 0;
while (count < 10) {
    count++;
    
    if (count === 5) {
        console.log("Skipping number 5");
        continue;
    }
    
    console.log(`Number: ${count}`);
}

// Processing file list example
let files = ["document.txt", "image.jpg", "video.mp4", "readme.md", "script.js"];

console.log("Processing text files only:");
for (let file of files) {
    if (!file.endsWith(".txt") && !file.endsWith(".md")) {
        console.log(`Skipping non-text file: ${file}`);
        continue;
    }
    
    console.log(`Processing text file: ${file}`);
    // Simulate file processing
    console.log(`  -> ${file} processed successfully`);
}
```

### return Statement

The `return` statement exits from a function and optionally returns a value.

**Examples:**
```javascript
// Basic return
function greet(name) {
    return `Hello, ${name}!`;
    console.log("This line never runs"); // Unreachable code
}

let message = greet("Alice");
console.log(message); // "Hello, Alice!"

// Early return (guard clause)
function divide(a, b) {
    if (b === 0) {
        return "Cannot divide by zero"; // Exit early
    }
    return a / b;
}

console.log(divide(10, 2)); // 5
console.log(divide(10, 0)); // "Cannot divide by zero"

// Return without value (returns undefined)
function processUser(user) {
    if (!user || !user.name) {
        console.log("Invalid user");
        return; // Exit function, returns undefined
    }
    
    console.log(`Processing user: ${user.name}`);
    // More processing here...
}

processUser(null);              // "Invalid user"
processUser({ name: "Bob" });   // "Processing user: Bob"

// Multiple return points based on conditions
function getGrade(score) {
    if (score >= 90) return "A";
    if (score >= 80) return "B";
    if (score >= 70) return "C";
    if (score >= 60) return "D";
    return "F";
}

console.log(getGrade(95)); // "A"
console.log(getGrade(75)); // "C"
console.log(getGrade(45)); // "F"

// Returning objects
function createUser(name, email) {
    if (!name || !email) {
        return null; // Return null for invalid input
    }
    
    return {
        id: Date.now(),
        name: name,
        email: email,
        created: new Date()
    };
}

let user1 = createUser("Alice", "alice@email.com");
let user2 = createUser("", "invalid");

console.log(user1); // User object
console.log(user2); // null

// Returning from loops inside functions
function findFirstEven(numbers) {
    for (let num of numbers) {
        if (num % 2 === 0) {
            return num; // Return and exit function immediately
        }
    }
    return -1; // Not found
}

let nums1 = [1, 3, 5, 8, 9];
let nums2 = [1, 3, 5, 7];

console.log(findFirstEven(nums1)); // 8
console.log(findFirstEven(nums2)); // -1
```

### throw Statement

The `throw` statement creates custom errors.

**Examples:**
```javascript
// Basic throw
function checkAge(age) {
    if (age < 0) {
        throw new Error("Age cannot be negative");
    }
    if (age > 150) {
        throw new Error("Age seems unrealistic");
    }
    return `Age ${age} is valid`;
}

try {
    console.log(checkAge(25));  // "Age 25 is valid"
    console.log(checkAge(-5));  // Throws error
} catch (error) {
    console.log("Error:", error.message); // "Error: Age cannot be negative"
}

// Throwing different error types
function divide(a, b) {
    if (typeof a !== "number" || typeof b !== "number") {
        throw new TypeError("Both arguments must be numbers");
    }
    if (b === 0) {
        throw new RangeError("Division by zero is not allowed");
    }
    return a / b;
}

// Custom error class
class ValidationError extends Error {
    constructor(message, field) {
        super(message);
        this.name = "ValidationError";
        this.field = field;
    }
}

function validateUser(user) {
    if (!user.name) {
        throw new ValidationError("Name is required", "name");
    }
    if (!user.email || !user.email.includes("@")) {
        throw new ValidationError("Valid email is required", "email");
    }
    if (user.age < 18) {
        throw new ValidationError("Must be 18 or older", "age");
    }
    return "User is valid";
}

try {
    validateUser({ name: "Alice", email: "invalid-email", age: 16 });
} catch (error) {
    if (error instanceof ValidationError) {
        console.log(`Validation failed for ${error.field}: ${error.message}`);
    }
}

// Throwing strings (not recommended, but possible)
function simpleCheck(value) {
    if (!value) {
        throw "Value is required!";
    }
    return value;
}

try {
    simpleCheck("");
} catch (error) {
    console.log("Caught string error:", error); // "Caught string error: Value is required!"
}
```

---

