### **What are Promises in JavaScript?**

A **Promise** in JavaScript is an object that represents the eventual completion (or failure) of an asynchronous operation and its resulting value. Promises provide a cleaner and more robust way to handle asynchronous operations compared to traditional callback-based approaches, avoiding issues like **callback hell**.

---

### **States of a Promise**
A Promise can be in one of the following states:
1. **Pending**: The initial state, neither fulfilled nor rejected.
2. **Fulfilled**: The operation completed successfully, and the promise has a resulting value.
3. **Rejected**: The operation failed, and the promise has a reason for the failure.

Once a promise is either fulfilled or rejected, it is considered **settled**, and its state cannot change.

---

### **Creating a Promise**
You can create a promise using the `Promise` constructor, which takes a function (called the executor) with two parameters: `resolve` and `reject`.

#### Example:
```javascript
const myPromise = new Promise((resolve, reject) => {
    const success = true;

    if (success) {
        resolve("Operation was successful!");
    } else {
        reject("Operation failed.");
    }
});
```

---

### **Consuming a Promise**
You can consume a promise using the `.then()`, `.catch()`, and `.finally()` methods.

#### Example:
```javascript
myPromise
    .then((result) => {
        console.log(result); // Output: "Operation was successful!"
    })
    .catch((error) => {
        console.error(error); // Output: "Operation failed." (if rejected)
    })
    .finally(() => {
        console.log("Promise settled."); // Always executed
    });
```

---

### **Chaining Promises**
Promises can be chained to perform a sequence of asynchronous operations.

#### Example:
```javascript
const fetchData = new Promise((resolve, reject) => {
    setTimeout(() => resolve("Data fetched"), 1000);
});

fetchData
    .then((data) => {
        console.log(data); // Output: "Data fetched"
        return "Processing data";
    })
    .then((processedData) => {
        console.log(processedData); // Output: "Processing data"
        return "Data processed";
    })
    .then((finalResult) => {
        console.log(finalResult); // Output: "Data processed"
    })
    .catch((error) => {
        console.error(error); // Handles any errors in the chain
    });
```

---

### **Error Handling in Promises**
Errors in promises can be caught using `.catch()`. If an error occurs in any part of the chain, it will propagate to the nearest `.catch()`.

#### Example:
```javascript
const myPromise = new Promise((resolve, reject) => {
    setTimeout(() => reject("Something went wrong!"), 1000);
});

myPromise
    .then((result) => {
        console.log(result);
    })
    .catch((error) => {
        console.error(error); // Output: "Something went wrong!"
    });
```

---

### **Promise Methods**

#### **1. `Promise.all()`**
- Takes an array of promises and resolves when all promises are resolved.
- If any promise is rejected, it immediately rejects with that error.

#### Example:
```javascript
const promise1 = Promise.resolve(10);
const promise2 = Promise.resolve(20);
const promise3 = Promise.resolve(30);

Promise.all([promise1, promise2, promise3])
    .then((results) => {
        console.log(results); // Output: [10, 20, 30]
    })
    .catch((error) => {
        console.error(error);
    });
```

---

#### **2. `Promise.race()`**
- Resolves or rejects as soon as the first promise in the array settles (either fulfilled or rejected).

#### Example:
```javascript
const promise1 = new Promise((resolve) => setTimeout(() => resolve("First"), 1000));
const promise2 = new Promise((resolve) => setTimeout(() => resolve("Second"), 500));

Promise.race([promise1, promise2])
    .then((result) => {
        console.log(result); // Output: "Second"
    });
```

---

#### **3. `Promise.allSettled()`**
- Waits for all promises to settle (either fulfilled or rejected) and returns an array of their results.

#### Example:
```javascript
const promise1 = Promise.resolve("Success");
const promise2 = Promise.reject("Error");
const promise3 = Promise.resolve("Another success");

Promise.allSettled([promise1, promise2, promise3])
    .then((results) => {
        console.log(results);
        // Output:
        // [
        //   { status: "fulfilled", value: "Success" },
        //   { status: "rejected", reason: "Error" },
        //   { status: "fulfilled", value: "Another success" }
        // ]
    });
```

---

#### **4. `Promise.any()`**
- Resolves as soon as any promise in the array is fulfilled.
- If all promises are rejected, it rejects with an `AggregateError`.

#### Example:
```javascript
const promise1 = Promise.reject("Error 1");
const promise2 = Promise.resolve("Success");
const promise3 = Promise.reject("Error 2");

Promise.any([promise1, promise2, promise3])
    .then((result) => {
        console.log(result); // Output: "Success"
    })
    .catch((error) => {
        console.error(error);
    });
```

---

### **Using Promises with `async/await`**
Promises can be consumed more cleanly using `async/await`.

#### Example:
```javascript
function fetchData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => resolve("Data fetched"), 1000);
    });
}

async function getData() {
    try {
        const data = await fetchData(); // Waits for the promise to resolve
        console.log(data); // Output: "Data fetched"
    } catch (error) {
        console.error(error);
    }
}

getData();
```

---

### **Advantages of Promises**
1. **Improved Readability**:
   - Promises make asynchronous code easier to read and maintain compared to nested callbacks.
2. **Error Handling**:
   - Centralized error handling using `.catch()`.
3. **Chaining**:
   - Promises allow chaining multiple asynchronous operations in a clean and structured way.

---

### **Disadvantages of Promises**
1. **Complexity**:
   - While better than callbacks, promises can still become complex in deeply nested scenarios.
2. **Debugging**:
   - Debugging promises can sometimes be tricky, especially when errors are not properly caught.

---

### **Summary**
- Promises are a powerful way to handle asynchronous operations in JavaScript.
- They have three states: **pending**, **fulfilled**, and **rejected**.
- Use `.then()`, `.catch()`, and `.finally()` to consume promises.
- Methods like `Promise.all()`, `Promise.race()`, and `Promise.any()` provide additional functionality for working with multiple promises.
- Promises work seamlessly with `async/await` for cleaner and more readable asynchronous code.

Similar code found with 1 license type