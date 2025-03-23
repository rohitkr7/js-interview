# **JavaScript Concepts and Examples**

## **Table of Contents**
1. [Async/Await](async-awit.md)
2. [Temporal Dead Zone (TDZ)](var-let-const-comparision.md)
3. [Prototype in JavaScript](prototype.md)
4. [Polyfill for `map` Function](polyfill-map.md)
5. [Memoization](memoization.md)
6. [Private Functions in JavaScript](private-functions.md)
7. [`apply()` Function](apply-fuction.md)
8. [Class in JavaScript](hoisting.md)
9. [Inheritance in JavaScript](hoisting.md)
10. [Currying](closure.md)
11. [Map, Filter, and Reduce](map-filter-reduce.md)

---

## **1. `async/await`**
`async/await` is a modern way to handle asynchronous operations in JavaScript. It makes asynchronous code look and behave more like synchronous code.

### Example:
```javascript
async function fetchData() {
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve("Data fetched!");
        }, 2000);
    });
}

async function getData() {
    try {
        const data = await fetchData(); // Waits for the Promise to resolve
        console.log(data); // Output: "Data fetched!"
    } catch (error) {
        console.error(error); // Handles any errors
    }
}

getData();
```

---

## **2. Temporal Dead Zone (TDZ)**
The **Temporal Dead Zone (TDZ)** is the time between when a variable is declared (using `let` or `const`) and when it is initialized. Accessing the variable during this period results in a `ReferenceError`.

### Example:
```javascript
console.log(myVar); // Output: undefined (no TDZ for `var`)
var myVar = 10;

console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization
let myLet = 20;

console.log(myConst); // ReferenceError: Cannot access 'myConst' before initialization
const myConst = 30;
```

---

## **3. Prototype in JavaScript**
The **prototype** is a mechanism by which objects inherit properties and methods from other objects.

### Example:
```javascript
function Person(name, age) {
    this.name = name;
    this.age = age;
}

Person.prototype.greet = function () {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
};

const person1 = new Person("Alice", 25);
person1.greet(); // Output: Hello, my name is Alice and I am 25 years old.
```

---

## **4. Polyfill for `map` Function**
A polyfill for the `Array.prototype.map` function ensures compatibility with older JavaScript environments.

### Polyfill:
```javascript
if (!Array.prototype.map) {
    Array.prototype.map = function (callback, thisArg) {
        if (this == null) {
            throw new TypeError("Array.prototype.map called on null or undefined");
        }

        if (typeof callback !== "function") {
            throw new TypeError(callback + " is not a function");
        }

        const result = [];
        const array = Object(this);
        const len = array.length >>> 0;

        for (let i = 0; i < len; i++) {
            if (i in array) {
                result[i] = callback.call(thisArg, array[i], i, array);
            }
        }

        return result;
    };
}
```

### Example Usage:
```javascript
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(num => num * 2);
console.log(doubled); // Output: [2, 4, 6, 8]
```

---

## **5. Memoization**
Memoization is a technique to optimize expensive function calls by caching the results of previous computations.

### Example:
```javascript
function memoize(fn) {
    const cache = new Map();

    return function (...args) {
        const key = JSON.stringify(args);
        if (cache.has(key)) {
            console.log("Fetching from cache:", key);
            return cache.get(key);
        }

        console.log("Computing result for:", key);
        const result = fn(...args);
        cache.set(key, result);
        return result;
    };
}

const memoizedFactorial = memoize(function factorial(n) {
    if (n === 0 || n === 1) return 1;
    return n * factorial(n - 1);
});

console.log(memoizedFactorial(5)); // Computes and returns 120
console.log(memoizedFactorial(5)); // Fetches from cache and returns 120
```

---

## **6. Private Functions in JavaScript**
Private functions can be implemented using closures, the `#` syntax (ES2022+), or modules.

### Using `#` Syntax (ES2022+):
```javascript
class MyClass {
    #privateFunction() {
        console.log("This is a private function.");
    }

    publicFunction() {
        console.log("This is a public function.");
        this.#privateFunction();
    }
}

const obj = new MyClass();
obj.publicFunction(); // Output: This is a public function. This is a private function.
// obj.#privateFunction(); // Error: Private field '#privateFunction' must be declared in an enclosing class
```

---

## **7. `apply()` Function**
The `apply()` method allows you to call a function with a specified `this` value and arguments provided as an array.

### Example:
```javascript
function greet(greeting, punctuation) {
    console.log(`${greeting}, ${this.name}${punctuation}`);
}

const person = { name: "Alice" };
greet.apply(person, ["Hello", "!"]); // Output: Hello, Alice!
```

---

## **8. Class in JavaScript**
A class is a blueprint for creating objects. It can include properties and methods.

### Example:
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

---

## **9. Inheritance in JavaScript**
You can use the `extends` keyword to inherit one class from another.

### Example:
```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }

    speak() {
        console.log(`${this.name} makes a sound.`);
    }
}

class Dog extends Animal {
    speak() {
        console.log(`${this.name} barks.`);
    }
}

const dog = new Dog("Buddy");
dog.speak(); // Output: Buddy barks.
```

---

## **10. Currying**
Currying is a technique where a function is transformed into a sequence of functions, each taking a single argument.

### Example:
```javascript
const add = a => b => c => a + b + c;

console.log(add(1)(2)(3)); // Output: 6
```

---

## **11. Map, Filter, and Reduce**
These are higher-order functions used to process arrays.

### Example:
```javascript
const numbers = [1, 2, 3, 4, 5];

// Map: Transform each element
const doubled = numbers.map(num => num * 2);
console.log(doubled); // Output: [2, 4, 6, 8, 10]

// Filter: Select elements based on a condition
const evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // Output: [2, 4]

// Reduce: Combine elements into a single value
const sum = numbers.reduce((acc, num) => acc + num, 0);
console.log(sum); // Output: 15
```

---

### **Summary**
This document covers key JavaScript concepts such as `async/await`, prototypes, polyfills, memoization, private functions, and more. Each section includes examples for easy reference and practical understanding.