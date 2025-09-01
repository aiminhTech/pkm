parent::  [[E2E Testing]]
relate:: [[Angular]], [[React]], [[Vue.js]], [[Mocha]], [[Chai]]

- https://www.cypress.io/
-
- ## 📔 Learning
	- [https://www.oreilly.com/library/view/cypress-automation-testing/9781835887080](https://www.oreilly.com/library/view/cypress-automation-testing/9781835887080)
	- [https://www.oreilly.com/library/view/end-to-end-web-testing/9781839213854/](https://www.oreilly.com/library/view/end-to-end-web-testing/9781839213854/)
	- [https://www.oreilly.com/library/view/mastering-angular-test-driven/9781805126089](https://www.oreilly.com/library/view/mastering-angular-test-driven/9781805126089)
	- [https://www.oreilly.com/search/?q=cypress&rows=100](https://www.oreilly.com/search/?q=cypress&rows=100)
-
- ## ✨ Features
	- Next generation frontend automation testing tool for modern web applications (React, Angular, Vue). It offers a fast, reliable and developer-friendly testing experience
	- ### Automatic Waiting
		- Cypress automatically waits for elements to appear, animations to complete and network requests to finish -  no need for manual `wait()` commands
	- ### Debuggability
		- Built-in developer tools with readable error messages and stack traces
		- Tests run directly in the browser with access to Chrome DevTools for debugging
	- ### Supports Multiple Testing Type
		- Cypress isn't just for E2E tests, it supports various types of tests
			- **End-to-End (E2E) Testing** #[[E2E Testing]]
			- **Component Testing** #[[Compontent Testing]]
			- **Integration Testing** #[[Integration Testing]]
			- **Unit Testing** #[[Unit Testing]]
	- ### Time Travel
		- Cypress takes snapshots at each step of test, allowing to hover over each command in the test runner and see exactly what happened in the browser at that point
	- ### Network Traffic Control
		- Intercept and stub HTTP requests and responses with `cy.intercept()`, enabling testing of different backend scenarios withour changing the backend itself
	- ### Flake Detection
		- Helps identify and reduce flaky tests using built-in retry logic and visual feedback when tests are inconsistent
		- #+BEGIN_CAUTION
		  What are Flaky Tests?
		  **Flaky tests** are tests that **sometimes pass and sometimes fail** — even when the code hasn’t changed.
		  
		  #+END_CAUTION
- ## </> Syntax
	- Cypress tests typically follow a **three-phases structure**
		- **Arrange (Given)** - Set up the application state
		  logseq.order-list-type:: number
			- Prepare the app, load necessary data, visit a page or configure conditions
		- **Act (When)** - Take an action
		  logseq.order-list-type:: number
			- Simulate user interactions like clicking, typing or selecting
		- **Assert (Then)** - Make assertions or verifications
		  logseq.order-list-type:: number
			- Confirm that the expected result occured
	- ### 🧪 Test Structure
		- Cypress use [[Mocha]] to organize test structure
		- #### 🔸 Test Suite
			- Group related tests
				- `describe()`: Defines a test suite
				- `context()`: Alias for `describe()`, useful for readability
		- #### 🔹 Test Cases
			- Define individual test scenarios
				- `it()`: Defines a single test
				- `specify()`: Alias for `it()`, less commonly used.
		- #### ✔️ Assertions & Verification
			- Cypress uses [[Chai]] for assertions, with extensions specific to DOM and browser testing.
			- `expect()` – Functional style assertions.
			- `should()` – Chainable style, often used directly on Cypress commands.
			-
-
- ## Assertions
	- Assertions are commands that ==verify== if ==something is true== during a test run. They check the state of your application or elements on the page and determine whether the test should pass or fail based on those conditions
		-
		-