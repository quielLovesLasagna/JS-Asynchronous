<h1>Promisifying - JS</h1>

Promisifying in JavaScript is a technique that helps make your asynchronous code cleaner and easier to work with. 
It involves converting functions that use callbacks into functions that return promises. 
Promises simplify asynchronous operations and make them more readable.

***

1) **Step 1: Understanding Callback Functions**
In JavaScript, many functions are asynchronous and use callbacks to handle results. For example:

```js
function fetchData(callback) {
  // Simulate fetching data after some time
  setTimeout(function () {
    callback('Data fetched successfully');
  }, 1000);
}

// Using the callback
fetchData(function (result) {
  console.log(result);
});
```

Here, we have fetchData that takes a callback function and calls it when data is ready.

2) **Step 2: Promisifying a Function**
To make this more manageable with promises, you can create a new function that returns a promise. Here's how:

```js
function fetchDataWithPromise() {
  return new Promise(function (resolve, reject) {
    setTimeout(function () {
      resolve('Data fetched successfully');
    }, 1000);
  });
}

// Using the promise
fetchDataWithPromise()
  .then(function (result) {
    console.log(result);
  })
  .catch(function (error) {
    console.error(error);
  });
```

Now, ```fetchDataWithPromise``` returns a promise, and you can use .then to handle success and .catch for errors.

3) **Step 3: How It Works**

- We create a new Promise object.
- Inside it, we use resolve and reject to control the flow.
- When the operation is successful, we call resolve with the result.
- When there's an error, we call reject.





