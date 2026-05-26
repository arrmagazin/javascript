
### Proxy Object and Reflect API

The Proxy object enables you to create a proxy for another object, which can intercept and redefine fundamental operations for that object. The Reflect API provides methods for interceptable JavaScript operations, working hand-in-hand with Proxy.

**Proxy Creation:**

```javascript
const target = {
    name: 'John',
    age: 30
};

const handler = {
    get(target, property, receiver) {
        console.log(`Getting ${property}`);
        return Reflect.get(target, property, receiver);
    },
    set(target, property, value, receiver) {
        console.log(`Setting ${property} to ${value}`);
        return Reflect.set(target, property, value, receiver);
    }
};

const proxy = new Proxy(target, handler);

proxy.name; // "Getting name" then "John"
proxy.age = 31; // "Setting age to 31"
```

**Common Proxy Traps:**

| Trap | Description | Use Case |
| ------ | ------------- | ---------- |
| `get` | Intercept property reading | Validation, logging, computed properties |
| `set` | Intercept property writing | Validation, type checking, side effects |
| `has` | Intercept `in` operator | Hiding properties, virtual properties |
| `deleteProperty` | Intercept `delete` | Preventing deletion, cleanup |
| `apply` | Intercept function calls | Logging, caching, access control |
| `construct` | Intercept `new` calls | Constructor validation, singleton enforcement |

**Validation with Proxy:**

```javascript
function createValidator(target, schema) {
    return new Proxy(target, {
        set(target, property, value) {
            if (schema[property]) {
                const validator = schema[property];
                if (!validator(value)) {
                    throw new Error(`Invalid value for ${property}`);
                }
            }
            return Reflect.set(target, property, value);
        }
    });
}

const user = createValidator({}, {
    age: value => typeof value === 'number' && value >= 0,
    email: value => typeof value === 'string' && value.includes('@')
});

user.age = 25;    // OK
user.email = 'john@example.com'; // OK
user.age = -5;    // Error: Invalid value for age
```

**Reflect API Methods:**

The Reflect API provides static methods that correspond to proxy traps:

```javascript
// Property operations
Reflect.get(target, property, receiver)
Reflect.set(target, property, value, receiver)
Reflect.has(target, property)
Reflect.deleteProperty(target, property)

// Function operations
Reflect.apply(target, thisArg, args)
Reflect.construct(target, args, newTarget)

// Object operations
Reflect.getOwnPropertyDescriptor(target, property)
Reflect.defineProperty(target, property, descriptor)
Reflect.getPrototypeOf(target)
Reflect.setPrototypeOf(target, prototype)
Reflect.preventExtensions(target)
Reflect.isExtensible(target)
Reflect.ownKeys(target)
```

**Advanced Proxy Patterns:**

**Observable Objects:**

```javascript
function createObservable(target, callback) {
    return new Proxy(target, {
        set(target, property, value) {
            const result = Reflect.set(target, property, value);
            callback(property, value);
            return result;
        }
    });
}

const person = createObservable({ name: 'John' }, (prop, value) => {
    console.log(`${prop} changed to ${value}`);
});

person.name = 'Jane'; // "name changed to Jane"
```

**Negative Array Index Support:**

```javascript
function createArray(arr) {
    return new Proxy(arr, {
        get(target, property) {
            const index = parseInt(property);
            if (!isNaN(index) && index < 0) {
                return target[target.length + index];
            }
            return Reflect.get(target, property);
        }
    });
}

const arr = createArray([1, 2, 3, 4, 5]);
console.log(arr[-1]); // 5
console.log(arr[-2]); // 4
```

**Key Benefits:**

- **Metaprogramming**: Intercept and customize object behavior
- **Validation**: Enforce constraints on object properties
- **Logging/Debugging**: Track object interactions
- **Backward Compatibility**: Polyfill new features
- **Performance**: Lazy loading and caching

**Performance Considerations:**

- Proxy operations are slower than direct object access
- Use proxies judiciously for hot code paths
- Consider alternatives like getters/setters for simple cases
