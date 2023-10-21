<h1>Asynchronous JavaScript, AJAX and APIs</h1>

**_Synchronous_**

To understand what Asynchronous JavaScript is, we must first understand what Synchronous JavaScript is first.
Synchronous is the opposite of Asynchronous.

Synchronous simply means that the code is executed line by line. In the exact order of execution that we defined in our code. Just like in this example:

```
const p = document.querySelector('.p');
p.textContent = 'My name is Jonas! ';
alert('Text set!');
p.style.color = 'red';
```

Each line of code **waits** for previous line to finish execution. This can create problems when one line of code takes a very long time to run. In the example above, we have an alert statement which creates an alert window. This alert window will block the code execution. So nothing will happen on the page until we click the **OK** button / close the alert, and only then the code can continue executing. The alert statement here is a good example of a long running operation which blocks execution of the code. Most of the time, synchronous code if fine but imagine that execution would have to wait, for example: for a five seconds timer to finish, that's just terrible because meanwhile, nothing on the page would work during this five seconds. So that's where asynchronous is helpful.

**_Asynchronous_**

In this example, the first line of code is still synchronous, then we move to the second line in a synchronous way. But then we encounter the setTimeout function which will basically start a timer in a asynchronous way. So this means that the timer will essentially run in the background without preventing the main code from executing, we also defined a callback function which will not be executed now but only after the timer has finished running. This callback function is asynchronous JavaScript, it is asynchronous because it't only going to be executed after a task that is running in the background finishes execution, in this case, that is the timer. So this callback is defined and then we immediately move on to the next line. So the main code is not being blocked and execution does not wait for the asynchronous timer to finish its work.
```
const p = document.querySelector('.p');
setTimeout(function () {
p.textContent = 'My name is Jonas!';
}, 5000);
p.style.color = 'red';
```

In summary, asynchronous programming is all about coordinating the behavior of our program over a certain period of time. It literally means not occuring at the same time.

Note: Callback functions alone does **NOT** make a code asynchronous. Also, event listeners alone does not make a code asynchronous.

**_AJAX_**

**_A_**synchronous **_J_**avascript **_A_**nd **_X_**ML: Allows us to communicate with remote web servers in an asynchronous way. With AJAX calls, we can
request data from web servers dynamically.
