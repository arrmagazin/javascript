# 10. Error Handling

### Exception Handling

JavaScript provides try-catch-finally blocks for handling runtime errors and exceptions. Proper error handling is crucial for building robust applications.

**Basic Error Handling:**

```javascript
try {
    // Code that might throw an error
    const result = riskyOperation();
    console.log('Success:', result);
} catch (error) {
    // Handle the error
    console.error('Error occurred:', error.message);
} finally {
    // Always executed
    cleanupResources();
}
```

**Error Types:**

- `Error`: Base error class
- `TypeError`: Invalid type operation
- `ReferenceError`: Invalid reference access
- `SyntaxError`: Invalid syntax
- `RangeError`: Value out of range
- `EvalError`: Error in eval()
- `URIError`: URI encoding/decoding error

**Custom Errors:**

```javascript
class ValidationError extends Error {
    constructor(message, field) {
        super(message);
        this.name = 'ValidationError';
        this.field = field;
    }
}

function validateUser(user) {
    if (!user.email) {
        throw new ValidationError('Email is required', 'email');
    }
}
```
