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

**Note**: An async function in JavaScript ```always returns a promise```, regardless of what's inside the function. This is one of the key features of async functions.


