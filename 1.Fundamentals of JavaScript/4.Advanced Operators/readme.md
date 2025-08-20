# JavaScript Advanced & Special Operators

## Table of Contents
- [Nullish Coalescing Operator](#nullish-coalescing-operator)
- [Optional Chaining Operator](#optional-chaining-operator)
- [Spread Operator](#spread-operator)
- [Rest Parameter](#rest-parameter)
- [Destructuring Assignment](#destructuring-assignment)
- [Template Literals](#template-literals)
- [in Operator](#in-operator)
- [delete Operator](#delete-operator)
- [void Operator](#void-operator)
- [new Operator](#new-operator)
- [super Operator](#super-operator)
- [this Keyword](#this-keyword)
- [Comma Operator](#comma-operator)
- [Conditional Assignment Operators](#conditional-assignment-operators)
- [BigInt Operators](#bigint-operators)
- [Symbol Operators](#symbol-operators)
- [Async/Await Operators](#asyncawait-operators)
- [Generator Operators](#generator-operators)

---

## Nullish Coalescing Operator (??)

Returns the right side when the left side is `null` or `undefined` (but not other falsy values like `0` or `""`).

```javascript
// Basic usage
let name = null ?? "Default Name";
console.log(name); // "Default Name"

let age = 0 ?? 25;
console.log(age); // 0 (because 0 is not null/undefined)

// Compare with OR operator
let value1 = 0 || "default";    // "default" (0 is falsy)
let value2 = 0 ?? "default";    // 0 (0 is not nullish)

let value3 = null || "default"; // "default"
let value4 = null ?? "default"; // "default"

// Practical examples
function getUserName(user) {
    return user.name ?? "Anonymous";
}

let settings = {
    theme: null,
    volume: 0,
    notifications: undefined
};

let theme = settings.theme ?? "light";           // "light"
let volume = settings.volume ?? 50;             // 0
let notifications = settings.notifications ?? true; // true
```

---

## Optional Chaining Operator (?.)

Safely access nested object properties without throwing errors if any link in the chain is `null` or `undefined`.

```javascript
// Object property access
let user = {
    name: "John",
    address: {
        street: "123 Main St",
        city: "Boston"
    }
};

// Safe property access
console.log(user?.name);              // "John"
console.log(user?.address?.street);   // "123 Main St"
console.log(user?.phone?.number);     // undefined (no error!)

// Without optional chaining, this would throw an error:
// console.log(user.phone.number); // TypeError: Cannot read property 'number' of undefined

// Array element access
let users = [
    { name: "Alice", posts: [{ title: "Hello" }] },
    { name: "Bob" }
];

console.log(users?.[0]?.name);           // "Alice"
console.log(users?.[0]?.posts?.[0]?.title); // "Hello"
console.log(users?.[1]?.posts?.[0]?.title); // undefined

// Method calling
let api = {
    getData() {
        return "data";
    }
};

console.log(api?.getData?.()); // "data"
console.log(api?.notExist?.()); // undefined (no error!)

// Dynamic property access
let propName = "address";
console.log(user?.[propName]?.city); // "Boston"
```

---

## Spread Operator (...)

Expands iterables (arrays, strings, objects) into individual elements.

### Array Spreading
```javascript
// Combining arrays
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4, 5, 6]

// Adding elements
let numbers = [2, 3, 4];
let moreNumbers = [1, ...numbers, 5];
console.log(moreNumbers); // [1, 2, 3, 4, 5]

// Copying arrays
let original = [1, 2, 3];
let copy = [...original];
copy.push(4);
console.log(original); // [1, 2, 3] (unchanged)
console.log(copy);     // [1, 2, 3, 4]

// Converting string to array
let str = "hello";
let chars = [...str];
console.log(chars); // ["h", "e", "l", "l", "o"]

// Function arguments
function sum(a, b, c) {
    return a + b + c;
}
let nums = [1, 2, 3];
console.log(sum(...nums)); // 6
```

### Object Spreading
```javascript
// Combining objects
let obj1 = { a: 1, b: 2 };
let obj2 = { c: 3, d: 4 };
let combined = { ...obj1, ...obj2 };
console.log(combined); // { a: 1, b: 2, c: 3, d: 4 }

// Copying objects
let person = { name: "John", age: 30 };
let personCopy = { ...person };
personCopy.age = 31;
console.log(person);     // { name: "John", age: 30 }
console.log(personCopy); // { name: "John", age: 31 }

// Overriding properties
let defaults = { theme: "light", size: "medium" };
let userPrefs = { theme: "dark" };
let settings = { ...defaults, ...userPrefs };
console.log(settings); // { theme: "dark", size: "medium" }

// Adding properties
let user = { name: "Alice" };
let userWithId = { ...user, id: 123, active: true };
console.log(userWithId); // { name: "Alice", id: 123, active: true }
```

---

## Rest Parameter (...)

Collects remaining elements into an array.

```javascript
// Function parameters
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3));       // 6
console.log(sum(1, 2, 3, 4, 5)); // 15

// Mixed parameters
function greet(greeting, ...names) {
    return greeting + " " + names.join(" and ");
}

console.log(greet("Hello", "Alice", "Bob", "Charlie"));
// "Hello Alice and Bob and Charlie"

// Array destructuring
let [first, second, ...rest] = [1, 2, 3, 4, 5];
console.log(first);  // 1
console.log(second); // 2
console.log(rest);   // [3, 4, 5]

// Object destructuring
let { name, age, ...otherProps } = {
    name: "John",
    age: 30,
    city: "Boston",
    country: "USA"
};

console.log(name);       // "John"
console.log(age);        // 30
console.log(otherProps); // { city: "Boston", country: "USA" }
```

---

## Destructuring Assignment

Unpacks values from arrays or properties from objects into separate variables.

### Array Destructuring
```javascript
// Basic destructuring
let [a, b, c] = [1, 2, 3];
console.log(a); // 1
console.log(b); // 2
console.log(c); // 3

// Skipping elements
let [first, , third] = [1, 2, 3];
console.log(first); // 1
console.log(third); // 3

// Default values
let [x = 10, y = 20] = [5];
console.log(x); // 5
console.log(y); // 20

// Swapping variables
let num1 = 10;
let num2 = 20;
[num1, num2] = [num2, num1];
console.log(num1); // 20
console.log(num2); // 10

// Nested destructuring
let [p, [q, r]] = [1, [2, 3]];
console.log(p); // 1
console.log(q); // 2
console.log(r); // 3
```

### Object Destructuring
```javascript
// Basic destructuring
let { name, age } = { name: "Alice", age: 25, city: "NYC" };
console.log(name); // "Alice"
console.log(age);  // 25

// Renaming variables
let { name: fullName, age: years } = { name: "Bob", age: 30 };
console.log(fullName); // "Bob"
console.log(years);    // 30

// Default values
let { theme = "light", size = "medium" } = { theme: "dark" };
console.log(theme); // "dark"
console.log(size);  // "medium"

// Nested destructuring
let user = {
    info: {
        personal: { name: "Charlie", age: 28 },
        contact: { email: "charlie@email.com" }
    }
};

let { info: { personal: { name: userName }, contact: { email } } } = user;
console.log(userName); // "Charlie"
console.log(email);    // "charlie@email.com"

// Function parameters
function displayUser({ name, age, city = "Unknown" }) {
    console.log(`${name}, ${age}, from ${city}`);
}

displayUser({ name: "Dave", age: 35 }); // "Dave, 35, from Unknown"
```

---

## Template Literals (``)

Enhanced string literals with embedded expressions and multi-line support.

```javascript
// Basic interpolation
let name = "World";
let greeting = `Hello, ${name}!`;
console.log(greeting); // "Hello, World!"

// Expressions
let a = 5;
let b = 3;
let result = `${a} + ${b} = ${a + b}`;
console.log(result); // "5 + 3 = 8"

// Multi-line strings
let multiLine = `This is
a multi-line
string`;
console.log(multiLine);

// Function calls
function formatCurrency(amount) {
    return `$${amount.toFixed(2)}`;
}

let price = 19.99;
let message = `The price is ${formatCurrency(price)}`;
console.log(message); // "The price is $19.99"

// Tagged templates
function highlight(strings, ...values) {
    return strings.reduce((result, string, i) => {
        return result + string + (values[i] ? `<mark>${values[i]}</mark>` : "");
    }, "");
}

let searchTerm = "JavaScript";
let text = highlight`Learning ${searchTerm} is fun!`;
console.log(text); // "Learning <mark>JavaScript</mark> is fun!"

// HTML template
let user = { name: "Alice", role: "Admin" };
let html = `
    <div class="user-card">
        <h3>${user.name}</h3>
        <p>Role: ${user.role}</p>
    </div>
`;
```

---

## in Operator

Checks if a property exists in an object.

```javascript
// Object properties
let person = { name: "John", age: 30 };

console.log("name" in person);    // true
console.log("height" in person);  // false
console.log("toString" in person); // true (inherited from Object.prototype)

// Array indices
let fruits = ["apple", "banana", "orange"];
console.log(0 in fruits); // true
console.log(3 in fruits); // false
console.log("length" in fruits); // true

// Checking for methods
if ("push" in fruits) {
    fruits.push("grape");
}

// Private properties (with Symbols)
let sym = Symbol("private");
let obj = { [sym]: "secret" };
console.log(sym in obj); // true

// Class instances
class Car {
    constructor(make) {
        this.make = make;
    }
    
    drive() {}
}

let myCar = new Car("Toyota");
console.log("make" in myCar);  // true
console.log("drive" in myCar); // true
```

---

## delete Operator

Removes properties from objects.

```javascript
// Deleting object properties
let user = {
    name: "Alice",
    age: 25,
    email: "alice@email.com"
};

delete user.email;
console.log(user); // { name: "Alice", age: 25 }

console.log(delete user.name); // true (successful deletion)
console.log(user); // { age: 25 }

// Cannot delete non-configurable properties
let obj = {};
Object.defineProperty(obj, "permanent", {
    value: "cannot delete",
    configurable: false
});

console.log(delete obj.permanent); // false
console.log(obj.permanent); // "cannot delete"

// Deleting array elements (creates holes)
let numbers = [1, 2, 3, 4, 5];
delete numbers[2];
console.log(numbers); // [1, 2, empty, 4, 5]
console.log(numbers.length); // 5 (length unchanged)
console.log(2 in numbers); // false

// Cannot delete variables
let x = 10;
console.log(delete x); // false (in strict mode, this throws an error)
```

---

## void Operator

Evaluates an expression and returns `undefined`.

```javascript
// Basic usage
console.log(void 0);        // undefined
console.log(void "hello");  // undefined
console.log(void (2 + 3));  // undefined

// Commonly used to generate undefined
let result = void 0; // safer than using undefined (which can be reassigned in old JS)

// In HTML links to prevent navigation
// <a href="javascript:void(0)" onclick="doSomething()">Click me</a>

// Immediately invoked function expressions (IIFE)
void function() {
    console.log("This runs immediately");
}();

// Arrow functions that shouldn't return values
let numbers = [1, 2, 3];
numbers.forEach(num => void console.log(num)); // Ensures forEach callback returns undefined
```

---

## new Operator

Creates instances of objects.

```javascript
// Built-in constructors
let date = new Date();
let arr = new Array(1, 2, 3);
let regex = new RegExp("\\d+");

// Custom constructors
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.greet = function() {
        return `Hi, I'm ${this.name}`;
    };
}

let person1 = new Person("Alice", 30);
console.log(person1.name); // "Alice"
console.log(person1.greet()); // "Hi, I'm Alice"

// Class constructors
class Animal {
    constructor(species, name) {
        this.species = species;
        this.name = name;
    }
    
    speak() {
        return `${this.name} makes a sound`;
    }
}

let dog = new Animal("dog", "Buddy");
console.log(dog.speak()); // "Buddy makes a sound"

// new.target (ES6)
function MyConstructor() {
    if (new.target) {
        console.log("Called with new");
    } else {
        console.log("Called without new");
    }
}

new MyConstructor(); // "Called with new"
MyConstructor();     // "Called without new"
```

---

## super Operator

Calls parent class methods in inheritance.

```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }
    
    speak() {
        return `${this.name} makes a sound`;
    }
    
    move() {
        return `${this.name} moves`;
    }
}

class Dog extends Animal {
    constructor(name, breed) {
        super(name); // Call parent constructor
        this.breed = breed;
    }
    
    speak() {
        return super.speak() + " - Woof!"; // Call parent method
    }
    
    getInfo() {
        return `${super.move()} and is a ${this.breed}`;
    }
}

let myDog = new Dog("Buddy", "Golden Retriever");
console.log(myDog.speak());   // "Buddy makes a sound - Woof!"
console.log(myDog.getInfo()); // "Buddy moves and is a Golden Retriever"

// Static methods
class MathUtils {
    static multiply(a, b) {
        return a * b;
    }
}

class AdvancedMath extends MathUtils {
    static power(base, exponent) {
        let result = super.multiply(base, base); // Call parent static method
        for (let i = 2; i < exponent; i++) {
            result = super.multiply(result, base);
        }
        return result;
    }
}
```

---

## this Keyword

References the current execution context.

```javascript
// In objects
let person = {
    name: "Alice",
    age: 30,
    greet() {
        return `Hello, I'm ${this.name} and I'm ${this.age} years old`;
    },
    
    // Arrow functions don't have their own 'this'
    greetArrow: () => {
        return `Hello from ${this.name}`; // 'this' refers to global object
    }
};

console.log(person.greet()); // "Hello, I'm Alice and I'm 30 years old"

// Explicit binding
function introduce() {
    return `I'm ${this.name}`;
}

let user1 = { name: "Bob" };
let user2 = { name: "Charlie" };

console.log(introduce.call(user1));  // "I'm Bob"
console.log(introduce.apply(user2)); // "I'm Charlie"

let boundIntroduce = introduce.bind(user1);
console.log(boundIntroduce()); // "I'm Bob"

// In classes
class Counter {
    constructor() {
        this.count = 0;
    }
    
    increment() {
        this.count++;
        return this;
    }
    
    decrement() {
        this.count--;
        return this;
    }
    
    getValue() {
        return this.count;
    }
}

let counter = new Counter();
console.log(
    counter.increment().increment().decrement().getValue()
); // 1 (method chaining)
```

---

## Comma Operator (,)

Evaluates multiple expressions and returns the last one.

```javascript
// Basic usage
let result = (1 + 2, 3 + 4, 5 + 6);
console.log(result); // 11 (last expression)

// In for loops
for (let i = 0, j = 10; i < 5; i++, j--) {
    console.log(`i: ${i}, j: ${j}`);
}

// Variable declarations
let a = 1, b = 2, c = 3;

// Complex expressions
let x = (console.log("First"), console.log("Second"), 42);
// Prints: "First", "Second"
console.log(x); // 42

// Conditional assignment
let condition = true;
let value = condition ? (console.log("True branch"), "yes") : (console.log("False branch"), "no");
// Prints: "True branch"
console.log(value); // "yes"
```

---

## Conditional Assignment Operators

### Logical AND Assignment (&&=)
Assigns only if the left side is truthy.

```javascript
let user = { name: "Alice" };

// Only assign if user exists and is truthy
user &&= { ...user, active: true };
console.log(user); // { name: "Alice", active: true }

let nullUser = null;
nullUser &&= { active: true };
console.log(nullUser); // null (unchanged)

// Equivalent to:
// user = user && { ...user, active: true };
```

### Logical OR Assignment (||=)
Assigns only if the left side is falsy.

```javascript
let settings = { theme: null, volume: 0 };

settings.theme ||= "light";
settings.volume ||= 50;

console.log(settings); // { theme: "light", volume: 50 }

// Equivalent to:
// settings.theme = settings.theme || "light";
```

### Nullish Coalescing Assignment (??=)
Assigns only if the left side is null or undefined.

```javascript
let config = { theme: null, volume: 0, notifications: undefined };

config.theme ??= "dark";
config.volume ??= 100;  // Won't assign (0 is not nullish)
config.notifications ??= true;

console.log(config); // { theme: "dark", volume: 0, notifications: true }
```

---

## BigInt Operators

Work with arbitrarily large integers.

```javascript
// Creating BigInts
let big1 = 123456789012345678901234567890n;
let big2 = BigInt("987654321098765432109876543210");

// Arithmetic operations
console.log(big1 + big2); // 1111111110111111111011111111100n
console.log(big1 - big2); // -864197532086419753208641975320n
console.log(big1 * 2n);   // 246913578024691357802469135780n
console.log(big1 / 3n);   // 41152263004115226300411522630n (truncated)

// Cannot mix BigInt with regular numbers
// console.log(big1 + 10); // TypeError

// Must convert
console.log(big1 + BigInt(10)); // Works
console.log(Number(big1) + 10); // Works (but may lose precision)

// Comparisons
console.log(big1 > big2); // false
console.log(big1 === 123456789012345678901234567890n); // true

// Bitwise operations
let a = 15n; // 1111 in binary
let b = 10n; // 1010 in binary

console.log(a & b); // 10n (1010)
console.log(a | b); // 15n (1111)
console.log(a ^ b); // 5n (0101)
console.log(a << 1n); // 30n
console.log(a >> 1n); // 7n
```

---

## Symbol Operators

Work with unique identifiers.

```javascript
// Creating symbols
let sym1 = Symbol("description");
let sym2 = Symbol("description");
console.log(sym1 === sym2); // false (each symbol is unique)

// Global symbols
let globalSym1 = Symbol.for("shared");
let globalSym2 = Symbol.for("shared");
console.log(globalSym1 === globalSym2); // true

// Using symbols as object keys
let obj = {
    name: "Public property",
    [sym1]: "Private property"
};

console.log(obj.name);  // "Public property"
console.log(obj[sym1]); // "Private property"

// Symbols are not enumerable
console.log(Object.keys(obj)); // ["name"]
console.log(Object.getOwnPropertySymbols(obj)); // [Symbol(description)]

// Well-known symbols
class MyArray {
    constructor(...items) {
        this.items = items;
    }
    
    // Custom iterator
    *[Symbol.iterator]() {
        for (let item of this.items) {
            yield item;
        }
    }
    
    // Custom toString
    [Symbol.toPrimitive](hint) {
        if (hint === "string") {
            return this.items.join(", ");
        }
        return this.items.length;
    }
}

let myArr = new MyArray(1, 2, 3);
console.log([...myArr]); // [1, 2, 3]
console.log(String(myArr)); // "1, 2, 3"
console.log(Number(myArr)); // 3
```

---

## Async/Await Operators

Handle asynchronous operations.

```javascript
// Basic async function
async function fetchData() {
    return "Data fetched!";
}

// Using await
async function processData() {
    try {
        let data = await fetchData();
        console.log(data); // "Data fetched!"
        return data.toUpperCase();
    } catch (error) {
        console.error("Error:", error);
    }
}

// Await with promises
async function apiCall() {
    let response = await fetch("https://api.example.com/data");
    let data = await response.json();
    return data;
}

// Parallel execution
async function fetchMultiple() {
    // Sequential (slower)
    let data1 = await fetchData();
    let data2 = await fetchData();
    
    // Parallel (faster)
    let [result1, result2] = await Promise.all([
        fetchData(),
        fetchData()
    ]);
    
    return { result1, result2 };
}

// Error handling
async function handleErrors() {
    try {
        let result = await riskyOperation();
        return result;
    } catch (error) {
        console.log("Caught error:", error.message);
        throw error; // Re-throw if needed
    } finally {
        console.log("Cleanup code here");
    }
}

// Top-level await (ES2022)
// Can be used at module top level
let data = await fetchData();
console.log(data);
```

---

## Generator Operators

Create functions that can pause and resume execution.

```javascript
// Basic generator
function* numberGenerator() {
    yield 1;
    yield 2;
    yield 3;
    return "Done";
}

let gen = numberGenerator();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
console.log(gen.next()); // { value: 3, done: false }
console.log(gen.next()); // { value: "Done", done: true }

// Generator with parameters
function* paramGenerator() {
    let value = yield "First";
    yield `Received: ${value}`;
    let another = yield "Third";
    return `Final: ${another}`;
}

let paramGen = paramGenerator();
console.log(paramGen.next());       // { value: "First", done: false }
console.log(paramGen.next("Hello")); // { value: "Received: Hello", done: false }
console.log(paramGen.next());       // { value: "Third", done: false }
console.log(paramGen.next("World")); // { value: "Final: World", done: true }

// Infinite generator
function* infiniteNumbers() {
    let i = 0;
    while (true) {
        yield i++;
    }
}

let infinite = infiniteNumbers();
console.log(infinite.next().value); // 0
console.log(infinite.next().value); // 1
console.log(infinite.next().value); // 2

// Generator delegation (yield*)
function* innerGenerator() {
    yield "inner1";
    yield "inner2";
}

function* outerGenerator() {
    yield "outer1";
    yield* innerGenerator(); // Delegate to inner generator
    yield "outer2";
}

let outer = outerGenerator();
console.log([...outer]); // ["outer1", "inner1", "inner2", "outer2"]

// Async generators
async function* asyncGenerator() {
    yield await Promise.resolve("First");
    yield await Promise.resolve("Second");
    yield await Promise.resolve("Third");
}

async function useAsyncGenerator() {
    for await (let value of asyncGenerator()) {
        console.log(value);
    }
}
```

---

## Quick Reference - Advanced Operators

| Operator | Name | Example | Description |
|----------|------|---------|-------------|
| `??` | Nullish Coalescing | `x ?? "default"` | Returns right if left is null/undefined |
| `?.` | Optional Chaining | `obj?.prop?.method?.()` | Safe property/method access |
| `...` | Spread | `[...arr]`, `{...obj}` | Expands iterables |
| `...` | Rest | `function(...args)` | Collects remaining elements |
| `[]` | Destructuring | `[a, b] = arr` | Unpacks array values |
| `{}` | Destructuring | `{x, y} = obj` | Unpacks object properties |
| `` ` `` | Template Literals | `` `Hello ${name}` `` | String interpolation |
| `in` | Property Check | `"prop" in obj` | Checks property existence |
| `delete` | Property Removal | `delete obj.prop` | Removes object properties |
| `void` | Void | `void expression` | Returns undefined |
| `new` | Constructor | `new Class()` | Creates object instances |
| `super` | Parent Access | `super.method()` | Calls parent methods |
| `this` | Context | `this.property` | Current execution context |
| `,` | Comma | `a, b, c` | Evaluates and returns last |
| `&&=` | AND Assignment | `x &&= y` | Assigns if x is truthy |
| `\|\|=` | OR Assignment | `x \|\|= y` | Assigns if x is falsy |
| `??=` | Nullish Assignment | `x ??= y` | Assigns if x is null/undefined |
| `async` | Async Function | `async function()` | Declares async function |
| `await` | Await | `await promise` | Waits for promise resolution |
| `yield` | Generator Yield | `yield value` | Pauses generator execution |
| `yield*` | Generator Delegate | `yield* generator` | Delegates to another generator |

---

## Best Practices

1. **Use optional chaining** to avoid null/undefined errors
2. **Prefer nullish coalescing** over OR for default values when 0 and "" are valid
3. **Use destructuring** to make code more readable and concise
4. **Leverage template literals** for string formatting
5. **Use spread operator** for immutable array/object operations
6. **Apply async/await** for cleaner asynchronous code
7. **Use generators** for lazy evaluation and infinite sequences
8. **Be careful with `this`** - consider arrow functions vs regular functions
9. **Use `in` operator** to safely check property existence
10. **Prefer `const` and destructuring** over multiple variable assignments

Remember: These advanced operators can make your code more concise and expressive, but use them judiciously to maintain readability!
