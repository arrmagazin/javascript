# 7. Regular Expressions

### RegExp Fundamentals

Regular expressions are patterns used to match character combinations in strings. They provide powerful string manipulation capabilities for validation, parsing, and text processing.

**RegExp Creation:**

```javascript
// Literal notation
const pattern = /hello/gim;

// Constructor
const pattern = new RegExp('hello', 'gim');
```

**Flags:**

| Flag | Description |
| ------ | ------------- |
| `g` | Global (find all matches) |
| `i` | Case-insensitive |
| `m` | Multiline |
| `s` | Dotall (. matches newlines) |
| `u` | Unicode |
| `y` | Sticky |

### Common Patterns

**Character Classes:**

| Pattern | Matches |
| --------- | --------- |
| `.` | Any character except newline |
| `\d` | Digit [0-9] |
| `\D` | Non-digit |
| `\w` | Word character [a-zA-Z0-9_] |
| `\W` | Non-word character |
| `\s` | Whitespace |
| `\S` | Non-whitespace |

**Quantifiers:**

| Pattern | Matches |
| --------- | --------- |
| `*` | 0 or more |
| `+` | 1 or more |
| `?` | 0 or 1 |
| `{n}` | Exactly n |
| `{n,}` | n or more |
| `{n,m}` | Between n and m |

**Groups and Ranges:**

```javascript
// Capture group
const match = "2024-01-15".match(/(\d{4})-(\d{2})-(\d{2})/);
// match[0] = "2024-01-15"
// match[1] = "2024", match[2] = "01", match[3] = "15"

// Non-capturing group
"hello123world".match(/(?:\d+)/); // Non-capturing

// Lookahead and lookbehind
const password = "password123";
password.match(/(?=.*[A-Z])/); // Positive lookahead
password.match(/(?<!123)$/);   // Positive lookbehind
```

**Greedy vs Lazy Matching:**

```javascript
const text = "a1b2c3";
text.match(/\d+/g);   // Greedy: ["1", "2", "3"]
text.match(/\d+?/g);  // Lazy: ["1", "2", "3"]
```
