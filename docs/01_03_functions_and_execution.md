# 3. Functions and Execution

### Function Declarations and Expressions

JavaScript supports multiple paradigms for defining functions, each with distinct characteristics and use cases. Understanding these differences is crucial for writing idiomatic JavaScript code.

**Function Declaration:**

```javascript
function greet(name) {
    return `Hello, ${name}!`;
}
```

**Function Expression:**

```javascript
const greet = function(name) {
    return `Hello, ${name}!`;
};
```

**Arrow Functions (ES6):**

```javascript
const greet = (name) => `Hello, ${name}!`;
const greet = name => `Hello, ${name}!`; // Single parameter, no parens
```

**Key Differences:**

- Function declarations are hoisted, allowing calls before definition
- Arrow functions do not have their own `this` binding
- Arrow functions cannot be used as constructors
- Arrow functions have implicit return for single expressions <citation>16,17</citation>

### Execution Context, Scope, Closures, and `this`

**Key Definitions:**

- **Execution Context**: The environment in which JavaScript code is evaluated and executed, containing the current scope, variable bindings, and the value of `this`. Each function call creates a new execution context.
- **Scope**: The region of the program where a variable is accessible. JavaScript uses lexical (static) scoping, meaning scope is determined by the physical location of code in the source. JavaScript has function scope (pre-ES6) and block scope (ES6+ with let/const).
- **Lexical Environment**: An internal JavaScript engine structure that holds identifier-variable mappings and a reference to the outer lexical environment, forming the scope chain.
- **Variable Resolution**: The process of finding where a variable is defined by traversing the scope chain from the current execution context outward.
- **Closure**: A function that has access to variables in its outer (enclosing) scope, even after the outer function has finished executing. Closures "close over" the variables they reference.
- **`this` Binding**: The mechanism that determines the value of the `this` keyword within a function. The binding depends on how the function is called, not where it's defined.
- **Global Object**: The top-level object in JavaScript (window in browsers, global in Node.js) that contains global variables and functions.
- **Module Pattern**: A design pattern that uses closures to create private variables and methods, exposing only a public API.
- **Function Factory**: A function that returns other functions, often using closures to customize the returned function's behavior.
- **Data Encapsulation**: The practice of hiding internal data and implementation details, exposing only necessary interfaces (achieved through closures in JavaScript).

#### Scope and Lexical Environment

JavaScript uses lexical scoping, where the scope of a variable is determined by its location in the source code. Each execution context has a lexical environment that maintains a mapping of identifiers to their values, forming the basis for variable resolution and closure behavior <citation>12</citation>.

#### Closures

A closure is created when a function retains access to variables from its outer (enclosing) scope, even after the outer function has returned. This powerful feature enables data encapsulation, function factories, and the module pattern.

**Closure Example:**

```javascript
function createCounter() {
    let count = 0; // Private variable
    
    return {
        increment() { return ++count; },
        getCount() { return count; }
    };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.increment()); // 2
console.log(counter.getCount());  // 2
```

#### `this` Binding

The behavior of `this` is often a source of confusion for JavaScript developers. The value of `this` depends on how a function is called, not where it's defined.

**`this` Binding Rules:**

| Binding Type | Description | Example |
| -------------- | ------------- | --------- |
| Global | In global scope, `this` is the global object | `console.log(this === window)` // true |
| Method | In object methods, `this` is the object | `obj.method()` // `this` is `obj` |
| Constructor | In constructor calls, `this` is new instance | `new User()` // `this` is new instance |
| Arrow | Arrow functions inherit `this` from enclosing scope | `() => {}` // lexical `this` |

**Manipulating `this`:** The `call()`, `apply()`, and `bind()` methods allow explicit control over `this` binding. The `bind()` method creates a new function with a permanently bound `this` value, while `call()` and `apply()` invoke functions immediately with specified `this` and arguments <citation>11,12</citation>.

### Advanced Function Patterns

**Higher-Order Functions:** Functions that take other functions as arguments or return functions are called higher-order functions. They enable powerful abstraction over behavior.

```javascript
// Function taking a function as argument
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map(n => n * 2);

// Function returning a function
const multiply = (factor) => (number) => number * factor;
const multiplyBy3 = multiply(3);
console.log(multiplyBy3(5)); // 15
```

**Currying:** The technique of converting a function that takes multiple arguments into a sequence of functions each taking a single argument. This enables function composition and partial application <citation>12</citation>.

**Pure Functions:** Functions that always return the same output for the same input and have no side effects. Pure functions are easier to test, debug, and reason about, making them ideal for functional programming approaches.
