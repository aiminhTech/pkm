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
		      cy.location('pathname').should('contain.text', '/sign-in');
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
-
- ## Cypress Tasks
	- Cypress tests run inside the browser, but sometimes we need to perform actions outside the browser like seeding a database, clearing test data or reading files => That is where tasks come in
	- Tasks are defined on the Node.js server side (in `cypress.config.ts` or `cypress/plugins/index.ts`) an we call them from test using `cy.task()`
	- ### Why use?
	- ### How to define?
		- ```javascript
		  // cypress.config.ts
		  const { defineConfig } = require('cypress');
		  
		  module.exports = defineConfig({
		    e2e: {
		      setupNodeEvents(on, config) {
		        on('task', {
		          // Example: seed the database
		          seedDatabase() {
		            // pretend this calls your DB seeding logic
		            console.log('Database seeded!');
		            return null;
		          },
		  
		          // Example: return environment info
		          getEnv() {
		            return process.env.NODE_ENV;
		          }
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
		  
		    it('retrieves environment info', () => {
		      cy.task('getEnv').then((env) => {
		        expect(env).to.equal('test'); // assert environment
		      });
		    });
		  });
		  
		  ```