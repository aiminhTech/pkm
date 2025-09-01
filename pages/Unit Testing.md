parent:: [[Testing]]
related:: [[JavaScript]] 
technology:: [[Vitest]], [[Jest]]

- **A way to to check if a small part of code (usually a single function or method) works correctly**
  background-color:: blue
- Think of it like:
	- Our code is a big machine made of many small parts
	- A unit test checks one smamll part at a time to make sure it behaves as expected
-
- ## Happy Path
  collapsed:: true
	- The happy path is when everything works perfectly
	- **Example**
	  background-color:: red
		- ```js
		  import { describe, it, expect } from 'vitest';
		  
		  const add = (a, b) => {
		    return a + b
		  };
		  
		  describe('add', () => {
		    it('should add two positive numbers', () => {
		      expect(add(2, 2)).toBe(4)
		    })
		  });
		  ```
- ## Unhappy Path
  collapsed:: true
	- The unhappy path is when things go wrong, like invalid inputs, errors, or unexpected situations. Testing the unhappy path means making sure our code handles these problems gracefully
	- ### Invalid input
		- ```javascript
		  import { describe, it, expect } from 'vitest';
		  
		  const add = (a, b) => {
		    const numA = Number(a);
		    const numB = Number(b);
		  
		    if (isNaN(numA) || isNaN(numB)) {
		      throw new Error('Invalid input: not a number');
		    }
		  
		    return numA + numB;
		  }
		  
		  describe('add', () => {
		    it('should add two positive numbers', () => {
		      expect(add(2, 2)).toBe(4)
		    })
		  
		    it('should add two numbers as strings', () => {
		      expect(add('1', '1')).toBe(2)
		    })
		  
		    it('should throw an error if inputs are not numbers', () => {
		      expect(() => add(2, "foo")).toThrow('Invalid input: not a number')
		    })
		  });
		  
		  ```
-
- ## Testing Equality
  collapsed:: true
	- ### Referential equality
		- Checks whether **two variables point to the exact same object in memory**, not just that they have the same value. Just because they are basically the same, it does not mean they are actually the same
		- ```js
		  Sure => 1 === 1 and 'string' === 'string'
		  But => { foo: 1 } !== { foo: 1 } and [1,2,3] !== [1,2,3]
		  ```
		- Works for objects, arrays and functions (non-primitives)
	- ### `toBe`
	  collapsed:: true
		- Checks **strict equality**  `===`
		- Work best for primitives (numbers, strings, booleans)
		- Does not work well for objects or arrays, because it checks reference, not value
		- **Example**
		  background-color:: red
			- ```javascript
			  expect(2 + 2).toBe(4); // passes
			  expect({ a: 1 }).toBe({ a: 1 }); // fails (different object references)
			  ```
	- ### `toEqual`
	  collapsed:: true
		- Checks **deep equality**
		- Compares values inside objects or arrays, not the reference
		- Great for objects and arrays
		- **Example**
		  background-color:: red
			- ```javascript
			  expect({ a: 1 }).toEqual({ a: 1 }); // passes
			  expect([1, 2, 3]).toEqual([1, 2, 3]); // passes
			  ```
	- ### `toStrictEqual`
	  collapsed:: true
		- Like `toEqual` but **more strict**
			- Checks types strictly
			- Detects differences like `undefined` vs missing properties
		- **Example**
		  background-color:: red
			- ```javascript
			  expect({ a: undefined }).toEqual({}); // passes with toEqual
			  expect({ a: undefined }).toStrictEqual({}); // fails with toStrictEqual
			  
			  ```
	- ### `objectContaining`
		- Checks if an object **contains certain key-value pairs**, without nedding an exact match of the entire object
		- Useful when the object has **extra props** we dont care about => provides flexible partial matching
		- **Example**
			- ```javascript
			  const user = {
			    id: 1,
			    name: 'Alice',
			    age: 25,
			    role: 'admin'
			  };
			  
			  expect(user).toEqual(expect.objectContaining({
			    name: 'Alice',
			    role: 'admin'
			  })); // passes
			  
			  ```
		-
- ## Hooks
	- Functions that run automatically at specific points in our test suite
		- **`beforeEach`:** Runs before every test
		  id:: 68b580c1-3cd8-4c1e-a95c-9278f3a65ae8
		- **`afterEach`:** Runs after every test
		- **`beforeAll`:** Runs once before all tests
		- **`afterAll`:** Runs once after all tests
	- **Why use Hooks?**
		- Reduce code repetition
		- Set up test data or environments
		- Clean up resources after tests (like closing connections)
		- Testing Asynchronous Code
			- Many modern apps use async functions. Hooks can handle setup/cleanup.
			- Tests can use `async/await` with hooks
		- **Example**
		  background-color:: red
			- ```javascript
			  let user;
			  
			  beforeEach(async () => {
			    // Simulate fetching a user before each test
			    user = await fetchUserData(1); // async setup
			  });
			  
			  describe('User Tests', () => {
			    it('should have a name', () => {
			      expect(user.name).toBe('John Doe');
			    });
			  
			    it('should have an id', () => {
			      expect(user.id).toBe(1);
			    });
			  });
			  ```