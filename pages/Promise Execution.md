tags:: [[Javascript]], [[JS EventLoop]]

- ## Learn Videos & Links
	- {{video https://www.youtube.com/watch?v=Xs1EMmBLpn4}}
- ## Promise
	- The new promise constructor creates a new promise object, which contains internal slots such as **promise state, promise result, promise fulfill reactions, and promise reject reactions**.
	- We can resolve a promise by calling resolve and reject it by calling reject, setting the state and result accordingly.
	- The promise fulfill reactions and promise reject reactions are where the real power of promises comes in. These fields contain promise reaction records, created by chaining a then or catch method to the promise, which contains a handler.
	- When the **promise is resolved**, the handler is added to the **microtask queue**, which executes the asynchronous part of the promise.
	- Asynchronous tasks can be initiated in the promise constructor, with callbacks used to resolve or reject the promise once the task is complete.
-