# 5. Classes and Object-Oriented Programming

### Class Syntax

ES6 introduced class syntax as a cleaner way to implement inheritance.
Classes provide a more familiar OOP paradigm for developers coming from other languages.

**Class Declaration:**

```javascript
class User {
    // Constructor
    constructor(name, email) {
        this.name = name;
        this._email = email; // Convention for internal use
    }
    
    // Instance method
    greet() {
        return `Hello, I'm ${this.name}`;
    }
    
    // Getter
    get email() {
        return this._email;
    }
    
    // Setter
    set email(newEmail) {
        if (newEmail.includes('@')) {
            this._email = newEmail;
        }
    }
    
    // Static method
    static createAnonymous() {
        return new User('Anonymous', 'anon@example.com');
    }
}
```

### Inheritance and Access Modifiers

**Inheritance:**

```javascript
class Admin extends User {
    constructor(name, email, permissions) {
        super(name, email); // Call parent constructor
        this.permissions = permissions;
    }
    
    deleteUser(user) {
        console.log(`Deleting user: ${user.name}`);
    }
}
```

**Access Modifiers:** Modern JavaScript supports private class fields using the `#` prefix, providing true encapsulation at the class level <citation>11</citation>.

```javascript
class BankAccount {
    #balance = 0;
    
    constructor(initialBalance) {
        this.#balance = initialBalance;
    }
    
    getBalance() {
        return this.#balance;
    }
    
    deposit(amount) {
        if (amount > 0) {
            this.#balance += amount;
        }
    }
}
```

### Design Patterns

**Singleton Pattern:** Ensures only one instance of a class exists throughout the application.

```javascript
class Singleton {
    constructor() {
        if (Singleton.instance) {
            return Singleton.instance;
        }
        Singleton.instance = this;
        this.data = [];
    }
}
```
