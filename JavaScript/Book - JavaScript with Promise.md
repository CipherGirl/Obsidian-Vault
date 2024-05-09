# 1. Asynchronous JavaScript
Web applications asynchronously fetch data and load scripts in the browser. Node.js and its derivatives provide a host of APIs for asynchronous I/O. And new web specifications for Streams, Service Workers, and Font Loading all include asynchronous calls.

## [[Callback]]
*A callback is a function provided to other code for invocation. In JavaScript, callbacks are used to manage the execution order of any code that depends on an async task.* 

* Callbacks can be invoked synchronously or asynchronously (i.e., before or after the function they are passed to returns.)
* Programmers need the ability to write async code so long-running tasks such as network requests do not block other parts of the program while incomplete.
* When programmers are new to asynchronous programming, it’s easy for them to incorrectly expect an async script to run as if it were synchronous. Putting code that relies on the completion of an async task outside the appropriate callback creates problems.

	```js
	// Example 1-7. Naive asynchronous code. This doesn’t work!
	var fs = require('fs');
	var timestamp = new Date().toString();
	var contents;
	fs.writeFile('date.txt', timestamp);
	fs.readFile('date.txt', function (err, data) {
	if (err) throw err;
	contents = data; // 3
	});
	console.log('Comparing the contents'); //1
	console.assert(timestamp == contents); //2 - Fail!
	
	//readFile is guaranteed to return before invoking the callback.
	```
* Functions that invoke a callback synchronously in some cases and asynchronously in others create forks in the execution path that make your code less predictable.

## Asynchronous JavaScript
Callbacks can be invoked synchronously or asynchronously (i.e., before or after the
function they are passed to returns.) The `array.forEach()` method used in the previous section invokes the callback it receives synchronously. An example of a function that invokes its callback asynchronously is `window.requestAnimationFrame()`.

Programmers need the ability to write async code so long-running tasks such as network requests do not block other parts of the program while incomplete.

In JavaScript, callbacks are used to manage the execution order of any code that depends on an async task. 

When programmers are new to asynchronous programming, it’s easy for them to incorrectly expect an async script to run as if it were synchronous. Putting code that relies on the completion of an async task outside the appropriate callback creates problems.

	Functions that invoke a callback synchronously in some cases and asynchronously in others create forks in the execution path that make your code less predictable.

## [[Event Loop]]
The JavaScript you write runs on a single thread, which avoids complications found
in other languages that share memory between threads. If JavaScript is single threaded, where are the async tasks and callbacks run? To explain,
```js
var http = require('http');
http.get('http://www.google.com', function (res) {
console.log('got a response');
});
```
The call to `http.get()` triggers a network request that a separate thread handles.

*JavaScript code you write all runs on a single thread, but the code that implements the async tasks (the `http.get()` implementation in Example) is not part of that JavaScript and is free to run in a separate thread.

Once the task completes the result needs to be provided to the JavaScript thread. At this point the callback is placed in a queue. A multi-threaded language might interrupt whatever code was currently executing to provide the results, but in JavaScript these interruptions are forbidden. Instead there is a run-to-completion rule, which means that your code runs without interruption until it passes control back to the host environment by returning from the function that the host initially called. At that point the callback can be removed from the queue and invoked.

All other threads communicate with your code by placing items on the queue. They are not permitted to manipulate any other memory accessible to JavaScript. In the previous example the callback accesses the response from the async HTTP request. 

After the callback is added to the queue, there is no guarantee how long it will have to wait. How long it takes the current code to run to completion and what else is in the queue controls the time. The queue can contain things such as mouse clicks, key‐strokes, and callbacks for other async tasks. The JavaScript runtime simply continues in an endless cycle of pulling an item off the queue if one is available, running the code that the item triggers, and then checking the queue again. *This cycle is known as* *the **`Event Loop`**.* 

### [[Race Condition]]
Allowing the event loop to turn before registering the event listeners would create a
race condition.

*Example 1-12. Race condition*
```js
var async = true;
var xhr = new XMLHttpRequest();
xhr.open('get', 'data.json', async);
xhr.send();

setTimeout(function delayed() { // Creates race condition!
	function listener() {
		console.log('greetings from listener');
	}
	xhr.addEventListener('load', listener);
	xhr.addEventListener('error', listener);
}, 3000);
```

Performing the event listener registration inside a callback given to setTimeout
causes a delay. Now the only way the listener function will be called is if the delayed function is pulled off the queue and run before the HTTP request completes and the load or error event is triggered. Experimenting with different values for the delay parameter of setTimeout shows listener being invoked sometimes but not always.

# 2. Introducing Promises
The biggest challenge with nontrivial amounts of async JavaScript is managing execution order through a series of steps and handling any errors that arise. Promises address this problem by giving you a way to organize callbacks into discrete steps that are easier to read and maintain. And when errors occur they can be handled outside the primary application logic without the need for boilerplate checks in each step.

*A promise is an object that serves as a placeholder for a value.* That value is usually
the result of an async operation such as an HTTP request or reading a file from disk.
When an async function is called it can immediately return a promise object. Using
that object, you can register callbacks that will run when the operation succeeds or an
error occurs.

When Promise is used as a constructor it requires a callback known as a resolver function. The resolver serves two purposes: it receives the resolve and reject arguments, which are functions used to update the promise once the outcome is known, and any error thrown from the resolver is implicitly used to reject the promise.

