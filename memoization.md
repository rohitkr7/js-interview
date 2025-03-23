A **memoization** function in JavaScript is used to optimize expensive function calls by caching the results of previous computations. If the function is called again with the same arguments, the cached result is returned instead of recomputing it.

Here’s an example of a `memoize` function:

---

### **Example: Memoizing a Function**
```javascript
function memoize(fn) {
    const cache = new Map(); // Cache to store results

    return function (...args) {
        const key = JSON.stringify(args); // Use arguments as the cache key
        if (cache.has(key)) {
            console.log("Fetching from cache:", key);
            return cache.get(key); // Return cached result
        }

        console.log("Computing result for:", key);
        const result = fn(...args); // Compute the result
        cache.set(key, result); // Store the result in the cache
        return result;
    };
}

// Example: Expensive computation (e.g., factorial)
function factorial(n) {
    if (n === 0 || n === 1) return 1;
    return n * factorial(n - 1);
}

// Memoized version of the factorial function
const memoizedFactorial = memoize(factorial);

console.log(memoizedFactorial(5)); // Computes and returns 120
console.log(memoizedFactorial(5)); // Fetches from cache and returns 120
console.log(memoizedFactorial(6)); // Computes and returns 720
console.log(memoizedFactorial(6)); // Fetches from cache and returns 720
```

---

### **How It Works**
1. **`memoize` Function**:
   - Takes a function (`fn`) as input.
   - Returns a new function that wraps the original function with caching logic.

2. **Cache**:
   - A `Map` is used to store the results of previous computations.
   - The arguments of the function are serialized (using `JSON.stringify`) to create a unique key for the cache.

3. **Logic**:
   - If the cache contains the result for the given arguments, it returns the cached result.
   - Otherwise, it computes the result, stores it in the cache, and then returns it.

---

### **Example: Memoizing a Fibonacci Function**
The Fibonacci sequence is a classic example where memoization can significantly improve performance.

#### Without Memoization:
```javascript
function fibonacci(n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

console.log(fibonacci(40)); // Takes a long time to compute
```

#### With Memoization:
```javascript
const memoizedFibonacci = memoize(function (n) {
    if (n <= 1) return n;
    return memoizedFibonacci(n - 1) + memoizedFibonacci(n - 2);
});

console.log(memoizedFibonacci(40)); // Much faster due to caching
console.log(memoizedFibonacci(40)); // Fetches result from cache
```

---

### **Benefits of Memoization**
1. **Performance Optimization**:
   - Reduces redundant computations for functions with repeated calls and the same inputs.
2. **Reusability**:
   - The `memoize` function can be applied to any pure function (a function that always produces the same output for the same input).

---

### **Limitations**
1. **Memory Usage**:
   - The cache can grow indefinitely if not managed properly.
   - You can implement a **cache size limit** or use a **WeakMap** for better memory management.

2. **Non-Pure Functions**:
   - Memoization works best with pure functions (functions without side effects). It may not work correctly with functions that depend on external state.

---

### **Improved Memoization with Cache Size Limit**
Here’s an enhanced version of `memoize` with a cache size limit:

```javascript
function memoizeWithLimit(fn, limit = 5) {
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

        // Remove the oldest entry if the cache exceeds the limit
        if (cache.size > limit) {
            const oldestKey = cache.keys().next().value;
            cache.delete(oldestKey);
        }

        return result;
    };
}

// Example usage
const memoizedAdd = memoizeWithLimit((a, b) => a + b, 3);
console.log(memoizedAdd(1, 2)); // Computes and returns 3
console.log(memoizedAdd(1, 2)); // Fetches from cache and returns 3
console.log(memoizedAdd(2, 3)); // Computes and returns 5
console.log(memoizedAdd(3, 4)); // Computes and returns 7
console.log(memoizedAdd(4, 5)); // Computes and returns 9 (oldest cache entry removed)
```

---

### **Summary**
- **Memoization** is a technique to cache the results of expensive function calls.
- Use the `memoize` function to wrap any pure function for caching.
- It is especially useful for recursive functions like Fibonacci or factorial.
- Manage cache size to avoid memory issues in long-running applications.