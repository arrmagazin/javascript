# 11. Strict Mode

Strict mode is a way to opt into a restricted variant of JavaScript that catches common coding mistakes and prevents certain error-prone features.

**Enabling Strict Mode:**

```javascript
// Global strict mode
'use strict';

function myFunction() {
    'use strict'; // Function-level strict mode
    // Strict code here
}
```

**Key Restrictions:**

- Eliminates silent errors (throws errors instead)
- Prevents accidental global variable creation
- Disallows duplicate property names in objects
- Makes eval() safer
- Throws error on invalid delete operations
- Requires function parameters to be unique
