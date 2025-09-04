parent::  [[E2E Testing]]
related:: [[Angular]], [[React]], [[Vue.js]], [[Mocha]], [[Chai]], [[Playwright]] 
link:: https://www.cypress.io/

-
- **Tool for [[E2E Testing]] of any browser-based web application**
  background-color:: blue
- Features
- ## 📔 Learning
	- [https://www.oreilly.com/library/view/cypress-automation-testing/9781835887080](https://www.oreilly.com/library/view/cypress-automation-testing/9781835887080)
	- [https://www.oreilly.com/library/view/end-to-end-web-testing/9781839213854/](https://www.oreilly.com/library/view/end-to-end-web-testing/9781839213854/)
	- [https://www.oreilly.com/library/view/mastering-angular-test-driven/9781805126089](https://www.oreilly.com/library/view/mastering-angular-test-driven/9781805126089)
	- [https://www.oreilly.com/search/?q=cypress&rows=100](https://www.oreilly.com/search/?q=cypress&rows=100)
	- https://frontendmasters.com/courses/cypress/
		- https://github.com/stevekinney/cypress
	-
- ## Features
	- **Time-travelling**: the ability to view state of application at each step of a test
	- **Real-time reloads**: tests automatically re-runs as we make changes
	- **Automatic waiting**: no need to add explicit waits or sleeps. Cypress waits for elements to be ready
-
- ## Installation
	- https://docs.cypress.io/app/get-started/install-cypress
	- **IGE**: https://wiki.ipip.ch/spaces/SWE/pages/131523249/E2E+Testing+mit+Cypress#E2ETestingmitCypress-SetupCypress
	- ### Running Test
		- ```bash
		  // Interactive mode (GUI)
		  npx cypress open
		  
		  // Headless mode (CLI, for CI/CD)
		  npx cypress run
		  ```
	- ### First Open Cypress
		- When we first run Cypress, it will:
			- Creates a `cypress/` dir. This includes folders like: `integration/` (older versions) or `e2e/` (new version), `fixtures/`, `support/`
			- Creates a config files
				- Cypress v9 and below: `cypress.json`
				- Cypress v10+: `cypress.config.ts`
			- Adds example test files
-
- ## Basics
  collapsed:: true
	- ### `cy.get`
		- Find elements by CSS selector
		- ```javascript
		  // finds the list 
		  cy.get('ul')
		  ```
	- ### `cy.contains`
		- Find elements that contain specific text
		- ```javascript
		  // finds an element with text "Submit" 
		  cy.contains('Submit').click();
		  ```
	- ### `should()`
		- Make an assertion about an element
		- ```javascript
		  // checks that the form exists and the email input is visible
		  cy.get('form').should('exist');
		  cy.get('input[name="email"]').should('be.visible');
		  ```
	- ### `type()`
		- Type text into input fields
		- ```javascript
		  // types into the email input field.
		  cy.get('input[name="email"]').type('hello@example.com');
		  ```
	- ### `find()`
		- Find child elements inside a parent element
		- ```javascript
		  // finds the password input inside the form and types into it.
		  cy.get('form').find('input[name="password"]').type('mypassword');
		  ```
	- ### `click()`
		- Click on a button or element
		- ```javascript
		  // clicks the first <button> found
		  cy.get('button').click();
		  ```
	- ### `each()`
		- Loop over multiple elements
		- ```javascript
		  // loops through each <li> in a list 
		  cy.get('ul li').each(($el) => {
		    
		  });
		  ```
	- ### `cy.wrap()`
		- Wrap a DOM element so we can use Cypress commands on it
		- ```javascript
		  // wraps each list item to click it
		  cy.get('ul li').each(($el) => {
		    cy.wrap($el).click();
		  });
		  ```
	- ### `invoke`
		- Call a method or get a property on a DOM element or jQuery object
		- Often used to read or change values that are not directly accessible through Cypress cmds
		- ```javascript
		  cy.get('button').invoke('text').then((text) => {
		    expect(text).to.eq('Submit'); // check button text
		  });
		  ```
- ## Aliases
  collapsed:: true
	- **Store elements or values** and **reuse** them later in the test
	- Live only for the current text (`it`block)
	- Useful for **complex pages** with multiple elements you reuse.
	- You can also alias **requests** (for API testing) or **fixtures** (test data).
	- ```javascript
	  // creating 
	  cy.get('form').as('myForm')
	  
	  // using
	  cy.get(''@myForm').find('button').click()
	  ```
-
- ## Testing Complex Input
  collapsed:: true
	- ### Select Box
		- Use `select()` method to choose an option
		- ```javascript
		  it('should select an option from the select and verify it', () => {
		      cy.get('@restaurant-filter').select('Taco Bell');
		      cy.get('@restaurant-filter').should('have.value', 'Taco Bell');
		    });
		  ```
	- ### Range Slider
		- Set the value with `invoke('val', value)` and trigger a change event
		- ```javascript
		   it('should set the range and verify it', () => {
		      cy.get('@rating-filter').invoke('val', 7).trigger('input');
		      cy.get('@rating-filter').should('have.value', 7);
		    });
		  ```
	- ### Checkbox
		- Use `check` and `uncheck` for  checkboxes and radios buttons
		- ```javascript
		  it('should check the checkbox and verify it', () => {
		    cy.get('input[type="checkbox"]').check().should('be.checked');
		  });
		  ```
- ## Generating Tests
  collapsed:: true
	- We can **dynamically generate Cypress tests** using JavaScript loops. This is useful when you have multiple similar elements (like checkboxes) and want to avoid repeating code.
	- ```javascript
	  const checkboxIds = ['subscribe', 'alerts', 'newsletter'];
	  
	  describe('Dynamic checkbox tests with for-in', () => {
	    const checkboxIds = ['subscribe', 'alerts', 'newsletter'];
	  
	    for (const i in checkboxIds) {
	      const id = checkboxIds[i];
	  
	      it(`should check the ${id} checkbox`, () => {
	        cy.visit('/settings-page');
	        cy.get(`#${id}`).check().should('be.checked');
	      });
	    }
	  });
	  
	  ```
	- ### Advantages
		- **Avoids repeating code** for multiple elements
		- Makes tests **scalable** if new checkboxes are added
		- Easy to combine with other Cypress commands like `.uncheck()` or `.should('not.be.checked')`
- ## Checking the current Path
  collapsed:: true
	- Checking a page's URL can be more reliable then querying DOM content
	- ### Check the URL
		- Using `cy.location()` method to query different parts of the current URL
		- `pathname` returns the path part of the URL
		- We ca also check `href`, `host`, `protocol`, etc.
		- ```javascript
		  // Check that the path is correct
		   it('should navigate to "/sign-in" when you click the "Sign In" button', () => {
		      cy.get('[data-test="sign-in"]').click();
		      cy.location('pathname').should('equal', '/sign-in');
		    });
		  ```
	- ### Check the page title
		- Use `cy.title()`
		- Useful to ensure you are on the **expected page**, especially after navigation
		- ```javascript
		  cy.title().should('eq', 'Login Page');
		  ```
- ## Form Validation
  collapsed:: true
	- ### Checking for the `:invalid` pseudo-class
		- Browser apply the `:invalid` CSS psesudo-class when an input fails validation
		- ```javascript
		  it('should require an email', () => {
		      cy.get('@submit').click();
		  	cy.get('[data-test="sign-up-email"]:invalid').should('exist')   
		  });
		  ```
	- ### Checking `validationMessage`
		- Every input field in HTML5 has a `validationMessage` prop that tells why the field is invalid
		- The actual msg can vary by browser and locale,
		- ```javascript
		  it('should require an email', () => {
		      cy.get('@submit').click();
		    
		  	cy.get('[data-test="sign-up-email"]:invalid')
		        .invoke('prop', 'validationMessage')
		        .should('contain', 'Please fill out of this field');  
		  }); 
		  ```
	- ### Checking the `validity`-prop
		- The `validity` obj provides detailed info on why an input is invalid
		- ```javascript
		  it('should require an email', () => {
		      cy.get('@submit').click();
		    
		      cy.get('[data-test="sign-up-email"]:invalid')
		        .invoke('prop', 'validity')
		        .its('valueMissing')
		        .should('be.true');
		  }); 
		  ```
	- ### More examples
		- ```javascript
		   it('should require that the email actually be an email address', () => {
		      cy.get('@email').type('notanemail');
		  
		      cy.get('@submit').click();
		  
		      cy.get('[data-test="sign-up-email"]:invalid').as('invalidEmail')
		  
		      cy.get('@invalidEmail')
		        .invoke('prop', 'validationMessage')
		        .should('not.be.empty');
		  
		      cy.get('@invalidEmail')
		        .invoke('prop', 'validity')
		        .its('typeMismatch')
		        .should('be.true')
		    });
		  
		    it('should require a password when the email is present', () => {
		      cy.get('@email').type('valid@email.com');
		  
		      cy.get('[data-test="sign-up-password"]:invalid').as('invalidPassword');
		  
		      cy.get('@invalidPassword')
		        .invoke('prop', 'validity')
		        .its('valueMissing')
		        .should('be.true')
		    });
		  ```
-
- ## Cypress Tasks
  collapsed:: true
	- Cypress tests run inside the browser, but sometimes we need to perform actions outside the browser like seeding a database, clearing test data or reading files => That is where tasks come in
	- Tasks are defined on the Node.js server side (in `cypress.config.ts` or `cypress/plugins/index.ts`) an we call them from test using `cy.task()`
	- ### Why use?
	- ### How to define?
		- ```javascript
		  // cypress.config.ts
		  import { defineConfig } from 'cypress';
		  import seed from './prisma/seed.cjs';
		  
		  export default defineConfig({
		    e2e: {
		      baseUrl: 'http://localhost:3000',
		      setupNodeEvents(on, config) {
		        on('task', {
		          seed() {
		            return seed();
		          },
		        });
		      },
		    },
		  });
		  
		  
		  ```
	- ### Usage
		- ```javascript
		  describe('Using tasks in Cypress', () => {
		    it('seeds the database before running tests', () => {
		      cy.task('seedDatabase'); // runs the server-side task
		      cy.visit('/login');
		    });
		  });
		  
		  ```
- ## Cypress Command
	- We can also define our own cmds inside `cypress/support/command.js`
	- This allows to:
		- Reuse **common routines** (e.g., login, form filling).
		- Keep test files shorter and cleaner.
		- Pass arguments to commands so they’re flexible and reusable.
	- ```javascript
	  /// <reference types="cypress" />
	  
	  Cypress.Commands.add('signIn', (user) => {
	    cy.visit('/echo-chamber/sign-up');
	    cy.get('[data-test="sign-in-email"]').type(user.email);
	    cy.get('[data-test="sign-in-password"]').type(user.password);
	    cy.get('[data-test="sign-in-submit"]').click();
	  });
	  
	  
	  // use in tests
	  describe("User dashboard", () => {
	    it("logs in and visits dashboard", () => {
	      cy.login("alice", "mypassword");   // ✅ custom command
	      cy.url().should("include", "/dashboard");
	    });
	  });
	  
	  ```
-
-
- ## Network Request `cy.intercept()`
  collapsed:: true
	- External systems (Google, Auth0, third-party APIs) aren’t always reliable or testable
	- Internal APIs may be owned by other teams, slow, or need seeded databases
	- Using real servers = true end-to-end tests but slower + harder to set up
	- Stubbing with `cy.intercept()` = faster, deterministic, test edge cases easily
	- ### Spy (just listen to  reqs)
	  collapsed:: true
		- ```js
		  // no response is changed, just verify the req happened
		  cy.intercept('GET', '/users/*').as('getUser');
		  
		  cy.visit('/profile/1');
		  cy.wait('@getUser').its('response.statusCode').should('eq', 200);
		  
		  ```
	- ### Stub with static data
	  collapsed:: true
		- ```js
		  // Return hardcoded response
		  cy.intercept('GET', '/users/*', [{ username: 'Jimi', id: 1 }]);
		  
		  // Return data from fixture
		  cy.intercept('GET', '/activities/*', { fixture: 'activities.json' });
		  
		  ```
	- ### Stub with status codes and headers
	  collapsed:: true
		- Useful for testin error-handling flows
		- ```js
		  cy.intercept('/not-found', {
		    statusCode: 404,
		    body: '404 Not Found!',
		    headers: { 'x-not-found': 'true' }
		  });
		  ```
	- ### Use a routeHandler (dynamic control)
	  collapsed:: true
		- ```js
		  // Assert request payload
		  cy.intercept('POST', '/greatest-bands', (req) => {
		    expect(req.body).to.include('Oasis');
		  });
		  
		  // Stub dynamic response
		  cy.intercept('POST', '/greatest-bands', (req) => {
		    req.reply({ body: 'We intercepted this request!' });
		  });
		  
		  ```
	- ### Advanced req lifecycle hook
	  collapsed:: true
		- ```js
		  cy.intercept('GET', '/users', (req) => {
		    req.on('before:response', (res) => {
		      res.send({ body: 'We modified this response!' });
		    });
		  
		    req.on('response', (res) => {
		      console.log('Got response from server');
		    });
		  
		    req.on('after:response', (res) => {
		      console.log('Response sent to browser');
		    });
		  });
		  
		  ```
	- ### Fixtures
	  collapsed:: true
		- Predefined **dummy data** that Cypress uses instead of a real API response.
		- They let us control test data so your tests are **fast, predictable, and isolated**.
		- Useful when:
			- You don’t care about testing the API itself
			- You only want to test **how your app handles the data** it receives
		- ### Inline
			- Quick and easy when only need small dummy data
			- ```js
			  cy.intercept('GET', '/users', {
			    body: [{ id: 1, username: 'Alice' }]
			  });
			  
			  ```
		- ### External fixture files
			- Place a JSON file inside `cypress/fixtures/activities.json`
			- ```json
			  [
			    { "id": 1, "activity": "Running" },
			    { "id": 2, "activity": "Swimming" }
			  ]
			  ```
			- ```javascript
			  describe('Activities page', () => {
			    it('displays mocked activities', () => {
			      cy.intercept('GET', '/activities', { fixture: 'activities.json' }).as('getActivities');
			  
			      cy.visit('/activities');
			      cy.wait('@getActivities');
			  
			      cy.contains('Running').should('be.visible');
			      cy.contains('Swimming').should('be.visible');
			    });
			  });
			  ```
- ## Cookies & Sessions
	- Cookies are often used for **authentication tokens**, **user preferences**, or **session management**.
	- Instead of always logging in through the UI, you can **mock cookies directly** → faster tests.
	- Cypress provides built-in commands:
		- `cy.getCookie()` → read a single cookie
		- `cy.getCookies()` → read all cookies
		- `cy.setCookie()` → write a cookie
		- `cy.clearCookie()` / `cy.clearCookies()` → remove cookies
	- ### Examples
		- ```javascript
		  /// <reference types="cypress" />
		  
		  // Helper functions to fake JWT encoding/decoding
		  const encodeToken = (payload) => Buffer.from(JSON.stringify(payload)).toString('base64');
		  const decodeToken = (token) => JSON.parse(Buffer.from(token, 'base64').toString('utf-8'));
		  
		  const user = { email: 'test@example.com', id: 1 };
		  
		  describe('Cookie-based login', () => {
		    it('logs in using UI and checks the cookie', () => {
		      cy.visit('/sign-in');
		  
		      // Pretend we have a login form
		      cy.signIn()
		  
		      // Check that app sets a cookie
		      cy.getCookie('jwt').should('exist').then((cookie) => {
		        const value = decodeToken(cookie.value);
		        expect(value.email).to.equal(user.email);
		      });
		    });
		  
		    it('logs in by setting cookie directly', () => {
		      // Skip the UI, just set the cookie
		      cy.setCookie('jwt', encodeToken(user));
		  
		      cy.visit('/dashboard');
		  
		      // App should think we’re logged in
		      cy.contains(`Signed in as ${user.email}`);
		    });
		  });
		  
		  ```