```js
//Example 2-3. Chaining calls using then and catch
loadImage('security_holes.png').then(function (img) {
	document.body.appendChild(img);
}).catch(function (e) {
	console.log('Error occurred while loading image');
	console.log(e);
});

// Example 2-4. Creating and resolving a promise
function loadImage(url) {
	var promise = new Promise(
		function resolver(resolve, reject) {
			var img = new Image();
			img.src = url;
			img.onload = function () {
				resolve(img);
			};
			img.onerror = function (e) {
				reject(e);
			};
		}
	);
	return promise;
}
```
## Multiple Consumer
```js
//Example 2-5. One promise with multiple consumers
var user = {
	profilePromise: null,
	getProfile: function () {
		if (!this.profilePromise) {
			// Assume ajax() returns a promise that is eventually
			// fulfilled with {name: 'Samantha', subscribedToSpam: true}
			this.profilePromise = ajax(/*someurl*/);
		}
		return this.profilePromise;
	}
};
var navbar = {
	show: function (user) {
		user.getProfile().then(function (profile) {
			console.log('*** Navbar ***');
			console.log('Name: ' + profile.name);
		});
	}
};
var account = {
show: function (user) {
	user.getProfile().then(function (profile) {
			console.log('*** Account Info ***');
			console.log('Name: ' + profile.name);
			console.log('Send lots of email? ' + profile.subscribedToSpam);
		});
	}
};
navbar.show(user);
account.show(user);
// Console output:
// *** Navbar ***
// Name: Samantha
// *** Account Info ***
// Name: Samantha
// Send lots of email? true
```

Remember that a promise serves as a placeholder for the result of an operation. In
this case, the `user.profilePromise` is a placeholder used by the `navbar.show()` and
`account.show() `functions. These functions can be safely called anytime before or
after the profile data is available. The callbacks they use to print the data to the con‐
sole will only be invoked once the profile is loaded. This removes the need for an if
statement in either function to check whether the data is ready.

```js
// Equivalent ways to create a resolved promise
new Promise(function (resolve, reject) {
resolve('the long way')
});
Promise.resolve('the short way');

// Equivalent ways to create a rejected promise
new Promise(function (resolve, reject) {
reject('long rejection')
});
Promise.reject('short rejection');
```


## Promise States
* Pending - The operation has not begun or is in progress
* Fulfilled - The operation has completed (We refer to the fulfilled and rejected states as success and error)
* Rejected - The operation could not be completed
The state of a promise never changes after it is fulfilled or rejected.

## Chaining Promises


## Callback Execution Order
Promises are primarily used to manage the order in which code is run relative to
other tasks. **The resolver function passed to the Promise constructor executes synchronously**. And all **callbacks passed to then and catch are invoked asynchronously**.

```js
// Example 2-11. Execution order of callbacks used by promises
var promise = new Promise(function (resolve, reject) {
	console.log('Inside the resolver function'); // 1
	resolve();
});
promise.then(function () {
	console.log('Inside the onFulfilled handler'); // 3
});
console.log('This is the last line of the script'); // 2
// Console output:
// Inside the resolver function
// This is the last line of the script
// Inside the onFulfilled handler
```

The resolver function passed to the Promise constructor executes immediately followed by the log statement at the end of the script. Then the event loop turns and the promise that is already resolved invokes the `onFulfilled` handler.

## Basic Error Propagation
Rejections and errors propagate through promise chains. hen one promise is rejec‐
ted all subsequent promises in the chain are rejected in a domino effect until an
`onRejected` handler is found.  In practice, one catch function is used at the end of a
chain (see Example 2-12) to handle all rejections.
```js
// Example 2-12. Using a rejection handler at the end of a chain
Promise.reject(Error('bad news')).then(
	function step2() {
	console.log('This is never run');
	}
).then(
	function step3() {
	console.log('This is also never run');
	}
).catch(
	function (error) {
	console.log('Something failed along the way. Inspect error for more info.');
	console.log(error); // Error object with message: 'bad news'
	}
);
// Console output:
// Something failed along the way. Inspect error for more info.
// [Error object] { message: 'bad news' ... }
```

	Using JavaScript Error objects to reject promises can capture the call stack for troubleshooting and makes it easier to treat the argument the catch handler receives in a uniform way.

## The Promise API
The complete Promise API consists of a constructor and six functions.
1. `Promise`:
	```js
	new Promise(function (resolve, reject) { … }) returns promise
```
	The Promise global is a constructor function that the new keyword invokes. The Promise global creates promise objects that have the two methods then and catch for registering callbacks that are invoked once the promise is fulfilled or rejected.
	
2. `Promise.then`: 
   ```js
   promise.then([onFulfilled], [onRejected]) returns promise
```
	The promise.then() method accepts an `onFulfilled` callback and an `onRejected`
	callback. People generally register `onRejected` callbacks using `promise.catch()` instead of passing a second argument to then.
	
3. `Promise.catch`: 
   ```js
   promise.catch(onRejected) returns promise
```
	The promise.catch() method accepts an `onRejected` callback and returns a promise that the return value of the callback or any error thrown by the callback resolves or rejects, respectively.
	
4. `Promise.resolve`:
	 ```js
 Promise.resolve([value|promise]) returns promise
```
    The `Promise.resolve()` function is a convenience function for creating a promise that is already resolved with a given value. If you pass a promise as the argument to. `Promise.resolve()`, the new promise is bound to the promise you provided and it will be fulfilled or rejected accordingly.
    
5. `Promise.reject`:
   ```js
Promise.reject([reason]) returns promise
```
	The Promise.reject() function is a convenience function for creating a rejected promise with a given reason.
	
6. `Promise.all`:
	```js 
Promise.all(iterable) returns promise
```
	The Promise.all() function maps a series of promises to their fulfillment values. 