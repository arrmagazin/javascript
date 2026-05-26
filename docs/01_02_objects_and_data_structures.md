# 2. Objects and Data Structures

### Object Creation Patterns

JavaScript objects are collections of key-value pairs that serve as the primary data structure for organizing and managing related data. Several patterns exist for object creation, each suited to different use cases.

**Object Literals:** The most common approach uses inline notation with curly braces, allowing rapid creation of objects with properties and methods.

```javascript
const user = {
    name: "John",
    age: 30,
    greet() {
        return `Hello, ${this.name}`;
    }
};
```

**Constructor Functions:** Traditional OOP-style object creation uses functions as constructors, with the `new` keyword creating instances that inherit from the constructor's prototype.

```javascript
function User(name, age) {
    this.name = name;
    this.age = age;
}

User.prototype.greet = function() {
    return `Hello, ${this.name}`;
};

const user = new User("John", 30);
```

**Object.create():** This method explicitly sets the prototype of a new object, enabling prototype-based inheritance without constructor functions <citation>11,12</citation>.

### Property Management

Objects in JavaScript support rich property management through various methods and descriptors that control how properties behave at a fundamental level.

**Property Descriptors:** Every object property has attributes that control its behavior—`writable` (can be changed), `enumerable` (appears in loops), and `configurable` (can be deleted or modified). The `Object.defineProperty()` method allows fine-grained control over these attributes.

**Special Methods for Property Operations:**

| Method | Purpose |
| -------- | --------- |
| `Object.keys()` | Returns enumerable property names |
| `Object.values()` | Returns property values (ES2017) |
| `Object.entries()` | Returns [key, value] pairs (ES2017) |
| `Object.assign()` | Copies properties from source objects |
| `Object.freeze()` | Makes object immutable |
| `Object.seal()` | Prevents adding/removing properties |

**Getters and Setters:** These special methods allow computed properties and controlled property access, enabling validation, formatting, or side effects when properties are read or written <citation>11</citation>.

### Prototype System

JavaScript's prototype-based inheritance is a unique feature that distinguishes it from classical OOP languages. Every JavaScript object has a prototype from which it inherits properties and methods. This system enables efficient memory usage through property sharing and dynamic method modification.

**Prototype Chain Visualization:**

```
user instance
    |
    +--[[Prototype]]--> User.prototype
                            |
                            +--[[Prototype]]--> Object.prototype
                                                    |
                                                    +--[[Prototype]]--> null
```

**Working with Prototypes:** The `prototype` property on functions defines what inherited members new instances will have. The `__proto__` accessor (deprecated in favor of `Object.getPrototypeOf()` and `Object.setPrototypeOf()`) provides access to an object's prototype <citation>12</citation>.

### Special Object Types

JavaScript provides several specialized object types for specific use cases:

| Type | Description | Use Case |
| ------ | ------------- | ---------- |
| `Array` | Ordered collections with index access | Lists, queues, stacks |
| `Map` | Key-value pairs with any key type | When keys aren't strings |
| `Set` | Unique values collection | Removing duplicates |
| `WeakMap` | Map with weakly referenced keys | Private data, memory management |
| `WeakSet` | Set with weakly referenced values | Tracking objects without preventing GC |
| `Date` | Date and time operations | Timestamp handling |
| `RegExp` | Pattern matching | String validation, parsing |
| `Symbol` | Unique immutable primitives | Property keys, constants |
| `BigInt` | Arbitrary precision integers | Financial calculations |
