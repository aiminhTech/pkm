parent:: [[Testing]]
related:: [[DOM - Document Object Model]]

- **A type of software testing that focused on verifying how different parts of system work toghether**
  background-color:: blue
- Integration testing = **Do the parts work toghether correctly?**
	- Unit tests = test **1 piece in isolation**
	- Integration tests = test **combined pieces**
-
-
- ## DOM Testing
	- Focus on how our UI components render and behave in the DOM
	- Usually done in a simulated environment like [[jsdom]] or [[Happy DOM]]
	- Tests **component-level behavior**: rendering, text content, attributes, and user interactions
	- Often considered **integration or component testing**, not full E2E
	- **Example**
	  background-color:: red
	  collapsed:: true
		- ```javascript
		  import { screen } from '@testing-library/dom';
		  import userEvent from '@testing-library/user-event';
		  
		  describe('createButton', () => {
		    beforeEach(() => {
		      document.body.innerHTML = ''
		    })
		  
		    it('should create a button element', () => {
		      document.body.appendChild(createButton())
		      const btn = screen.getByRole('button', { name: 'Click Me' })
		  
		      expect(btn).toBeInTheDocument()
		    });
		  
		    it('should have the text "Click Me"', () => {
		      document.body.appendChild(createButton())
		      const btn = screen.getByRole('button', { name: 'Click Me' })
		  
		      expect(btn.textContent).toBe('Click Me')
		    });
		  
		    it('should change the text to "Clicked!" when clicked', async () => {
		      document.body.appendChild(createButton(), { name: 'Click Me' })
		      const btn = screen.getByRole('button')
		  
		      await userEvent.click(btn)
		      expect(btn.textContent).toBe('Clicked!')
		    });
		  });
		  
		  function createButton() {
		    const button = document.createElement('button');
		    button.textContent = 'Click Me';
		  
		    button.addEventListener('click', () => {
		      button.textContent = 'Clicked!';
		    });
		  
		    return button;
		  }
		  ```
	- ### Functions from Testing Library
		- #### Rendering `render()`
			- Mounts React component into a mock DOM for testing
				- ```javascript
				  render(<Counter />);
				  ```
		- #### Querying
			- All queries come from `screen` (recommended).
				- `screen.getByRole(query, options)`
					- Finds an element by its semantic role (button, heading, etc.). Throws if not found.
					- ```javascript
					  screen.getByRole('button', { name: /increment/i });
					  ```
				- `screen.getByTestId(id)`
					- Finds an element by its `data-testid` attribute.
					- ```javascript
					  screen.getByTestId('counter-count');
					  ```
		- #### User Interactions
			- From `@testing-library/user-event`
			- `userEvent.click(element)` - Simulates a user clicking the element
			- There are more: `type`, `hover`, `keyboard`, etc. but you only used `click` here
			- ```javascript
			  await userEvent.click(button);
			  ```