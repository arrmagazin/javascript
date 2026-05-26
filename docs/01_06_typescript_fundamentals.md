# 6. TypeScript Fundamentals

### Type System Overview

TypeScript extends JavaScript with a static type system that catches errors at compile time rather than runtime. Understanding TypeScript's type system is essential for building scalable applications <citation>39,40</citation>.

**Basic Types:**

```typescript
let isDone: boolean = false;
let decimal: number = 6;
let color: string = "blue";
let list: number[] = [1, 2, 3];
let tuple: [string, number] = ["hello", 10];
let any: any = "could be anything";
let unknown: unknown = "uncertain type";
let void: undefined = undefined;
let never: never = throw new Error();
```

### Advanced Types

**Union and Intersection Types:**

```typescript
type stringOrNumber = string | number;
type stringAndNumber = string & number; // Intersection

function format(value: stringOrNumber): string {
    return typeof value === 'number' 
        ? value.toFixed(2) 
        : value.trim();
}
```

**Generic Types:** Enable writing flexible, reusable code that works with multiple types <citation>41,42</citation>.

```typescript
function identity<T>(arg: T): T {
    return arg;
}

const numberIdentity = identity<number>(5);
const stringIdentity = identity<string>("hello");

// Generic constraints
interface Lengthwise {
    length: number;
}

function logLength<T extends Lengthwise>(item: T): void {
    console.log(item.length);
}
```

**Utility Types:** TypeScript provides several utility types for common type transformations:

| Utility Type | Description | Example |
| -------------- | ------------- | --------- |
| `Partial<T>` | All properties optional | `Partial<User>` |
| `Required<T>` | All properties required | `Required<User>` |
| `Omit<T, K>` | Exclude properties | `Omit<User, 'password'>` |
| `Pick<T, K>` | Select properties | `Pick<User, 'name' | 'email'>` |
| `Exclude<T, U>` | Exclude from union | `Exclude<'a' | 'b', 'a'>` |
| `ReturnType<T>` | Function return type | `ReturnType<typeof func>` |
