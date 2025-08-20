# JavaScript Operators - Complete Guide

## Table of Contents
- [What are Operators?](#what-are-operators)
- [Arithmetic Operators](#arithmetic-operators)
- [Assignment Operators](#assignment-operators)
- [Comparison Operators](#comparison-operators)
- [Logical Operators](#logical-operators)
- [Unary Operators](#unary-operators)
- [Ternary Operator](#ternary-operator)
- [Bitwise Operators](#bitwise-operators)
- [String Operators](#string-operators)
- [Type Operators](#type-operators)
- [Operator Precedence](#operator-precedence)

---

## What are Operators?

Operators are special symbols or keywords that perform operations on values (called operands). Think of them as tools that help you manipulate data in JavaScript.

**Example:**
```javascript
let result = 5 + 3; // '+' is the operator, '5' and '3' are operands
```

---

## Arithmetic Operators

These operators perform mathematical calculations.

### Addition (+)
Adds two numbers together.
```javascript
let sum = 10 + 5;        // Result: 15
let total = 2.5 + 3.7;   // Result: 6.2
```

### Subtraction (-)
Subtracts the second number from the first.
```javascript
let difference = 20 - 8;  // Result: 12
let result = 5.5 - 2.3;   // Result: 3.2
```

### Multiplication (*)
Multiplies two numbers.
```javascript
let product = 4 * 6;      // Result: 24
let area = 3.14 * 5 * 5;  // Result: 78.5
```

### Division (/)
Divides the first number by the second.
```javascript
let quotient = 20 / 4;    // Result: 5
let half = 10 / 2;        // Result: 5
```

### Modulus (%)
Returns the remainder after division.
```javascript
let remainder = 17 % 5;   // Result: 2
let evenCheck = 8 % 2;    // Result: 0 (8 is even)
```

### Exponentiation (**)
Raises the first number to the power of the second.
```javascript
let power = 2 ** 3;       // Result: 8 (2 to the power of 3)
let square = 5 ** 2;      // Result: 25
```

---

## Assignment Operators

These operators assign values to variables.

### Basic Assignment (=)
Assigns a value to a variable.
```javascript
let name = "John";
let age = 25;
let isStudent = true;
```

### Addition Assignment (+=)
Adds a value to the variable and assigns the result.
```javascript
let count = 10;
count += 5;    // Same as: count = count + 5
console.log(count); // Result: 15
```

### Subtraction Assignment (-=)
Subtracts a value from the variable and assigns the result.
```javascript
let score = 100;
score -= 20;   // Same as: score = score - 20
console.log(score); // Result: 80
```

### Multiplication Assignment (*=)
Multiplies the variable by a value and assigns the result.
```javascript
let price = 50;
price *= 2;    // Same as: price = price * 2
console.log(price); // Result: 100
```

### Division Assignment (/=)
Divides the variable by a value and assigns the result.
```javascript
let total = 200;
total /= 4;    // Same as: total = total / 4
console.log(total); // Result: 50
```

### Modulus Assignment (%=)
Assigns the remainder of division to the variable.
```javascript
let number = 17;
number %= 5;   // Same as: number = number % 5
console.log(number); // Result: 2
```

---

## Comparison Operators

These operators compare values and return true or false.

### Equal (==)
Checks if two values are equal (with type conversion).
```javascript
console.log(5 == 5);     // true
console.log(5 == "5");   // true (string "5" becomes number 5)
console.log(true == 1);  // true
```

### Strict Equal (===)
Checks if two values are equal without type conversion.
```javascript
console.log(5 === 5);    // true
console.log(5 === "5");  // false (different types)
console.log(true === 1); // false
```

### Not Equal (!=)
Checks if two values are not equal (with type conversion).
```javascript
console.log(5 != 3);     // true
console.log(5 != "5");   // false
console.log(true != 1);  // false
```

### Strict Not Equal (!==)
Checks if two values are not equal without type conversion.
```javascript
console.log(5 !== 3);    // true
console.log(5 !== "5");  // true (different types)
console.log(true !== 1); // true
```

### Greater Than (>)
Checks if the left value is greater than the right value.
```javascript
console.log(10 > 5);     // true
console.log(3 > 8);      // false
console.log("b" > "a");  // true (alphabetical comparison)
```

### Greater Than or Equal (>=)
Checks if the left value is greater than or equal to the right value.
```javascript
console.log(10 >= 10);   // true
console.log(15 >= 12);   // true
console.log(5 >= 8);     // false
```

### Less Than (<)
Checks if the left value is less than the right value.
```javascript
console.log(3 < 7);      // true
console.log(9 < 4);      // false
```

### Less Than or Equal (<=)
Checks if the left value is less than or equal to the right value.
```javascript
console.log(5 <= 5);     // true
console.log(3 <= 7);     // true
console.log(10 <= 6);    // false
```

---

## Logical Operators

These operators work with boolean values (true/false).

### Logical AND (&&)
Returns true only if both conditions are true.
```javascript
let age = 25;
let hasLicense = true;

console.log(age >= 18 && hasLicense); // true
console.log(age >= 30 && hasLicense); // false

// Short-circuit evaluation
let name = "John" && "Hello"; // "Hello" (truthy && truthy = second value)
let result = false && "Hello"; // false (stops at first falsy)
```

### Logical OR (||)
Returns true if at least one condition is true.
```javascript
let isWeekend = false;
let isHoliday = true;

console.log(isWeekend || isHoliday); // true
console.log(false || false);         // false

// Default values
let username = "" || "Guest"; // "Guest" (empty string is falsy)
```

### Logical NOT (!)
Reverses the boolean value.
```javascript
let isLoggedIn = true;
console.log(!isLoggedIn);    // false
console.log(!false);         // true
console.log(!"hello");       // false (non-empty string is truthy)
console.log(!"");            // true (empty string is falsy)
```

---

## Unary Operators

These operators work with a single operand.

### Unary Plus (+)
Converts a value to a number.
```javascript
console.log(+"5");        // 5 (string to number)
console.log(+true);       // 1
console.log(+false);      // 0
console.log(+"hello");    // NaN (Not a Number)
```

### Unary Minus (-)
Converts a value to a number and makes it negative.
```javascript
console.log(-"5");        // -5
console.log(-(-10));      // 10
```

### Increment (++)
Increases a number by 1.
```javascript
let count = 5;

// Pre-increment: increment first, then use
console.log(++count);     // 6, count is now 6

// Post-increment: use first, then increment
let score = 10;
console.log(score++);     // 10, but score becomes 11 after
console.log(score);       // 11
```

### Decrement (--)
Decreases a number by 1.
```javascript
let lives = 3;

// Pre-decrement: decrement first, then use
console.log(--lives);     // 2, lives is now 2

// Post-decrement: use first, then decrement
let attempts = 5;
console.log(attempts--);  // 5, but attempts becomes 4 after
console.log(attempts);    // 4
```

---

## Ternary Operator

The ternary operator is a shorthand for if-else statements.

### Syntax: condition ? valueIfTrue : valueIfFalse

```javascript
let age = 20;
let status = age >= 18 ? "adult" : "minor";
console.log(status); // "adult"

let score = 75;
let grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";
console.log(grade); // "C"

// Instead of:
let message;
if (age >= 18) {
    message = "You can vote";
} else {
    message = "Too young to vote";
}

// You can write:
let message = age >= 18 ? "You can vote" : "Too young to vote";
```

---

## Bitwise Operators

These operators work with binary representations of numbers.

### AND (&)
Performs bitwise AND operation.
```javascript
console.log(5 & 3);    // 1
// 5 in binary: 101
// 3 in binary: 011
// Result:      001 = 1
```

### OR (|)
Performs bitwise OR operation.
```javascript
console.log(5 | 3);    // 7
// 5 in binary: 101
// 3 in binary: 011
// Result:      111 = 7
```

### XOR (^)
Performs bitwise XOR (exclusive OR) operation.
```javascript
console.log(5 ^ 3);    // 6
// 5 in binary: 101
// 3 in binary: 011
// Result:      110 = 6
```

### NOT (~)
Performs bitwise NOT operation (flips all bits).
```javascript
console.log(~5);       // -6
```

### Left Shift (<<)
Shifts bits to the left.
```javascript
console.log(5 << 1);   // 10 (5 * 2^1)
console.log(3 << 2);   // 12 (3 * 2^2)
```

### Right Shift (>>)
Shifts bits to the right.
```javascript
console.log(10 >> 1);  // 5 (10 / 2^1)
console.log(12 >> 2);  // 3 (12 / 2^2)
```

---

## String Operators

### Concatenation (+)
Joins strings together.
```javascript
let firstName = "John";
let lastName = "Doe";
let fullName = firstName + " " + lastName;
console.log(fullName); // "John Doe"

let greeting = "Hello, " + "World!";
console.log(greeting); // "Hello, World!"
```

### Concatenation Assignment (+=)
Adds text to an existing string.
```javascript
let message = "Hello";
message += " World";
message += "!";
console.log(message); // "Hello World!"
```

---

## Type Operators

### typeof
Returns the type of a variable.
```javascript
console.log(typeof 42);          // "number"
console.log(typeof "hello");     // "string"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof null);        // "object" (this is a known quirk)
console.log(typeof {});          // "object"
console.log(typeof []);          // "object"
console.log(typeof function(){}); // "function"
```

### instanceof
Checks if an object is an instance of a specific type.
```javascript
let numbers = [1, 2, 3];
let today = new Date();

console.log(numbers instanceof Array);  // true
console.log(today instanceof Date);     // true
console.log("hello" instanceof String); // false (primitive string)
```

---

## Operator Precedence

Operators are executed in a specific order. Here's the priority from highest to lowest:

1. **Parentheses** `()`
2. **Unary operators** `++`, `--`, `!`, `typeof`
3. **Multiplication, Division, Modulus** `*`, `/`, `%`
4. **Addition, Subtraction** `+`, `-`
5. **Comparison** `<`, `>`, `<=`, `>=`
6. **Equality** `==`, `!=`, `===`, `!==`
7. **Logical AND** `&&`
8. **Logical OR** `||`
9. **Ternary** `? :`
10. **Assignment** `=`, `+=`, `-=`, etc.

### Examples:
```javascript
// Without parentheses
let result1 = 2 + 3 * 4;        // 14 (3*4 first, then +2)

// With parentheses to change order
let result2 = (2 + 3) * 4;      // 20 (2+3 first, then *4)

// Complex example
let x = 10;
let y = 5;
let z = x > y && y < 8 || x == 10; // true
// Step by step:
// 1. x > y → 10 > 5 → true
// 2. y < 8 → 5 < 8 → true  
// 3. true && true → true
// 4. x == 10 → 10 == 10 → true
// 5. true || true → true
```

---

## Quick Reference Table

| Operator | Name | Example | Result |
|----------|------|---------|---------|
| `+` | Addition | `5 + 3` | `8` |
| `-` | Subtraction | `10 - 4` | `6` |
| `*` | Multiplication | `3 * 7` | `21` |
| `/` | Division | `15 / 3` | `5` |
| `%` | Modulus | `17 % 5` | `2` |
| `**` | Exponentiation | `2 ** 3` | `8` |
| `==` | Equal | `5 == "5"` | `true` |
| `===` | Strict Equal | `5 === "5"` | `false` |
| `!=` | Not Equal | `5 != 3` | `true` |
| `!==` | Strict Not Equal | `5 !== "5"` | `true` |
| `>` | Greater Than | `8 > 5` | `true` |
| `<` | Less Than | `3 < 7` | `true` |
| `>=` | Greater or Equal | `5 >= 5` | `true` |
| `<=` | Less or Equal | `4 <= 6` | `true` |
| `&&` | Logical AND | `true && false` | `false` |
| `\|\|` | Logical OR | `true \|\| false` | `true` |
| `!` | Logical NOT | `!true` | `false` |
| `++` | Increment | `x++` | `x + 1` |
| `--` | Decrement | `x--` | `x - 1` |
| `? :` | Ternary | `age >= 18 ? "adult" : "minor"` | depends on age |

---

## Practice Tips

1. **Start with basic arithmetic** - Get comfortable with `+`, `-`, `*`, `/`
2. **Practice comparisons** - Use `==`, `===`, `>`, `<` in if statements
3. **Learn logical operators** - Master `&&`, `||`, `!` for conditions
4. **Use parentheses** - When in doubt about precedence, use `()` to be clear
5. **Try the ternary operator** - Great for simple if-else replacements
6. **Experiment in console** - Test operators directly in browser console

Remember: Practice makes perfect! Try these operators in real code to understand them better.
