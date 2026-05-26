# 9. Execution Model

### JavaScript Runtime Architecture

JavaScript's execution model is built on several key components that work together to process code efficiently. Understanding this model is crucial for writing performant JavaScript applications <citation>11</citation>.

**Runtime Components:**

```
┌─────────────────────────────────────────┐
│           JavaScript Runtime            │
├─────────────────────────────────────────┤
│  ┌─────────────────────────────────┐    │
│  │           Heap Memory           │    │
│  │  (Objects, closures, data)      │    │
│  └─────────────────────────────────┘    │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │        Call Stack (Thread)      │    │
│  │  - Execution contexts           │    │
│  │  - Function calls               │    │
│  │  - Stack frames                 │    │
│  └─────────────────────────────────┘    │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │        Job Queue / Event        │    │
│  │        Loop (RunLoop)           │    │
│  │  - Microtask queue (Promises)   │    │
│  │  - Macrotask queue (timers, IO) │    │
│  └─────────────────────────────────┘    │
│                                         │
│  ┌─────────────────────────────────┐    │
│  │          Web APIs / Node        │    │
│  │  - DOM operations               │    │
│  │  - Timers (setTimeout)          │    │
│  │  - Network requests (fetch)     │    │
│  │  - File system (Node.js)        │    │
│  └─────────────────────────────────┘    │
└─────────────────────────────────────────┘
```

### Event Loop

The event loop is the mechanism that allows JavaScript to perform non-blocking operations despite being single-threaded. It processes tasks from the queue, executing them one at a time while delegating I/O operations to browser/Node.js APIs.

**Execution Order:**

1. Execute current synchronous code
2. Process all microtasks (Promise callbacks)
3. Process one macrotask from the queue
4. Render if needed (browser)
5. Repeat

**Key Timers and Scheduling:**

| API | Purpose |
| ----- | --------- |
| `setTimeout(callback, delay)` | Execute after delay |
| `setInterval(callback, delay)` | Execute repeatedly |
| `requestAnimationFrame()` | Execute before next paint |
| `setImmediate()` | Execute in next iteration (Node.js) |

**Debounce and Throttle:**

```javascript
// Debounce - execute after calls stop
function debounce(fn, delay) {
    let timeoutId;
    return (...args) => {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => fn(...args), delay);
    };
}

// Throttle - execute at most every N ms
function throttle(fn, limit) {
    let inThrottle;
    return (...args) => {
        if (!inThrottle) {
            fn(...args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}
```

### Module Systems

JavaScript supports multiple module systems, each with different loading semantics and use cases.

**CommonJS (Node.js):**

```javascript
// Exporting
module.exports = { myFunction, myVariable };

// Importing
const { myFunction } = require('./myModule');
```

**ES Modules (ESM):**

```javascript
// Exporting
export const myVariable = 42;
export function myFunction() {}

// Importing
import { myVariable, myFunction } from './myModule.js';

// Default export
import defaultExport from './myModule.js';
```

**Key Differences:**

- ESM is statically analyzable (tree-shaking friendly)
- ESM uses async loading, CommonJS is synchronous
- ESM has `import`/`export`, CommonJS uses `require`/`module.exports`
- ESM runs in strict mode by default <citation>11,12</citation>
