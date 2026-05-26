# 12. Built-in Objects and APIs

### Array Methods

Arrays in JavaScript have powerful methods for manipulation and iteration.

**Mutation Methods:**

```javascript
const arr = [1, 2, 3, 4, 5];

// Add/remove elements
arr.push(6);        // [1, 2, 3, 4, 5, 6]
arr.pop();          // [1, 2, 3, 4, 5]
arr.unshift(0);     // [0, 1, 2, 3, 4, 5]
arr.shift();        // [1, 2, 3, 4, 5]

// Modify array
arr.splice(2, 1, 'a', 'b'); // [1, 2, 'a', 'b', 4, 5]
arr.reverse();      // [5, 4, 'b', 'a', 2, 1]
arr.sort();         // [1, 2, 4, 5, 'a', 'b']
```

**Non-mutation Methods:**

```javascript
const arr = [1, 2, 3, 4, 5];

// Transformation
const doubled = arr.map(x => x * 2);        // [2, 4, 6, 8, 10]
const evens = arr.filter(x => x % 2 === 0); // [2, 4]
const sum = arr.reduce((acc, x) => acc + x, 0); // 15

// Searching
const found = arr.find(x => x > 3);         // 4
const index = arr.findIndex(x => x > 3);    // 3
const includes = arr.includes(3);           // true

// Iteration
arr.forEach(x => console.log(x));           // Logs each element
const joined = arr.join('-');               // "1-2-3-4-5"
```

### String Methods

Strings have methods for manipulation and searching.

```javascript
const str = "Hello, World!";

// Searching
str.indexOf('World');     // 7
str.includes('World');    // true
str.startsWith('Hello');  // true
str.endsWith('!');        // true

// Extraction
str.slice(7, 12);         // "World"
str.substring(7, 12);     // "World"
str.substr(7, 5);         // "World"

// Modification
str.toUpperCase();        // "HELLO, WORLD!"
str.toLowerCase();        // "hello, world!"
str.trim();               // "Hello, World!"
str.replace('World', 'Universe'); // "Hello, Universe!"

// Splitting/Joining
str.split(', ');          // ["Hello", "World!"]
```

### Math and Date Objects

**Math Object:**

```javascript
Math.PI;                    // 3.141592653589793
Math.E;                     // 2.718281828459045

Math.round(4.7);           // 5
Math.ceil(4.1);            // 5
Math.floor(4.9);           // 4
Math.trunc(4.9);           // 4

Math.max(1, 2, 3, 4, 5);  // 5
Math.min(1, 2, 3, 4, 5);  // 1
Math.random();             // Random number 0-1
Math.sqrt(16);             // 4
Math.pow(2, 3);            // 8
```

**Date Object:**

```javascript
// Current date/time
const now = new Date();

// Specific date
const birthday = new Date('1990-01-01');

// Getters
now.getFullYear();         // 2024
now.getMonth();            // 0-11
now.getDate();             // 1-31
now.getDay();              // 0-6 (Sunday = 0)
now.getHours();            // 0-23

// Setters
now.setFullYear(2025);
now.setMonth(11);          // December

// Formatting
now.toISOString();         // "2024-01-15T10:30:00.000Z"
now.toLocaleDateString();  // "1/15/2024"
now.toLocaleTimeString();  // "10:30:00 AM"

// Timestamps
Date.now();                // Current timestamp
now.getTime();             // Timestamp for date
```

### JSON Handling

JSON (JavaScript Object Notation) is a lightweight data interchange format.

```javascript
const user = {
    name: "John",
    age: 30,
    hobbies: ["reading", "coding"]
};

// Serialize to JSON
const jsonString = JSON.stringify(user);
// '{"name":"John","age":30,"hobbies":["reading","coding"]}'

// Parse from JSON
const parsedUser = JSON.parse(jsonString);

// Custom serialization
const customJSON = JSON.stringify(user, (key, value) => {
    if (key === 'age') return value + 1; // Increment age
    return value;
});

// Pretty printing
const prettyJSON = JSON.stringify(user, null, 2);
```
