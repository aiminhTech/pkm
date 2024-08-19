tags:: [[Deno]], [[Perfomance API]]

-
- ## Performance
	- https://docs.deno.com/api/web/~/Performance
	- ### `performance.now()`
		- https://docs.deno.com/api/web/~/Performance.now
		- Returns a current time from Deno's start in milliseconds.
		- ```ts
		  const t = performance.now();
		  console.log(`${t} ms since start!`);
		  ```