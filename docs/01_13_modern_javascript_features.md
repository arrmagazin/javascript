# 13. Modern JavaScript Features

### Destructuring

Destructuring allows unpacking values from arrays or properties from objects into distinct variables.

**Array Destructuring:**

```javascript
const [first, second, ...rest] = [1, 2, 3, 4, 5];
// first = 1, second = 2, rest = [3, 4, 5]

const [a, , c] = [1, 2, 3];
// a = 1, c = 3 (skip second element)
```

**Object Destructuring:**

```javascript
const { name, age, hobbies } = user;
// Equivalent to: const name = user.name; etc.

const { name: fullName, age: userAge = 18 } = user;
// Rename and default value

const { address: { city } } = user;
// Nested destructuring
```

**Parameter Destructuring:**

```javascript
function greet({ name, age }) {
    return `Hello ${name}, you are ${age} years old`;
}

greet({ name: "John", age: 30 }); // "Hello John, you are 30 years old"
```

### Spread and Rest Operators

**Spread Operator (...):**

```javascript
// Arrays
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2]; // [1, 2, 3, 4, 5, 6]

// Objects
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const merged = { ...obj1, ...obj2 }; // { a: 1, b: 2, c: 3, d: 4 }

// Function calls
Math.max(...[1, 2, 3, 4, 5]); // 5
```

**Rest Operator (...):**

```javascript
// Function parameters
function sum(...numbers) {
    return numbers.reduce((acc, n) => acc + n, 0);
}
sum(1, 2, 3, 4, 5); // 15

// Array destructuring
const [first, ...rest] = [1, 2, 3, 4, 5];
// first = 1, rest = [2, 3, 4, 5]

// Object destructuring
const { name, ...otherProps } = user;
// name = user.name, otherProps = rest of properties
```

### Optional Chaining and Nullish Coalescing

**Optional Chaining (?.):**

```javascript
// Instead of: user && user.address && user.address.city
const city = user?.address?.city;

// With function calls
const result = obj?.method?.();

// With arrays
const firstItem = arr?.[0];
```

**Nullish Coalescing (??):**

```javascript
// Returns right operand only if left is null or undefined
const value = null ?? 'default';     // 'default'
const value2 = 0 ?? 'default';       // 0 (not nullish)
const value3 = '' ?? 'default';      // '' (not nullish)
```
