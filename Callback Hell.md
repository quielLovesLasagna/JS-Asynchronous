<h1>Callback Hell</h1>

**Callback hell**, is a common issue in JavaScript when dealing with multiple asynchronous operations. It can make your code hard to read and maintain.

Callback hell occurs when you have several nested callbacks in your code, often due to asynchronous tasks like fetching data from a server or handling user interactions.

Here's am example:

```
 setTimeout(() => {
   console.log("1 second passed");
   setTimeout(() => {
     console.log("2 seconds passed");
     setTimeout(() => {
       console.log("3 seconds passed");
       setTimeout(() => {
         console.log("4 seconds passed");
       }, 1000);
     }, 1000);
   }, 1000);
 }, 1000);
```

As you can see, the code becomes deeply nested, making it hard to follow and debug. It's challenging to keep track of what each callback does.
