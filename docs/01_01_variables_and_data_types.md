# 1. Variables and Data Types

### Variable Declarations

JavaScript provides three ways to declare variables, each with distinct scoping behaviors that are crucial for writing maintainable code. Understanding the differences between `var`, `let`, and `const` is fundamental to mastering JavaScript development.

| Declaration | Scope | Hoisting | Reassignment | Re-declaration |
| ------------- | ------- | ---------- | -------------- | ---------------- |
| `var` | Function-scoped | Yes | Allowed | Allowed |
| `let` | Block-scoped | Temporal Dead Zone | Allowed | Not Allowed |
| `const` | Block-scoped | Temporal Dead Zone | Not Allowed | Not Allowed |

The `var` keyword has been part of JavaScript since its inception and exhibits function-level scoping. Variables declared with `var` are hoisted to the top of their containing function or global scope, initialized with `undefined`. This behavior can lead to unexpected results, particularly in loops with closures. The `let` and `const` keywords were introduced in ES6 (ECMAScript 2015) to address these scoping issues by providing block-level scoping. The "Temporal Dead Zone" refers to the period between the beginning of the scope and the point where the variable is declared—attempting to access a `let` or `const` variable during this period throws a ReferenceError <citation>11,12</citation>.

### Primitive Types

JavaScript's primitive types represent the fundamental building blocks of data in the language. Each primitive type has unique characteristics and methods that developers must understand to write effective code.

**String Types and Templates:** Strings in JavaScript are immutable sequences of Unicode characters. ES6 introduced template literals, denoted by backticks (`` ` ``), which enable multi-line strings, string interpolation using `${expression}` syntax, and improved readability for complex string constructions <citation>14,16</citation>.

```javascript
// Traditional string concatenation
const greeting = "Hello, " + name + "!";

// Template literal syntax
const greeting = `Hello, ${name}!`;
```

**Numeric Types:** JavaScript uses IEEE 754 double-precision floating-point format for all numeric values, encompassing integers, floating-point numbers, `BigInt` for arbitrarily large integers, and special values like `NaN` (Not a Number) and `Infinity`. The `parseInt()` and `parseFloat()` functions provide explicit parsing from strings, while `Number.isNaN()` and `Number.isFinite()` offer type-safe checks <citation>11</citation>.

**Boolean and Truthiness:** JavaScript's boolean type has only two values: `true` and `false`. However, the concept of "truthiness" is crucial—values like `0`, `""`, `null`, `undefined`, `NaN`, and `false` are falsy, while all other values are truthy. This behavior impacts conditional statements and logical operations significantly.
Null and Undefined

JavaScript distinguishes between two special values that represent the absence of data, though they differ in origin and use cases.

**Undefined:** A variable that has been declared but not assigned a value is `undefined`. Functions with no explicit return statement also return `undefined`. The `undefined` type serves as the default value for uninitialized variables and missing function parameters.

**Null:** The `null` value represents an intentional absence of value, explicitly assigned by developers. Unlike `undefined`, `null` must be deliberately set and indicates a conscious decision that a variable has no value.

| Aspect | undefined | null |
| -------- | ----------- | ------ |
| Type | `undefined` | `object` (quirk in JavaScript) |
| Cause | Uninitialized variables, missing returns | Explicitly assigned |
| Falsy | Yes | Yes |
| `== null` | `true` (null == undefined) | `true` |
| `=== null` | `false` | `true` |

Both values are falsy and will evaluate to `false` in boolean contexts. The loose equality operator (`==`) treats them as equal, but strict equality (`===`) distinguishes them. For practical purposes, use `undefined` for system defaults and `null` for explicit "no value" assignments <citation>11,16</citation>.

### Type Coercion

Type coercion occurs when JavaScript automatically converts values from one type to another. Understanding the difference between implicit and explicit coercion is essential for avoiding subtle bugs.

| Operator | Behavior |
| ---------- | ---------- |
| `==` | Loose equality with type coercion |
| `===` | Strict equality without type coercion |
| `!=` | Loose inequality with type coercion |
| `!==` | Strict inequality without type coercion |

The loose equality operator (`==`) performs type coercion before comparison, which can lead to unexpected results. For example, `"" == 0` evaluates to `true`. The strict equality operator (`===`) compares both type and value without coercion, making it the preferred choice in modern JavaScript development <citation>16,17</citation>.
