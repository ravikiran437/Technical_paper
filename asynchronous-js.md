# Asynchronous JavaScript Concepts

## How JavaScript Executes Code

JavaScript is a **single-threaded** language, meaning it can execute one task at a time in a sequential order. It uses a **synchronous execution model** for the main thread and a **non-blocking asynchronous model** for I/O operations using an **event loop** and **callback queue**.

Steps:
1. Code is parsed and compiled.
2. Synchronous code is executed line by line.
3. Asynchronous tasks (timers, network calls, etc.) are delegated to browser APIs.
4. Once completed, callbacks are queued for execution after the main thread is free.

---

## Difference Between Synchronous and Asynchronous Code

| Synchronous | Asynchronous |
|------------|--------------|
| Executes line-by-line. | Executes tasks in the background. |
| Blocks further code execution until current task is completed. | Doesn't block code execution. |
| Simple and predictable. | Requires callbacks, promises, or async/await. |
| Example: `let a = 1; let b = 2; let c = a + b;` | Example: `setTimeout(() => console.log("Hello"), 1000);` |

---

## Ways to Make Code Asynchronous

1. `setTimeout` / `setInterval`
2. `XMLHttpRequest` / `fetch`
3. Event listeners
4. Promises
5. Async/await

---

## Web Browser APIs

Web APIs are features provided by the browser (not JavaScript) that enable asynchronous tasks. Examples:

- `DOM` manipulation
- `setTimeout`, `setInterval`
- `fetch`, `XMLHttpRequest`
- `Event Listeners`
- `Geolocation`, `Web Storage`, `Canvas`, etc.

---

## What is the Event Loop?

The **event loop** is the mechanism that allows JavaScript to perform non-blocking operations by putting asynchronous operations in a queue to be executed later. It continuously checks the call stack and the task queue:

1. Executes all synchronous code.
2. When the call stack is empty, the event loop pushes the first callback from the queue into the call stack.

---

## Callback Hell

**Callback Hell** is a situation where callbacks are nested within callbacks, leading to unreadable and hard-to-maintain code.

```js
getData(function(a){
  processA(a, function(b){
    processB(b, function(c){
      processC(c, function(result){
        console.log(result);
      });
    });
  });
});
```

---

## Inversion of Control in Callbacks

Inversion of Control happens when you pass control of your program’s flow to a third-party function (e.g., a callback), which may behave unexpectedly.

---

# Promises

## What is a Promise?

A **Promise** is an object representing the eventual completion or failure of an asynchronous operation.

---

## Creating a New Promise

```js
const myPromise = new Promise((resolve, reject) => {
  // async work
  if(success){
    resolve('Success');
  } else {
    reject('Error');
  }
});
```

---

## Promise States

1. **Pending** – Initial state
2. **Fulfilled** – Operation completed successfully
3. **Rejected** – Operation failed

---

## Consuming a Promise

```js
myPromise.then(result => console.log(result)).catch(error => console.error(error));
```

---

## Chaining Promises

```js
myPromise
  .then(result => anotherAsync(result))
  .then(data => process(data))
  .catch(error => console.error(error))
  .finally(() => console.log("Done"));
```

---

## Error Handling in Promise Chains

- `.catch()` catches any error in the chain.
- If an error is thrown inside `.then()` and there is no `.catch()`, the error is unhandled.
- Always place `.catch()` at the end of a promise chain.

---

## Multiple Promises

### Chaining
```js
promise1()
  .then(() => promise2())
  .then(() => promise3());
```

### `Promise.all`
```js
Promise.all([p1, p2, p3])
  .then(values => console.log(values))
  .catch(error => console.error(error));
```

### `Promise.allSettled`
```js
Promise.allSettled([p1, p2, p3])
  .then(results => console.log(results));
```

### `Promise.any`
```js
Promise.any([p1, p2, p3])
  .then(firstSuccess => console.log(firstSuccess))
  .catch(error => console.error(error));
```

### `Promise.race`
```js
Promise.race([p1, p2, p3])
  .then(firstResolved => console.log(firstResolved))
  .catch(error => console.error(error));
```

---

## Promisifying Callback-Based Functions

```js
function delay(ms) {
  return new Promise(resolve => setTimeout(resolve, ms));
}
```

Example with `fs.readFile` in Node.js:
```js
const fs = require('fs');
const { promisify } = require('util');
const readFileAsync = promisify(fs.readFile);

readFileAsync('file.txt', 'utf8')
  .then(data => console.log(data))
  .catch(err => console.error(err));
```

---

## Built-in Promise Methods

### `Promise.resolve(value)`
Returns a resolved promise.

### `Promise.reject(error)`
Returns a rejected promise.

### `Promise.all([...])`
Waits for all promises to resolve or any to reject.

### `Promise.allSettled([...])`
Waits for all promises to either resolve or reject.

### `Promise.any([...])`
Returns the first resolved promise, ignores rejected ones.

### `Promise.race([...])`
Returns the first settled promise (resolved or rejected).
