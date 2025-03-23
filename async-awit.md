### **What are `async` and `await` in JavaScript?**

`async` and `await` are modern JavaScript features introduced in ES2017 (ES8) that simplify working with asynchronous code. They provide a cleaner and more readable way to handle Promises, making asynchronous code look and behave more like synchronous code.

---

### **Key Concepts**

1. **`async`**:
   - Declares a function as asynchronous.
   - An `async` function always returns a **Promise**.
   - Inside an `async` function, you can use the `await` keyword.

2. **`await`**:
   - Pauses the execution of an `async` function until the Promise is resolved or rejected.
   - Can only be used inside an `async` function.

---

### **Why Use `async/await`?**
- **Improved Readability**: Makes asynchronous code easier to read and understand compared to chaining `.then()` and `.catch()`.
- **Error Handling**: Allows you to use `try...catch` for handling errors, making error handling more consistent.

---

### **Basic Syntax**

#### Declaring an `async` Function:
```javascript
async function myAsyncFunction() {
    // Asynchronous code here
}
```

#### Using `await`:
```javascript
async function myAsyncFunction() {
    const result = await somePromise; // Waits for the Promise to resolve
    console.log(result);
}
```

---

### **Examples**

#### **1. Basic Example**
```javascript
function fetchData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => resolve("Data fetched!"), 2000);
    });
}

async function getData() {
    console.log("Fetching data...");
    const data = await fetchData(); // Waits for the Promise to resolve
    console.log(data); // Output: "Data fetched!"
}

getData();
```

**Output**:
```
Fetching data...
(Data fetched after 2 seconds)
Data fetched!
```

---

#### **2. Error Handling with `try...catch`**
```javascript
function fetchDataWithError() {
    return new Promise((resolve, reject) => {
        setTimeout(() => reject("Error fetching data!"), 2000);
    });
}

async function getData() {
    try {
        const data = await fetchDataWithError(); // Waits for the Promise to resolve
        console.log(data);
    } catch (error) {
        console.error(error); // Output: "Error fetching data!"
    }
}

getData();
```

---

#### **3. Sequential Execution**
Using `await`, you can execute asynchronous operations sequentially.

```javascript
function fetchData1() {
    return new Promise((resolve) => setTimeout(() => resolve("Data 1 fetched"), 1000));
}

function fetchData2() {
    return new Promise((resolve) => setTimeout(() => resolve("Data 2 fetched"), 2000));
}

async function getData() {
    const data1 = await fetchData1(); // Waits for fetchData1 to resolve
    console.log(data1); // Output: "Data 1 fetched"

    const data2 = await fetchData2(); // Waits for fetchData2 to resolve
    console.log(data2); // Output: "Data 2 fetched"
}

getData();
```

---

#### **4. Parallel Execution**
You can execute multiple asynchronous operations in parallel using `Promise.all`.

```javascript
function fetchData1() {
    return new Promise((resolve) => setTimeout(() => resolve("Data 1 fetched"), 1000));
}

function fetchData2() {
    return new Promise((resolve) => setTimeout(() => resolve("Data 2 fetched"), 2000));
}

async function getData() {
    const [data1, data2] = await Promise.all([fetchData1(), fetchData2()]);
    console.log(data1); // Output: "Data 1 fetched"
    console.log(data2); // Output: "Data 2 fetched"
}

getData();
```

---

### **Key Points**

1. **`async` Functions Always Return a Promise**:
   - If you return a value from an `async` function, it is automatically wrapped in a Promise.
   ```javascript
   async function example() {
       return "Hello!";
   }

   example().then((result) => console.log(result)); // Output: "Hello!"
   ```

2. **`await` Can Only Be Used Inside `async` Functions**:
   - Using `await` outside an `async` function will throw a syntax error.
   ```javascript
   const result = await somePromise; // SyntaxError: await is only valid in async functions
   ```

3. **Error Handling**:
   - Use `try...catch` to handle errors in `async` functions.
   - If an error is not caught, the Promise returned by the `async` function will be rejected.

4. **Mixing `async/await` with Promises**:
   - You can mix `async/await` with `.then()` and `.catch()` if needed, but it’s better to stick to one style for consistency.

---

### **Comparison: `async/await` vs Promises**

| **Feature**               | **Promises**                                   | **`async/await`**                              |
|---------------------------|-----------------------------------------------|-----------------------------------------------|
| **Readability**           | Can become hard to read with nested `.then()`. | Cleaner and more readable, looks synchronous. |
| **Error Handling**        | Use `.catch()` for errors.                     | Use `try...catch` for errors.                 |
| **Chaining**              | Requires chaining `.then()` calls.            | Sequential code with `await`.                 |
| **Parallel Execution**    | Use `Promise.all()`.                          | Use `Promise.all()` with `await`.             |

---

### **When to Use `async/await`**
1. When you want cleaner, more readable asynchronous code.
2. When you need to handle errors using `try...catch`.
3. When you have sequential asynchronous operations.

---

### **Summary**
- **`async`**: Declares a function as asynchronous and ensures it returns a Promise.
- **`await`**: Pauses the execution of an `async` function until a Promise is resolved or rejected.
- Use `try...catch` for error handling in `async` functions.
- Combine `Promise.all` with `await` for parallel execution.

`async/await` is a powerful tool for writing asynchronous code in a clean and readable way, making it easier to manage complex workflows.