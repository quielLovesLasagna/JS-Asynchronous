<h1>Error Handling with try & catch</h1>

```try``` and ```catch``` are keywords used in JavaScript to handle errors and exceptions in your code.
When you place code inside a ```try block```, JavaScript attempts to execute it. If an error occurs within the try block, the program doesn't crash. 
Instead, it immediately jumps to the ```catch block```. Inside the catch block, you can handle the error in a controlled manner.

Here's an example:

```js
async function exampleAsyncFunction() {
  try {
    // Code that may throw an error
    let result = await someAsyncTask();
    console.log(result);
  } catch (error) {
    // Handle the error here
    console.error("An error occurred:", error);
  }
}
```

1) ```async function```: You create an ```async``` function to work with asynchronous code. This allows you to use ```await``` inside the function.
2) ```try block```: Inside the try block, you place the code that might throw an error. In this example, we use await to await the result of an asynchronous task.
3) ```catch block```: If an error occurs in the try block, the code inside the catch block is executed. It captures the error in the error variable. You can then handle the error as you see fit. 
In this case, we log the error to the console.
4) ```Using await```: When you use await, it pauses the execution of your function until the promise resolves or rejects. If the promise rejects (an error occurs), it jumps to the catch block.

This is how it would look like if we use ```.then()``` and ```.catch()```:

```js
exampleAsyncFunction()
  .then(() => {
    console.log("Async function completed successfully.");
  })
  .catch((error) => {
    console.error("Async function encountered an error:", error);
  });
```

This is how you would use the function, and if an error occurs within it, it will be caught and handled in the catch block. 
Error handling ensures that your application doesn't crash when something goes wrong during an asynchronous operation. 
It's a fundamental part of writing reliable JavaScript code.
