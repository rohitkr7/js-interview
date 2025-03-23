In JavaScript, the `map`, `filter`, and `reduce` functions are **higher-order functions** available on arrays. They are used to process and transform data in a declarative and functional programming style.

---

### **1. `map`**
The `map` function is used to **transform** each element of an array. It applies a given function to every element and returns a new array with the transformed elements.

#### Syntax:
```javascript
array.map(callback(element, index, array))
```

- **`callback`**: A function that is called for each element in the array.
- **Returns**: A new array with the transformed elements.

#### Example:
```javascript
const numbers = [1, 2, 3, 4, 5];

// Multiply each number by 2
const doubled = numbers.map(num => num * 2);

console.log(doubled); // Output: [2, 4, 6, 8, 10]
```

---

### **2. `filter`**
The `filter` function is used to **select elements** from an array based on a condition. It applies a predicate (a function that returns `true` or `false`) to each element and includes only those elements that satisfy the condition.

#### Syntax:
```javascript
array.filter(callback(element, index, array))
```

- **`callback`**: A function that is called for each element in the array and returns `true` to include the element or `false` to exclude it.
- **Returns**: A new array with the elements that satisfy the condition.

#### Example:
```javascript
const numbers = [1, 2, 3, 4, 5];

// Select only even numbers
const evenNumbers = numbers.filter(num => num % 2 === 0);

console.log(evenNumbers); // Output: [2, 4]
```

---

### **3. `reduce`**
The `reduce` function is used to **combine all elements** of an array into a single value. It applies a reducer function to each element, accumulating the result.

#### Syntax:
```javascript
array.reduce(callback(accumulator, currentValue, index, array), initialValue)
```

- **`callback`**: A function that is called for each element in the array.
  - **`accumulator`**: The running total or accumulated value.
  - **`currentValue`**: The current element being processed.
- **`initialValue`**: The initial value of the accumulator (optional).
- **Returns**: A single value.

#### Example:
```javascript
const numbers = [1, 2, 3, 4, 5];

// Sum all the numbers
const sum = numbers.reduce((acc, num) => acc + num, 0);

console.log(sum); // Output: 15
```

---

### **Combining `map`, `filter`, and `reduce`**
You can chain these functions together to perform complex operations on arrays.

#### Example:
Find the sum of squares of even numbers:
```javascript
const numbers = [1, 2, 3, 4, 5];

const sumOfSquares = numbers
  .filter(num => num % 2 === 0)  // Select even numbers
  .map(num => num * num)         // Square each number
  .reduce((acc, num) => acc + num, 0); // Sum the squares

console.log(sumOfSquares); // Output: 20 (2^2 + 4^2)
```

---

### **Differences Between `map`, `filter`, and `reduce`**

| Function  | Purpose                                | Input Type         | Output Type        |
|-----------|----------------------------------------|--------------------|--------------------|
| `map`     | Transforms each element               | Callback function  | New array          |
| `filter`  | Filters elements based on a condition | Predicate function | New array          |
| `reduce`  | Combines elements into a single value | Reducer function   | Single value       |

---

### **Use Cases**
1. **`map`**:
   - Transforming data (e.g., converting an array of numbers to their squares).
   - Extracting specific properties from objects.

2. **`filter`**:
   - Selecting elements based on conditions (e.g., filtering even numbers or valid users).

3. **`reduce`**:
   - Aggregating data (e.g., summing numbers, finding the maximum value, or flattening arrays).

---

### **Summary**
- **`map`**: Transforms each element and returns a new array.
- **`filter`**: Selects elements based on a condition and returns a new array.
- **`reduce`**: Combines all elements into a single value.

These functions are powerful tools for working with arrays in JavaScript, enabling concise and readable functional programming.