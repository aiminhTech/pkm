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
	- Provide interfaces to interact with browser feature
	- Allow offloading of long-running tasks to the browser, preventing program freezing.
- ## Task queues
	- **Callback-based web APIs**, like geolocation and setTimeout, use callbacks to handle asynchronous tasks.
	  id:: 6628d078-2193-4df1-9e74-f4acbb183626
	- Callback functions are registered and pushed to the task queue when the task is completed.
	- The event loop checks if the call stack is empty and then moves the first available task from the task queue to the call stack for execution.
- ## Microtask queue
  id:: 6628d019-6516-4e58-a62f-461d7bf7c526
	- **Promise-based web APIs**, like fetch, use promises to handle asynchronous tasks.
	- Promise reactions, such as then and catch callbacks, are pushed to the microtask queue
	- The event loop prioritizes the microtask queue, executing all tasks from the microtask queue before moving to the task queue.
- ## Event Loop
	- An endless loop waits for tasks, executes them, sleeps until another task comes.
	- It manages the execution of tasks in the JS runtime environment
	- When an async operation is initiated, such as reading a file or making an API call, the event loop continues to run other tasks while 
	  waiting for these asynchronous operations to complete.
	- The event loop consists of multiple components, including the call stack, callback queue, and microtask queue
	- Ensures that the microtask queue is empty before moving to the task queue.
	- ![image.png](../assets/image_1714372336344_0.png)