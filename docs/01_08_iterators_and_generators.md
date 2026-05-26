# 8. Iterators and Generators

### Iterator Protocol

Iterators provide a standardized way to traverse data structures. An iterator is an object with a `next()` method that returns `{value, done}` objects.

**Iterator Example:**

```javascript
const iterable = {
    [Symbol.iterator]() {
        let step = 0;
        return {
            next() {
                step++;
                if (step <= 3) {
                    return { value: step, done: false };
                }
                return { value: undefined, done: true };
            }
        };
    }
};

for (const num of iterable) {
    console.log(num); // 1, 2, 3
}
```

### Generators

Generators are functions that can pause and resume execution, yielding multiple values over time. They simplify iterator creation and enable new control flow patterns <citation>11,12</citation>.

**Generator Function:**

```javascript
function* numberGenerator() {
    yield 1;
    yield 2;
    yield 3;
}

const gen = numberGenerator();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
console.log(gen.next()); // { value: 3, done: false }
console.log(gen.next()); // { value: undefined, done: true }
```

**Advanced Generator Patterns:**

```javascript
// Infinite sequence
function* infiniteNumbers() {
    let n = 0;
    while (true) {
        yield n++;
    }
}

// Delegating to other generators
function* combine() {
    yield* [1, 2, 3];
    yield* [4, 5, 6];
}

// Sending values into generators
function* inputGenerator() {
    const a = yield 'First';
    const b = yield 'Second';
    return a + b;
}

const gen = inputGenerator();
gen.next();      // { value: 'First', done: false }
gen.next(10);    // { value: 'Second', done: false }
gen.next(20);    // { value: 30, done: true }
```
