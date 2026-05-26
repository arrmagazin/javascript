# 15. Performance Optimization Basics

### Efficient Code Patterns

**Avoid unnecessary work:**

```javascript
// Inefficient
for (let i = 0; i < arr.length; i++) {
    // arr.length recalculated every iteration
}

// Efficient
const len = arr.length;
for (let i = 0; i < len; i++) {
    // Use cached length
}
```

**Use appropriate data structures:**

```javascript
// For frequent lookups, use Set/Map instead of arrays
const items = new Set([1, 2, 3, 4, 5]);
items.has(3); // O(1) vs O(n) for array.includes()
```

### Profiling and Debugging

**Performance monitoring:**

```javascript
// High-resolution timing
const start = performance.now();
// ... code to measure ...
const end = performance.now();
console.log(`Operation took ${end - start} milliseconds`);

// Memory usage (Node.js)
console.log(process.memoryUsage());
```

**Common performance pitfalls:**

- Excessive DOM manipulation
- Memory leaks from event listeners
- Inefficient algorithms (O(n²) vs O(n))
- Large bundle sizes
- Synchronous operations blocking the main thread
