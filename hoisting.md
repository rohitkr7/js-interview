### **What is Hoisting in JavaScript?**

**Hoisting** is a JavaScript mechanism where variable and function declarations are moved to the top of their containing scope (script or function) during the compilation phase, before the code is executed. This means you can use variables and functions before they are declared in the code.

However, **only declarations are hoisted**, not initializations or assignments.

---

### **How Hoisting Works**

#### **1. Variable Hoisting**
Variables declared with `var` are hoisted to the top of their scope and initialized with `undefined`. Variables declared with `let` and `const` are also hoisted, but they are not initialized and remain in the **Temporal Dead Zone (TDZ)** until the code execution reaches their declaration.

#### Example with `var`:
```javascript
console.log(a); // Output: undefined
var a = 10;
console.log(a); // Output: 10
```

- **What Happens Internally**:
  ```javascript
  var a; // Declaration is hoisted
  console.log(a); // undefined
  a = 10; // Initialization happens here
  console.log(a); // 10
  ```

#### Example with `let` and `const`:
```javascript
console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 20;

console.log(c); // ReferenceError: Cannot access 'c' before initialization
const c = 30;
```

- Variables declared with `let` and `const` are hoisted but remain in the **Temporal Dead Zone (TDZ)** until their declaration is encountered.

---

#### **2. Function Hoisting**
Function declarations are fully hoisted, meaning you can call the function before it is defined in the code.

#### Example:
```javascript
greet(); // Output: Hello, World!

function greet() {
    console.log("Hello, World!");
}
```

- **What Happens Internally**:
  ```javascript
  function greet() {
      console.log("Hello, World!");
  }

  greet(); // Hello, World!
  ```

#### Function Expressions:
Function expressions (both regular and arrow functions) are not hoisted in the same way as function declarations. Only the variable declaration is hoisted, not the function definition.

#### Example:
```javascript
sayHello(); // TypeError: sayHello is not a function
var sayHello = function () {
    console.log("Hello!");
};
```

- **What Happens Internally**:
  ```javascript
  var sayHello; // Declaration is hoisted
  sayHello(); // TypeError: sayHello is not a function
  sayHello = function () {
      console.log("Hello!");
  };
  ```

---

### **Key Points About Hoisting**
1. **Declarations Are Hoisted**:
   - Variable and function declarations are hoisted to the top of their scope.
   - For `var`, the variable is initialized to `undefined`.
   - For `let` and `const`, the variable is not initialized and remains in the **Temporal Dead Zone (TDZ)**.

2. **Initializations Are Not Hoisted**:
   - Only the declaration is hoisted, not the assignment or initialization.

3. **Function Declarations Are Fully Hoisted**:
   - You can call a function declared with `function` before its definition.

4. **Function Expressions Are Not Fully Hoisted**:
   - Only the variable declaration is hoisted, not the function definition.

---

### **Examples to Illustrate Hoisting**

#### **Example 1: Variable Hoisting with `var`**
```javascript
console.log(x); // Output: undefined
var x = 5;
console.log(x); // Output: 5
```

#### **Example 2: Variable Hoisting with `let` and `const`**
```javascript
console.log(y); // ReferenceError: Cannot access 'y' before initialization
let y = 10;

console.log(z); // ReferenceError: Cannot access 'z' before initialization
const z = 15;
```

#### **Example 3: Function Hoisting**
```javascript
sayHi(); // Output: Hi!

function sayHi() {
    console.log("Hi!");
}
```

#### **Example 4: Function Expression Hoisting**
```javascript
sayHello(); // TypeError: sayHello is not a function
var sayHello = function () {
    console.log("Hello!");
};
```

#### **Example 5: Hoisting in a Block Scope**
```javascript
{
    console.log(a); // ReferenceError: Cannot access 'a' before initialization
    let a = 10;
}
```

---

### **How to Avoid Confusion with Hoisting**
1. **Use `let` and `const`**:
   - Avoid using `var` to declare variables, as it can lead to unexpected behavior due to hoisting.
   - `let` and `const` are block-scoped and do not initialize until their declaration is encountered.

2. **Declare Variables at the Top**:
   - Always declare variables at the top of their scope to make the code more predictable and readable.

3. **Use Function Declarations Carefully**:
   - Be mindful of where you define and call functions.

---

### **Summary**
- **Hoisting** is JavaScript's behavior of moving declarations to the top of their scope during the compilation phase.
- Variables declared with `var` are hoisted and initialized to `undefined`.
- Variables declared with `let` and `const` are hoisted but remain in the **Temporal Dead Zone (TDZ)** until their declaration.
- Function declarations are fully hoisted, but function expressions are not.
- To avoid confusion, use `let` and `const` for variables and declare them at the top of their scope.