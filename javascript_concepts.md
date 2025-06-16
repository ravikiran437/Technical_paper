# JavaScript Concepts 

---

## 1. What are the different data types in JavaScript?

JavaScript has the following data types:

**Primitive Types**:
- `String`
- `Number`
- `Boolean`
- `undefined`
- `null`
- `Symbol`
- `BigInt`

**Non-Primitive Type**:
- `Object` (includes arrays, functions, dates, etc.)

---

## 2. What is the difference between `let`, `var`, and `const`?

- `var`: Function-scoped, can be re-declared and updated.
- `let`: Block-scoped, cannot be re-declared in the same scope, but can be updated.
- `const`: Block-scoped, cannot be re-declared or updated.

---

## 3. Why should we not use `var`?

- `var` is function-scoped and can lead to **hoisting-related bugs**.
- It allows **re-declaration**, which can cause unexpected behaviors.

---

## 4. Why is using global variables considered bad?

- They can be **modified from anywhere** in the code.
- They **increase the chance of name conflicts**.
- They **hinder modular and maintainable code**.

---

## 5. What are truthy and falsy values?

**Falsy values** in JavaScript:
- `false`
- `0`
- `""` (empty string)
- `null`
- `undefined`
- `NaN`

Everything else is **truthy**.

---

## 6. What is function hoisting?

Function declarations are hoisted to the top of their scope.  
This means you can call the function before its declaration.

```js
sayHello(); // Works

function sayHello() {
  console.log("Hello!");
}
```

---

## 7. What happens when a function does not have a return statement?

It returns `undefined` by default.

---

## 8. What are the different ways of declaring a function?

- Function declaration
- Function expression
- Arrow function
- Constructor function using `Function` (not recommended)

---

## 9. What is the difference between pass by reference and pass by value?

- **Primitive values**: Passed **by value**.
- **Objects and arrays**: Passed **by reference**.

---

## 10. What are the different types of `for` loops?

- `for` (traditional loop)
- `for...in` (iterates over keys/indexes)
- `for...of` (iterates over values)
- `forEach` (array method for iteration)

---

## 11. How to search documentation on MDN?

Use Google or MDN directly:
```
site:developer.mozilla.org array map
```

---

## 12. Popular array utility methods?

- `map()`
- `filter()`
- `reduce()`
- `forEach()`
- `find()`
- `some()`, `every()`
- `includes()`
- `concat()`, `slice()`, `splice()`

---

## 13. Popular string utility methods?

- `split()`
- `replace()`
- `toUpperCase()`, `toLowerCase()`
- `includes()`
- `substring()`, `slice()`
- `trim()`
- `startsWith()`, `endsWith()`

---

## 14. Popular object utility methods?

- `Object.keys()`
- `Object.values()`
- `Object.entries()`
- `Object.assign()`
- `hasOwnProperty()`
- Spread `{ ...obj }`

---

## 15. When to use `forEach` vs `map`, `filter`, `reduce`?

- Use `forEach` for **side-effects**.
- Use `map` to **transform data**.
- Use `filter` to **select data**.
- Use `reduce` to **accumulate** values.

---

## 16. What are immutable vs mutable methods?

- **Immutable**: Do not change original data (e.g., `map`, `filter`, `slice`)
- **Mutable**: Change original data (e.g., `push`, `pop`, `splice`)

---

## 17. How does error handling work using `try...catch`?

```js
try {
  // code that might throw
} catch (error) {
  console.error(error.message);
}
```

---

## 18. How to throw custom errors?

```js
throw new Error("Something went wrong");
```

---

## 19. Difference between `throw new Error("msg")` vs `throw "msg"`?

- `throw new Error("msg")`: Standard way, provides a **stack trace**.
- `throw "msg"`: Throws a **string**, lacks detailed info.

---

## 20. How to read error messages and trace from stack trace?

- Read the **error type and message**.
- Trace the **file and line number**.
- Understand **call stack** to find where it went wrong.

---

## 21. What is the importance of the `catch` block?

- Prevents app crash.
- Allows graceful error handling and debugging.
- Can log and recover from issues.

---

## 22. What is the spread operator?

```js
const arr1 = [1, 2];
const arr2 = [...arr1, 3]; // [1, 2, 3]
```

---

## 23. What are template literals?

Use backticks `` and `${}` for embedding:

```js
let name = "Ravi";
console.log(`Hello, ${name}`);
```

---

## 24. What are default parameters?

```js
function greet(name = "Guest") {
  console.log(`Hello, ${name}`);
}
```

---

## 25. What is destructuring?

```js
const obj = { a: 1, b: 2 };
const { a, b } = obj;
```

---

## 26. What are closures?

A function "remembers" variables from its outer scope even after that scope is gone.

```js
function outer() {
  let count = 0;
  return function inner() {
    count++;
    console.log(count);
  };
}
```

---

## 27. Difference between arrow functions and regular functions?

| Feature              | Arrow Function             | Regular Function        |
|----------------------|----------------------------|-------------------------|
| `this` context       | Lexical                    | Dynamic                 |
| `arguments` object   | Not available              | Available               |
| Use as constructor   | ❌                         | ✅                      |

---

## 28. Difference between `===` and `==`?

- `===`: Strict equality (checks type and value)
- `==`: Loose equality (allows type coercion)

```js
"5" == 5   // true
"5" === 5  // false
```

---

## 29. Why is `value === undefined` better than `!value`?

- `!value` checks for falsy values (`0`, `""`, `null`, `undefined`)
- `value === undefined` is **explicit**, safer when `0` or `""` is valid

---

## 30. What is method chaining in arrays?

```js
arr.filter(...).map(...).reduce(...)
```

Calls multiple methods in sequence on the result.

---

## 31. Difference between `null` and `undefined`?

- `undefined`: Variable declared but not assigned.
- `null`: Intentionally set as "no value".

---

## 32. How to import/export using `require` and `module.exports`?

**In exporting file:**
```js
module.exports = { funcA, funcB };
```

**In importing file:**
```js
const { funcA } = require('./file');
```

---

## 33. What are the different `console` methods?

- `console.log()`
- `console.error()`
- `console.warn()`
- `console.info()`
- `console.table()`
- `console.time()` / `console.timeEnd()`

---

## 34. What are some JavaScript best practices?

- Use `let` and `const`
- Use meaningful variable names
- Use consistent indentation (2 or 4 spaces)
- Avoid global variables
- Use arrow functions where appropriate
- Avoid deeply nested callbacks

---

## 35. How to pass functions as arguments and call them?

```js
function greet(callback) {
  callback();
}

greet(() => console.log("Hello"));
```

---

## 36. Difference between named and anonymous functions?

- **Named**: Has a name, helpful in debugging.
- **Anonymous**: No name, often used as arguments.

---

## 37. How to handle variable number of arguments?

Use **rest parameters**:

```js
function sum(...nums) {
  return nums.reduce((a, b) => a + b, 0);
}
```

Or use `arguments` object in regular functions.

---
