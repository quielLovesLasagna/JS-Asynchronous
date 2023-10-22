<h1>Handling Rejected Promises</h1>

###

1) **Using the ```.then()``` method with two callback functions:**

When using the ```.then()``` method with ***two callback*** functions, you're explicitly providing one function for the ***resolved case*** and another function for the ***rejected case***.

Here's an example:

```
fetch('https://api.example.com/data')
  .then(
    function(response) {
      // This is the first function for the resolved case
      return response.json();
    },
    function(error) {
      // This is the second function for the rejected case
      console.error('Error:', error);
    }
  );
```
In this example, the first function inside the first .then() handles the successful response, while the second function inside the same .then() block handles errors if the promise is rejected.

Using two callback functions with the .then() method is a valid approach, and it can make your code more explicit in terms of handling success and error cases. However, it's less common than the .then() and .catch() combination, which provides a cleaner separation between success and error handling and is widely used in practice. Both methods are effective, and your choice may depend on your coding style and project requirements.

2) ***Using the ```.then()``` with the ```.catch()``` method***:

You can also use the ```.catch()``` method to handle errors in a more centralized way. This is especially useful when you have multiple ```.then()``` blocks in your promise chain.

Here's an example:

```
fetch('https://api.example.com/data')
  .then(response => {
    // Handle a successful response here
    return response.json();
  })
  .then(data => {
    // Handle the parsed JSON data
    console.log(data);
  })
  .catch(error => {
    // This block will handle any errors from the previous .then() blocks
    console.error('Error:', error);
  });
```

**Summary**:

Both methods are valid, and your choice depends on your code structure and how you want to handle errors. The .then() method with two arguments allows you to handle errors more explicitly in the specific .then() block, while .catch() provides a centralized way to handle errors in the entire promise chain, which can make your code cleaner and more organized.

***
**Notes**:

In the ```.catch()``` method, the ```error``` parameter represents the ```error object``` that caused a promise to be rejected. 
When a promise is rejected, it typically means that something went wrong during the asynchronous operation, and the error parameter contains information about what went wrong. 
This object can provide valuable details about the error, allowing you to handle and troubleshoot the issue.

When an error occurs in any of the .then() methods within a promise chain, JavaScript will propagate that error down the chain to the nearest .catch() block. 
If you have a parameter defined in the .catch() method, you can access and handle the error inside the .catch block.

**Important Notes**:

The ```fetch()``` method only gets rejected when there's an error in your network. Taking this into account, we must handle errors caused by other things, not just caused by the network error.
This is important because even if we request ```invalid``` data from an API, the promise will always be resolve to a response, so even if the reponse is invalid and we can still work with it but **not** the way we intend to,
this will cause serious problems in our code. To solve this, we can ```Manually throw an error```.

Here's am example:

```
fetch('https://api.example.com/data')
  .then(response => {
    // Handle a successful response here
    if (!response.ok) {
      throw new Error('Network request failed');
    }
    return response.json();
  })
  .then(data => {
    // Handle the parsed JSON data
    console.log(data);
  })
  .catch(error => {
    // This block will execute if any error occurs in the previous .then() blocks
    console.error('Error:', error.message);
  });
```

1) ```new Error()``` creates a new Error object. This object can store information about the error, including an error message.
2) **Throwing the Error**: When you use the ```throw``` statement followed by the Error object, you raise an exception. 
This means that your code will stop executing at that point, and the control will be transferred to the nearest error-handling mechanism, 
which could be a .catch() block in a promise chain.
3) **Providing an Error Message**: You can include an error message as a string inside the Error() constructor. 
This message describes the nature of the error. It's useful for both debugging and providing context about what went wrong.

In the code above:

1) If the ```response.ok``` property is ```false```, indicating a network request failure, we manually throw an error with the message "Network request failed."
2) This error is then caught in the ```.catch()``` block where you can handle it. The ```error.message``` property is used to access and log the error message, making it easier to identify the cause of the error.

Throwing errors is a crucial part of error handling in JavaScript, as it allows you to handle exceptional cases in your code and provide meaningful error messages to assist in debugging and troubleshooting.

