tags:: [[Javascript]]

- https://examples.deno.land/web-workers
- https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API
- Web Workers are a simple means for web content to run scripts in background threads. The worker thread can perform tasks without interfering with the user interface.
-
- ## Example
	- ### `webworker.htm`
	  collapsed:: true
		- which create worker to run an expensive operation on worker thread instead of running on the main thread.
		- ```html
		  !DOCTYPE html>
		  <html>
		  <head>
		      <meta charset="utf-8">
		      <meta name="viewport" content="width=device-width">
		      <title>Web Workers Example</title>
		      <script>
		          let myWorker;
		          function startWorker(){
		              var para = document.createElement("P");
		              para.innerText = "Worker Started";
		              document.body.appendChild(para);
		              if (window.Worker) {
		                  myWorker = new Worker('worker.js');
		                  myWorker.onmessage = function (e) {
		                      var para = document.createElement("P");
		                      para.innerText = e.data;
		                      document.body.appendChild(para);
		                  };
		              }
		          }
		          function terminateWorker(){
		              if(myWorker!=undefined){
		                  myWorker.terminate();
		                  myWorker=undefined;
		                  var para = document.createElement("P");
		                  para.innerText = "Worker Terminated";
		                  document.body.appendChild(para);
		              }
		          }
		          function checkBlocking() {
		              var para = document.createElement("P");
		              para.innerText = "It works, not blocked by CPU expensive operation";
		              document.body.appendChild(para);
		          }
		      </script>
		      <style>
		          button {
		              display: inline-block;
		              padding: 10px 20px;
		              background: #2196F3;
		              color: white;
		              cursor: pointer;
		              border: none;
		              font-size: 16px;
		              margin: 30px;
		          }
		      </style>
		  </head>
		  
		  <body>
		      <button onclick="startWorker()">Start Worker</button> <br>
		      <button onclick="terminateWorker()">Terminate Worker</button><br>
		      <button onclick="checkBlocking()">Test browser responsive</button>
		  </body>
		  
		  </html>
		  ```
	- ### `worker.js`
		- which holds the expensive CPU operation task and communicates with worker.html file after task completion
		- ```js
		  let i = 0;
		  
		  let start = Date.now();
		  function count() {
		      // some heavy job here
		      for (let j = 0; j < 1e9; j++) {
		          i++;
		      }
		      postMessage("Task took " + (Date.now() - start) + 'ms');
		  }
		  count();
		  ```
- After running above code you will notice webworker works efficiently without blocking user interface or from rendering.
-