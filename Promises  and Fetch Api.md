<h1>Promises and Fetch API</h1>

<h2>Fetch API:</h2>

The Fetch API is a modern way to make network requests, such as fetching data from a server. It returns promises, making it ideal for asynchronous operations.

1) ***Making a GET Request:***

To fetch data from a server, you use the fetch() function. It takes the URL as its argument. You should pass the URL of the resource you want to request data from. This URL could point to a web API, a server, or any online resource that provides data.

```
const request = fetch('https://jsonplaceholder.typicode.com/posts/1');
```

2) ***Handling the Response:*** 

The ```fetch()``` function returns a promise that resolves to the Response object. You can use ```.then()``` to work with the response. This is called ***Consuming the Promise*** with ```.then()```.

```
request.then(response => {
  // Check if the response is okay (status 200)
  if (!response.ok) {
    throw new Error('Network response was not ok');
  }
  // Parse the response as JSON and return the result
  return response.json();
})
```

3) ***Chaining Promises:***
You can chain ```.then()``` to process the data. This allows you to handle the response in multiple steps.

```
fetch('https://jsonplaceholder.typicode.com/posts/1')
  .then((response) => response.json())
  .then((data) => {
    console.log('Data:', data);
  });
```

***

***Important notes:***




