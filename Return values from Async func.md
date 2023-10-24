<h1>Returning Values from Async Functions</h1>

When you create an async function in JavaScript, it always returns a promise. The value that you ```explicitly``` return from within that async function is the fulfilled value of the promise.

```js
async function fetchData() {
  return 42;
}

fetchData().then((result) => {
  console.log(result); // This will log 42
});
```

In this example, the fetchData function is an async function that returns the value 42. 
When we call ```fetchData()```, it returns a promise that will be fulfilled with the value 42. The then method is used to handle the fulfilled promise and log the value.
