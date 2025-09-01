parent:: [[Testing]]
related:: [[Unit Testing]]
tags:: [[Vitest]]

-
- Test Doubles are **fake versions of functions, objects, or modules** that replace real code during testing.
  background-color:: blue
- They let you **control, observe, or isolate behavior** without relying on real dependencies like APIs, databases, or timers.
- Think of them as “stand-ins” for parts of your app that you **don’t want to call for real** during a test.
-
- **Stub:** fake output only.
- **Mock:** fake + track calls.
- **Spy:** watch real function calls.
-
- ## Spies
	- **Watch an existing function**
	- Lets the original function run normally but tracks calls
	- ```javascript
	  import { describe, it, expect, vi } from 'vitest';
	  
	  const obj = {
	    greet: (name) => `Hello ${name}`
	  };
	  
	  describe('spy example', () => {
	    it('observes function calls', () => {
	      const spy = vi.spyOn(obj, 'greet');
	  
	      const message = obj.greet('Alice'); // original function runs
	  
	      expect(spy).toHaveBeenCalled();
	      expect(spy).toHaveBeenCalledWith('Alice');
	      expect(message).toBe('Hello Alice');
	  
	      spy.mockRestore(); // clean up
	    });
	  });
	  
	  ```
-
- ## Mocks
	- **Fakes function and records calls**
	- Can check how it was called
	- ```javascript
	  import { describe, it, expect, vi } from 'vitest';
	  
	  describe('mock example', () => {
	    it('tracks calls', () => {
	      const mockFn = vi.fn();
	  
	      mockFn('hello');
	      mockFn('world');
	  
	      expect(mockFn).toHaveBeenCalled(); // called at least once
	      expect(mockFn).toHaveBeenCalledTimes(2);
	      expect(mockFn).toHaveBeenCalledWith('hello');
	    });
	  });
	  
	  ```
-
- ## Stubs
	- **Returns controlled data**
	- Just fakes a function's return value
	- ```javascript
	  import { describe, it, expect } from 'vitest';
	  
	  describe('stub example', () => {
	    it('returns fake data', () => {
	      const fetchData = () => 'real data';
	      const stub = () => 'fake data';
	  
	      expect(stub()).toBe('fake data');
	    });
	  });
	  ```
-
- ## Mock Dependencies
	- When we write tests for components, they often **depend on other modules or services** (like APIs, utility functions, or context providers).
	- **Stubs and mocks** let you **replace these dependencies** with fake versions so your tests are **predictable and isolated**.
	- **Example**: instead of calling a real API, you return fake data immediately
	- ### Why be careful
		- Mocking **too many dependencies** can make tests **unrealistic**.
		- The component may pass tests, but in real usage, it could fail because real dependencies behave differently.
		- Tests become **harder to maintain**.
	- ### Better Approach: Dependency Injection
		- Instead of importing dependencies directly inside a component, **pass them as props or parameters**.
		- This allows you to **easily swap in mocks or stubs** for testing **without changing the component code**.
	- ### Examples
		- ```javascript
		  // Component with a dependency
		  // Greeting.js
		  export function Greeting({ fetchUser }) {
		    const user = fetchUser();
		    return `<h1>Hello ${user.name}</h1>`;
		  }
		  
		  // Test with a stub
		  import { describe, it, expect } from 'vitest';
		  import { Greeting } from './Greeting';
		  
		  describe('Greeting component', () => {
		    it('renders with a fake user', () => {
		      const fakeFetch = () => ({ name: 'Alice' }); // stub
		      const output = Greeting({ fetchUser: fakeFetch });
		  
		      expect(output).toBe('<h1>Hello Alice</h1>');
		    });
		  });
		  
		  ```