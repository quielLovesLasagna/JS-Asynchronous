<h1>Consuming Promises with Async/Await</h1>

To consume a promise with async await, we start by creating a special function **__async function__**. We can do this by simple adding ```async``` in from of the function:

```js
async function () {
  // code goes here
}
```

after doing that, then the ```function``` will now be an ```asynchronous function``` __(a function that will basically keep running in the background while performing the code inside of it)__ then when the function is done,
it will automatically return a promise. Inside an async function, we can have one or more ```await``` statements.

Here's an example:

```js
const whereAmI = async (country) => {
  const res = await fetch(`https://restcountries.com/v2/name/${country}`);
  console.log(res);
}
```

In the example above, the ```fetch``` will return a promise. In an async fuction like the example above, we can use the ```await``` statement to basically await for the result of the promise coming from ```fetch```.
So basically, await will stop/pause the execution of the function while the ```fetch``` function is doing its task (which is making a request to a Web API). During the pause, the callstack is free to execute other tasks.
While waiting for the fetch operation to complete, the event loop continues to check if there are any other tasks in the call stack to execute. If there are, it will execute them.
Once the fetch operation is done (whether it succeeds or fails), the code after the await will continue to execute, and the result will be logged to the console.

Stopping execution in an async function, (which is what we have in the example above) is not a problem, it will ```not``` block the execution. Because the async function is ```running asynchronously``` in the background.
Therefore, it is not blocking the main thread of execution (it's not blocking the call stack). 

That's what so special about ```async await```. It makes our code look like a regular synchronous code while behind the scenes everything is in fact asynchronous.

As soon as the promise (from fetch) is resolved, then the value of the whole await is gonna be the resolved value of the promise (from the fetch function), so we can store it to a variable.

```async/await``` is simply syntactic sugar over the ```then``` method in promises. So of course behind the scenes, we are still using promises. We are just using a different way of consuming them.

***

**Note**: 

- An async function in JavaScript ```always returns a promise```, regardless of what's inside the function. This is one of the key features of async functions.
- If we don't use ```await``` inside the async function, it will behave differently -> it doesn't wait for the asynchronous task to complete before moving to the next line of code.

Here's an example:

```js
async function exampleAsyncFunction() {
  console.log("Start");
  // Without await, this promise will not be waited for.
  fetch('https://jsonplaceholder.typicode.com/posts/1')
    .then(response => response.json())
    .then(data => console.log(data));
  console.log("End");
}

exampleAsyncFunction();
console.log("Function call finished");
```

In this example, "Start" and "End" will be logged before the data is fetched because there's ```no await```. This can be useful in some cases when you want to initiate multiple asynchronous tasks and don't need to wait for their results before proceeding with other tasks.

But, keep in mind that if you do need the result of the asynchronous operation, you should use await to ensure that your code doesn't continue until the promise is resolved. If you omit await, you might not get the expected behavior in your program.

Looking back at the example, we didn't use await, the async function will not stop its execution. It will continue running, and this can potentially block other tasks in the call stack.

When you make an asynchronous call without await, like the fetch in the example, it starts a network request in the background, but the function doesn't wait for it to complete.

If there are other functions in the call stack (the stack of function calls in your program), they will execute independently, which can lead to non-deterministic behavior. In other words, there's no guarantee about the order in which various parts of your code will finish.

So, not using await can lead to a lack of control over the order of execution in your program, which is usually not the behavior you want when dealing with asynchronous operations.

If you do want your code to wait for the asynchronous operation to complete, you should use await. This ensures that the function will pause until the promise is resolved and then continue executing the subsequent code. This way, you have better control over the flow of your program and can handle the asynchronous result more predictably.

**Additions**:
Marking a function as async explicitly tells JavaScript that this function will perform asynchronous operations. This designation makes it return a promise.

When you use await inside an async function, it tells the function to pause execution until the awaited promise is resolved. This allows you to handle the result of that asynchronous task in a synchronous-like manner.

If you don't use await inside the async function, it doesn't stop the function from being asynchronous. The function still executes asynchronously; it just doesn't wait for the asynchronous task to complete before moving on to the next lines of code.


To summarize, adding async to a function always makes it asynchronous. Whether you use await inside it or not determines how you handle the asynchronous tasks within the function, but it doesn't change the fact that the function itself remains asynchronous and can potentially run concurrently **(at the same time; simultaneously)** with other code.

***

Watch [this](https://www.youtube.com/watch?v=V_Kr9OSfDeU&t=334s) to learn more about async/await.


