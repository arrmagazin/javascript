# 14. Memory Management

### Garbage Collection

JavaScript uses automatic garbage collection to manage memory. The garbage collector periodically frees memory occupied by objects that are no longer reachable.

**Memory Lifecycle:**

1. Allocate memory for objects
2. Use allocated memory
3. Release allocated memory when no longer needed

**Common Memory Leaks:**

```javascript
// Global variables
globalVar = 'This creates a global variable';

// Forgotten timers
setInterval(() => {
    // This callback and its closure are never garbage collected
}, 1000);

// Detached DOM references
const element = document.getElementById('myElement');
element.remove(); // Element removed from DOM but still referenced

// Closures capturing large objects
function createLargeClosure() {
    const largeArray = new Array(1000000);
    return () => {
        console.log(largeArray.length); // Keeps largeArray alive
    };
}
```

### Weak References

WeakMap and WeakSet use weak references, allowing garbage collection of keys/values.

```javascript
const weakMap = new WeakMap();
let key = { id: 1 };
weakMap.set(key, 'value');

// If key is no longer referenced elsewhere, it can be garbage collected
key = null; // weakMap entry may be removed by GC
```
