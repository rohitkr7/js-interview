In JavaScript, **prototype** is a mechanism by which objects inherit properties and methods from other objects. Every JavaScript object has an internal property called `[[Prototype]]`, which points to another object. This is used to implement **prototypal inheritance**.

---

### **Key Concepts**

1. **Prototype Property (`prototype`)**:
   - Functions in JavaScript (specifically constructor functions) have a special property called `prototype`.
   - This `prototype` property is an object that is shared among all instances created by the constructor function.
   - You can add methods or properties to the `prototype` object, and they will be available to all instances.

2. **`__proto__`**:
   - Every object has an internal `[[Prototype]]` property, which can be accessed using the `__proto__` property (though it's not recommended to use directly).
   - This property points to the prototype object from which the object inherits.

3. **Prototype Chain**:
   - If a property or method is not found on an object, JavaScript looks for it in the object's prototype. If it's not found there, it continues up the prototype chain until it reaches `null`.

---

### **Example: Using Prototype**

#### Constructor Function Example:
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

// Adding a method to the prototype
Person.prototype.greet = function () {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
};

// Creating instances
const person1 = new Person("Alice", 25);
const person2 = new Person("Bob", 30);

person1.greet(); // Output: Hello, my name is Alice and I am 25 years old.
person2.greet(); // Output: Hello, my name is Bob and I am 30 years old.
```

- Here, the `greet` method is defined on the `Person.prototype` object, and all instances of `Person` share this method.

---

### **Prototype Chain**

#### Example:
```javascript
const obj = { a: 1 };

// Check the prototype of obj
console.log(obj.__proto__); // Output: {} (Object.prototype)

// Check the prototype of Object.prototype
console.log(Object.prototype.__proto__); // Output: null (end of the chain)
```

- When you access a property on `obj`, JavaScript first looks for it on `obj`. If it doesn't find it, it looks at `obj.__proto__` (i.e., `Object.prototype`).

---

### **Adding Methods to Built-In Prototypes**
You can add methods to built-in prototypes like `Array` or `String`. However, this is generally discouraged because it can lead to unexpected behavior.

#### Example:
```javascript
Array.prototype.sum = function () {
    return this.reduce((acc, val) => acc + val, 0);
};

const numbers = [1, 2, 3, 4];
console.log(numbers.sum()); // Output: 10
```

---

### **Prototype vs `__proto__`**

| **Property**   | **Description**                                                                 |
|-----------------|---------------------------------------------------------------------------------|
| `prototype`     | A property of constructor functions. Used to define methods and properties for instances. |
| `__proto__`     | A property of objects that points to the prototype object they inherit from.    |

---

### **Class Syntax and Prototype**
When you use the `class` syntax in JavaScript, it is essentially syntactic sugar over the prototype system.

#### Example:
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    greet() {
        console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
    }
}

const person1 = new Person("Alice", 25);
person1.greet(); // Output: Hello, my name is Alice and I am 25 years old.
```

- Behind the scenes, the `greet` method is added to `Person.prototype`.

---

### **Checking Prototypes**
You can check an object's prototype using:
1. **`Object.getPrototypeOf(obj)`**:
   ```javascript
   const obj = {};
   console.log(Object.getPrototypeOf(obj)); // Output: Object.prototype
   ```

2. **`instanceof`**:
   ```javascript
   console.log(person1 instanceof Person); // Output: true
   ```

---

### **Summary**
- **Prototype** is a mechanism for inheritance in JavaScript.
- Objects inherit properties and methods from their prototype.
- The `prototype` property is used to define shared methods for instances created by a constructor function.
- The `__proto__` property (or `Object.getPrototypeOf`) points to an object's prototype.
- Modern JavaScript uses `class` syntax, but it is built on top of the prototype system.

Similar code found with 1 license type