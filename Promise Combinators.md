<h1>Promise Combinators</h1>

Promise combinators are are utility methods to deal with multiple promises that need to be executed in parallel.
Each combinator method takes in an array of promises as an argument.
Each combinator method in-turn returns a Promise.

***

1) ```Promise.all()```: 
- This is the most used kind of combinator. An example scenario will be the one discussed above - get multiple Quotes in parallel.
- **IMPORTANT**: ```all()``` will settle if all the supplied promises have **fulfilled**, or if any of them is rejected.
We use this when: we want to get some data about something at the same time but in which the order that the data arrives does not matter at all.
```Promise.all()``` will ```short circuit``` as soon as one promise rejects.
- Always surround call to Promise.all() by try { ... } catch(e) { ... } blocks.
- When we await Promise.all(), the result will be an array of objects returned for each promise supplied.

Here's an example:
```js
const getDataFromApi = async (pathParam) => {
  return fetch(`https://demo2202897.mockable.io/${pathParam}`).then(res => res.json());
};

// 
const getAllData = async () => {
  const promises = [];
  promises.push(getDataFromApi("qotd"));
  promises.push(getDataFromApi("getLargeData"));
  try {
    const result = await Promise.all(promises);
    document.write(JSON.stringify(result, null, 2)); 
  } catch(e) {
    console.error(e);
  }
}

getAllData();
```

2) ```Promise.race()```:
- This is mostly used in conditions where we want to race the execution of promises against time. An example would be, "Get me all the quotes within 500ms or you fail".
- This is not at all limited to just race against time, it can also be a race between many asynchronous operations.
- **IMPORTANT**: ```race()``` will settle if any of the supplied promises have fulfilled or rejected. Meaning, the race will terminate after first success or failure.
- Always a good practice to surround Promise.race() call by try { ... } catch(e) { ... } blocks.
- When we await Promise.race(), the result will be the return value of the first settled promise.

The promise returned by Promise.race is settled as soon as one of the input promises settles. Remember that settled simply means that a value is available but it does not matter if the promise got rejected or fulfilled. So, in Promise.race, basically, the first settled promise wins the race. 

Here's a basic example using ```IIFE```:

```js
(async function () {
  const res = await Promise.race([
    getJSON(`https://restcountries.com/v2/name/italy`),
    getJSON(`https://restcountries.com/v2/name/egypt`),
    getJSON(`https://restcountries.com/v2/name/mexico`),
  ]);
  console.log(res[0]);
})();
```


Here's an example where we are setting a condition that: if the ```getJSON``` function takes too long to fetch data from an API/it takes > 5 seconds to fetch the data, then we call the ```timeout``` function which automatically rejects and creates an error after 5 seconds.

```js
const timeout = function (sec) {
  return new Promise((_, reject) => {
    setTimeout(() => {
      reject(new Error("Request took too long!"));
    }, sec * 1000);
  });
};

Promise.race([
  getJSON(`https://restcountries.com/v2/name/philippines`),
  timeout(5),
])
  .then((res) => console.log(res[0]))
  .catch((err) => console.error(err));
```

3) ```Promise.allSettled()```:
- Introduced in ES2020, ```allSettled``` combinator should be used when the result of each promise supplied doesn't matter (either fulfilled or rejected), but still want to execute each one of it.
- **IMPORTANT**: allSettled() will settle when all the supplied promises are settled.
It will simply return an array of all the ```settled promises```. No matter if the promise got rejected or fulfilled. It's similar to ```Promise.all``` in regards that it also returns an array of all the results. But the difference is that Promise.all will short circuit as soon as one promise rejects, but Promies.allSettled, simply never short circuits. So it will simply return all the results of all the promises.
- When we await Promise.allSettled(), the result will be an array of result values of all the settled promises.

```js
async function allSettledFunc() {
  const promises = [
    Promise.resolve("Success"),
    Promise.reject("ERROR"),
    Promise.resolve("Another success"),
  ];

  try {
    const results = await Promise.allSettled(promises);
    console.log(results);
  } catch (err) {
    console.error(err);
  }
}
allSettledFunc();
```

The code above is the same here:

```js
Promise.allSettled([
  Promise.resolve("Success"),
  Promise.reject("ERROR"),
  Promise.resolve("Another success"),
])
  .then((res) => console.log(res))
  .catch((err) => console.error(err));
```

4) ```Promise.any()```
- Introduced in ES2021, any combinator should be used when you want the result of the first fulfilled promise.
- The only difference from race combinator is that the promise rejections are neglected here.
- **IMPORTANT**: any() will settle when any of the supplied promise is fulfilled.
- When we await Promise.any(), the result will be the result of the first fulfilled promise. If all promises are rejected, then an error will be thrown.
- Hence, it becomes important to surround Promise.any() call by try { ... } catch(e) { ... } blocks.

**AGAIN**: Takes in an array of promises, and it will return the first fulfilled promise, and it will simply ignore rejected promises. It is similar to Promise.race but the difference is that rejected promises are ignored. Therefore, the results of Promise.any is always gonna be a fulfilled promise. Unless, all of them reject.

```js
async function anyFunc() {
  const promises = [
    Promise.resolve("Success"),
    Promise.reject("ERROR"),
    Promise.resolve("Another success"),
  ];

  try {
    const result = await Promise.any(promises);
    console.log(result);
  } catch (err) {
    console.log(err);
  }
}

anyFunc();
```

The code above is the same as the code below:

```js
Promise.any([
  Promise.resolve("Success"),
  Promise.reject("ERROR"),
  Promise.resolve("Another success"),
])
  .then((res) => console.log(res))
  .catch((err) => console.error(err));
```

***
**Credits**:
Check this [article](https://dev.to/iyashsoni/javascript-promise-combinators-in-3-mins-52b3#:~:text=What%20are%20Promise%20Combinators%3F,in%2Dturn%20returns%20a%20Promise.) for more information.


