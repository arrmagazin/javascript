# 4. Asynchronous JavaScript

### Callbacks and the Callback Pattern

The callback pattern is the foundation of asynchronous JavaScript, where a function is passed as an argument to be executed once an operation completes. However, deeply nested callbacks can lead to "callback hell"—difficult-to-read and maintain code.

**Callback Hell Example:**

```javascript
fetchData(data => {
    processData(data, result => {
        saveResult(result, () => {
            notifyUser(() => {
                console.log('Complete!');
            });
        });
    });
});
```

**Best Practices for Callbacks:**

- Keep callback functions small and focused
- Handle errors as the first argument (Node.js convention)
- Consider using named functions instead of anonymous callbacks for better stack traces <citation>11</citation>

### Promises

Promises provide a cleaner way to handle asynchronous operations, representing a value that may be available now, in the future, or never. A Promise exists in one of three states: pending, fulfilled, or rejected.

**Promise Lifecycle:**

```
                    +-----------+
                    |  Pending  |
                    +-----------+
                         |
           +-------------+-------------+
           |                           |
           v                           v
    +-------------+             +-------------+
    |   Fulfilled |             |   Rejected  |
    +-------------+             +-------------+
```

**Promise Methods:**

| Method | Description |
| -------- | ------------- |
| `Promise.all()` | Waits for all promises to fulfill |
| `Promise.allSettled()` | Waits for all promises to settle |
| `Promise.any()` | Returns first fulfilled promise |
| `Promise.race()` | Returns first settled promise |
| `Promise.resolve()` | Creates resolved promise |
| `Promise.reject()` | Creates rejected promise |

**Promise Chaining:**

```javascript
fetchData()
    .then(processData)
    .then(saveResult)
    .then(notifyUser)
    .catch(handleError);
```

### Async/Await

ES2017 introduced `async` functions and the `await` keyword, providing syntactic sugar over Promises that makes asynchronous code look and behave more like synchronous code.

**Async Function Syntax:**

```javascript
async function processData() {
    try {
        const data = await fetchData();
        const result = await processData(data);
        await saveResult(result);
        return 'Success!';
    } catch (error) {
        console.error('Error:', error);
        throw error;
    }
}
```

**Key Points:**

- `async` functions always return Promises
- `await` pauses execution until the Promise resolves
- `try/catch` handles rejections
- Multiple `await` statements can run sequentially or in parallel using `Promise.all()` <citation>11,12</citation>
