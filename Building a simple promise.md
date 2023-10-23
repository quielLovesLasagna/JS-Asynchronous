<h1>Building a Simple Promise</h1>

1) **Step 1: Create a Promise**

You start by creating a ```new Promise``` object. It takes a single argument, a function that, in turn, takes two parameters, ```resolve``` and ```reject```. 
These are functions you'll call to indicate whether the promise is fulfilled or rejected.

```js
const myPromise = new Promise((resolve, reject) => {
  // Your async code goes here
});
```

- The promise constructor takes exactly one argument which is called ```executor function```
- As soon as the promise constructor runs, it will automatically execute the executor function that we passed in
- And as it executes the function, it will do so by passing two other arguments (which are funtions) -> (resolve, reject)
- The executor function is the function which will contain the asynchronous behavior that we're trying to handle with the promise
- The executor function should eventually produce a result value (the future value of the promise)

2) **Step 2: Resolve and Reject**

Inside the function you passed to the Promise, you write your asynchronous code. When the task is successful, you call resolve. 
If there's an error, you call reject. For example, let's simulate a simple delay:

```js
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const randomNumber = Math.random();
    if (randomNumber < 0.5) {
      resolve(randomNumber);
    } else {
      reject("Oops, something went wrong!");
    }
  }, 2000); // Simulating a 2-second delay
});
```

3) **Step 3: Handling the Promise**

Now, you can use ```.then()``` to handle the resolved value and ```.catch()``` for errors. For instance:

```js
myPromise
  .then((result) => {
    console.log("Success! Random number is: " + result);
  })
  .catch((error) => {
    console.error("Error: " + error);
  });
```

Here, if the promise resolves successfully, it prints the random number. If there's an error, it logs the error message.

4) **Step 4: Chaining Promises**

Promises can also be chained. For example, you can add another ```.then()``` to handle the result from the first ```.then()```.

```js
myPromise
  .then((result) => {
    console.log("Success! Random number is: " + result);
    return result * 2; // Modify the result
  })
  .then((newResult) => {
    console.log("Doubled random number is: " + newResult);
  })
  .catch((error) => {
    console.error("Error: " + error);
  });
```

***

<h2>A way to easily create a fulfilled or a rejected promise IMMEDIATELY</h2>

```js
Promise.resolve("This is resolved immediately").then((res) => console.log(res));
Promise.reject(new Error("This is rejected immediately")).catch((err) =>
  console.error(err)
);
```


