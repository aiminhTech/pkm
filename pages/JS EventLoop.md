tags:: [[JavaScript]]

- ## Learn Videos & Links
	- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Event_loop
	- https://chanduivaturi.medium.com/non-blocking-dom-fdaeb3ddd08a
	- {{video https://www.youtube.com/watch?v=eiC58R16hb8}}
	-
- ## Single-threaded
	- JavaScript is single-threaded and can only handle one task at a time.
	- At any given time, only one piece of code is being executed, and concurrent operations are handled by **event loop** mechanisms.
	- ## Problem
		- Blocking the main thread when executing slow or long-running tasks
		- This can cause the user interface to become unresponsive, resulting in a poor UX.
		- **To mitigate this issue, developers often use techniques like**
		  background-color:: blue
			- asynchronous programming with callbacks
			- promises
			- async/await to handle non-blocking I/O operations and keep the application responsive
- ## JavaScript Runtime
	- ### Call Stack
		- The excution of the programm
	- ### Memory heap
		- stores variables and objects
- ## Web APIs
  collapsed:: true
	- Provide interfaces to interact with browser feature
	- Allow offloading of long-running tasks to the browser, preventing program freezing.
- ## Macrotask queues
  collapsed:: true
	- **Callback-based web APIs**, like geolocation and setTimeout, use callbacks to handle asynchronous tasks.
	  id:: 6628d078-2193-4df1-9e74-f4acbb183626
	- Callback functions are registered and pushed to the task queue when the task is completed.
	- The event loop checks if the call stack is empty and then moves the first available task from the task queue to the call stack for execution.
- ## Microtask queue
  id:: 6628d019-6516-4e58-a62f-461d7bf7c526
  collapsed:: true
	- **Promise-based web APIs**, like fetch, use promises to handle asynchronous tasks.
	- Promise reactions, such as then and catch callbacks, are pushed to the microtask queue
	- The event loop prioritizes the microtask queue, executing all tasks from the microtask queue before moving to the task queue.
- ## Event Loop
  collapsed:: true
	- An endless loop waits for tasks, executes them, sleeps until another task comes.
	- It manages the execution of tasks in the JS runtime environment
	- When an async operation is initiated, such as reading a file or making an API call, the event loop continues to run other tasks while 
	  waiting for these asynchronous operations to complete.
	- The event loop consists of multiple components, including the call stack, callback queue, and microtask queue
	- Ensures that the microtask queue is empty before moving to the task queue.
	- ### Summary
	  collapsed:: true
		- **Synchronous Code:** Runs immediately as it's encountered in the call stack.
		- **Microtasks (Promise and `queueMicrotask`):** Run after the current synchronous code completes, but before any macrotasks.
		- **Macrotasks (`setTimeout`):** Run after the synchronous code and microtasks are complete.
	- ### Examples
		- #### Example 1
		  collapsed:: true
			- ```js
			  Promise.resolve()
			      .then(() => console.log(1));
			  
			  queueMicrotask(() => console.log(2));
			  
			  setTimeout(() => console.log(3), 0);
			  
			  console.log(4);
			  
			  new Promise(() => console.log(5));
			  
			  (async () => console.log(6))();
			  ```
			- **Step-by-Step Execution**
			  collapsed:: true
				- **Synchronous Code:**
					- `console.log(4)` is executed first because it's a synchronous operation.
					- `new Promise(() => console.log(5))` is executed immediately. When a new `Promise` is created, its executor function runs synchronously.
				- **Async Functions:**
					- `(async () => console.log(6))()` is executed immediately. This is an immediately invoked async function, and the `console.log(6)` inside it runs synchronously before the `Promise` returned by the async function is resolved.
				- **Microtasks:**
					- `Promise.resolve().then(() => console.log(1))` schedules a microtask to log `1`.
					- `queueMicrotask(() => console.log(2))` schedules a microtask to log `2`.
				- **Macrotasks:**
					- `setTimeout(() => console.log(3), 0)` schedules a macrotask to log `3`.
			- **Execution Order**
			  collapsed:: true
				- `console.log(4)` — synchronous
				- `new Promise(() => console.log(5))` — synchronous within the executor
				- `(async () => console.log(6))()` — synchronous within the async function
				- Microtasks:
					- `Promise.resolve().then(() => console.log(1))` — microtask
					- `queueMicrotask(() => console.log(2))` — microtask
				- Macrotask:
					- `setTimeout(() => console.log(3), 0)` — macrotask
				-
		- #### Example 2
		  collapsed:: true
			- ```js
			  async function asyncFunction() {
			    console.log(1);
			    new Promise(() => console.log(2));
			    await new Promise((res) => {
			        setTimeout(() => console.log(3), 0);
			        res();
			    });
			  }
			  
			  new Promise((res) => {
			    console.log(4);
			    (async () => {
			      console.log(5);
			      await asyncFunction();
			      console.log(6);
			    })();
			    res();
			  }).then(() => console.log(7));
			  
			  console.log(8);
			  
			  ```
			- **Step-by-Step Execution**
			  collapsed:: true
				- collapsed:: true
				  
				  **Synchronous Code:**
					- `console.log(4)` is executed because it's inside a synchronous `Promise` executor.
					- `(async () => { ... })()` is called synchronously, so:
						- `console.log(5)` is executed immediately.
					- `console.log(8)` is executed next because it's in the main script.
				- collapsed:: true
				  
				  **Async Functions:**
					- The `asyncFunction` is called within the `async` IIFE:
						- `console.log(1)` is executed inside `asyncFunction`.
						- `new Promise(() => console.log(2))` logs `2` immediately because the `Promise` executor runs synchronously.
						- `await new Promise((res) => { ... })` pauses `asyncFunction` and schedules the macrotask with `setTimeout(() => console.log(3), 0)`.
				- collapsed:: true
				  
				  **Microtasks:**
					- After the main script completes, the microtask queue starts:
						- The `then` callback from `new Promise(...).then(() => console.log(7))` executes and logs `7`.
				- collapsed:: true
				  
				  **Macrotasks:**
					- The macrotask from `setTimeout(() => console.log(3), 0)` executes and logs `3`.
					- After the `await` in `asyncFunction` resolves, `console.log(6)` inside the `async` IIFE runs.
			- **Execution Order**
			  collapsed:: true
				- `console.log(4)` — synchronous
				- `(async () => { ... })()` starts and `console.log(5)` — synchronous
				- `console.log(8)` — synchronous
				- `asyncFunction` starts and `console.log(1)` — synchronous
				- `new Promise(() => console.log(2))` — synchronous within `asyncFunction`
				- **Microtasks**:
					- The `then` callback from `new Promise(...).then(() => console.log(7))` — microtask
				- **Macrotasks**:
					- `setTimeout(() => console.log(3), 0)` — macrotask
					- After the `await`, `console.log(6)` runs within the `async` IIFE.
		- #### Example 3
			- ```js
			  (async () => {
			      const asyncFunc = async () => 'asyncFunc';
			      const promise = new Promise((res) => {
			          console.log('promise');
			      }).then(() => console.log('then'));
			  
			      console.log('async body');
			  
			      queueMicrotask(() => console.log('queueMicrotask'));
			  
			      const results = await Promise.all([asyncFunc(), promise]);
			  
			      return results;
			  })();
			  
			  console.log('script');
			  
			  ```
		- **Step-by-Step Execution**
			- **Synchronous Code:**
				- The immediately invoked async function starts executing.
				- `const promise = new Promise((res) => { console.log('promise'); })` logs `'promise'` because the executor function of the `Promise` runs synchronously.
				- `console.log('async body')` is executed next within the async function.
				- `queueMicrotask(() => console.log('queueMicrotask'))` schedules a microtask to log `'queueMicrotask'`.
			- **Microtasks:**
				- `const results = await Promise.all([asyncFunc(), promise]);`:
					- `asyncFunc()` returns a `Promise` that resolves immediately with `'asyncFunc'`.
					- The `promise` resolves and its `.then()` handler logs `'then'`.
			- **Final Output:**
				- The `await` keyword pauses the async function, allowing the microtasks to run.
				- `console.log('script')` is executed in the main script.
				- Microtasks:
					- The `queueMicrotask` logs `'queueMicrotask'`.
		- **Execution Order**
			- `console.log('promise')` — synchronous within the `Promise` executor.
			- `console.log('async body')` — synchronous within the async function.
			- `console.log('script')` — synchronous in the main script.
			- Microtasks:
				- `queueMicrotask(() => console.log('queueMicrotask'))` — logs `'queueMicrotask'`.