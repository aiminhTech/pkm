tags:: [[HTML]], [[CSS]], [[DOM - Document Object Model]]

- https://frontendmasters.com/courses/web-components/
- https://htmlwithsuperpowers.netlify.app/
-
- ## Overview
  collapsed:: true
	- A **Web Component** is a reuseable, custom-built piece of a webpage that we can use like a regular HTML element.
	- **Template and Slots**:** Templates** define reuseable chunks of HTML that can be inserted into a page**. Slots** act like placeholders inside a web component where custom content can be placed
	- **Custom Elements:** These are new HTML tags created, such as `<my-button>`. The apprearance and behavior are defined using JS
	- **Shadow DOM:** A special hidden part inside a custom element that keeps it styles and markup seperate from the rest of the page. This seperation helps avoid style conflicts and makes the components self-contained
	- **ES (ECMAScript) Modules:** Modules organize JS code into seperate files with import/export capabilities. This keeps web components code clean and reusable
	- ### Why use?
		- It works with plain HTML/JS, React, Vue, Angular, etc.
		- Keep markup, logic  and style in 1 place without global CSS conflicts => **Encapsulation**
		- Drop the same component into multiple projects => **Reusebility**
		- Can provide a graceful fallback when JS is disabled
	- **==Basic Usage:==** https://htmlwithsuperpowers.netlify.app/using/
-
- ## Lifecycle
	- ### 1. `constructor()`
		- Called **when the element is created**.
		- Good for **initial setup** like creating a shadow DOM or initializing properties.
		- ```js
		  constructor() {
		  super();
		  this.attachShadow({ mode: 'open' });
		  }
		  ```
	- ### 2. `connectedCallback()`
		- Called **when the element is added to the DOM**.
		- Good for **fetching data, adding event listeners**, or starting animations.
		- ```js
		  connectedCallback() {
		  console.log('Added to page');
		  }
		  ```
	- ### 3. `disconnectedCallback()`
		- Called **when the element is removed from the DOM**.
		- Good for **cleanup**, like removing event listeners or stopping timers.
		- ```js
		  disconnectedCallback() {
		  console.log('Removed from page');
		  }
		  ```
	- ### 4. `attributeChangedCallback(name, oldValue, newValue)`
		- Called **when an observed attribute changes**.
		- Useful for **reacting to property changes**.
		- ```js
		  static get observedAttributes() { return ['title']; }
		  
		  attributeChangedCallback(name, oldValue, newValue) {
		  console.log(`${name} changed from ${oldValue} to ${newValue}`);
		  }
		  ```
	- ### 5. `adoptedCallback()`
		- Called **when the element is moved to a new document** (rarely used)
- ## Using Components
  collapsed:: true
	- **Web Components Examples**: https://htmlwithsuperpowers.netlify.app/using/examples/two-up.html
	- **generic-components**: https://genericcomponents.netlify.app/
	- **awesome-standalones**: https://github.com/davatron5000/awesome-standalones
	- **GoogleChromeLabs:** https://github.com/GoogleChromeLabs
	- ### Some Components
		- ### `<a-scene>`
			- **Purpose:** Root element for an A-Frame 3D scene
			- **Features:**
				- Sets up the **WebGL/Three.js renderer** automatically.
				- Handles **camera, lights, and VR/AR support** out of the box.
				- Allows you to declare 3D entities in HTML like `<a-box>`, `<a-sphere>`, `<a-camera>`.
		- ### `<generic-tabs>`
			- Converts **semantic HTML** (like a `<section>` with `<h2>` headers) into **accessible, keyboard-navigable tabs**.
			- https://genericcomponents.netlify.app/generic-tabs/demo/
- ## DOM #[[DOM - Document Object Model]]
	- ### Light DOM styling
	  collapsed:: true
		- Content placed inside a **`<slot>`** is part of the **light DOM**.
		- CSS from outside the web component can style these elements just like normal HTML.
		- **Example**:
			- The `<p>` element is styled because it remains part of the page’s DOM.
			- ```html
			  <my-card>
			    <p class="red-text">I’m in the slot!</p>
			  </my-card>
			  
			  <style>
			    .red-text { color: red; } /* ✅ works */
			  </style>
			  ```
	- ### Shadow DOM styling
	  collapsed:: true
		- Elements inside the **shadow DOM** are **isolated** from external CSS.
		- Styles from outside the component cannot affect them.
		- **Example**:
			- ```js
			  shadow.innerHTML = `<p>I’m hidden!</p>`;
			  
			  // This CSS will not affect it:
			  p { color: red; } /* ❌ has no effect on shadow DOM <p> */
			  ```
		- **Reason**: Shadow DOM provides **encapsulation**, preventing external CSS from accidentally changing the component’s appearance.
	- ### Shadow DOM Styling Options
	  collapsed:: true
		- #### CSS Custom Properties (Variables)
			- Web components can use CSS variables defined outside the shadow DOM
			- These variables **can pass values into the shadow DOM**
			- ```css
			  :root {
			    --main-color: blue;
			  }
			  ```
			- ```js
			  shadow.innerHTML = `<p style="color: var(--main-color)">Hello</p>`;
			  ```
		- #### Parts
			- Shadow DOM elements can expose specific parts using the `part` attribute
			- **Example
				- In the component:**
					- ```html
					  <button part="my-button">Click me</button>
					  ```
				- Outside the component, the **`::part()` pseudo-element** can style it:
					- ```css
					  my-card::part(my-button) {
					    background-color: green;
					    color: white;
					  }
					  
					  ```
	- ### New CSS syntax
	  collapsed:: true
		- `:host`
			- Targets the **custom element itself from inside its shadow DOM
			- ```css
			  // This styles <my-card> itself.
			  :host {
			    display: block;
			    border: 1px solid black;
			  }
			  
			  ```
		- `:host(<selector>)`
			- Targets the host **only if it matches a condition**
			- ```css
			  // Only <my-card class="highlight"> gets a red border.
			  :host(.highlight) {
			    border-color: red;
			  }
			  ```
		- `:host-context()`
			- Styles the host element **based on its ancestors** (An **ancestor** is any element that is **above another element in the HTML hierarchy**.)
			- ```css
			  // If an ancestor has class dark-mode, the component text turns white.
			  :host-context(.dark-mode) {
			    color: white;
			  }
			  ```
		- `::slotted()`
			- Styles **light DOM content** that is inserted into a `<slot>`
			- ```css
			  // Any <p> passed into a slot gets blue text.
			  ::slotted(p) {
			    color: blue;
			  }
			  ```
		- `@property` (CSS Custom Property Definition)
			- Allows defining **custom properties** with type, initial value, and inheritance
			- ```css
			  // This makes --main-color usable and more controllable inside the shadow DOM.
			  @property --main-color {
			    syntax: '<color>';
			    inherits: true;
			    initial-value: black;
			  }
			  ```
	- ### Native CSS Module Scripts
		- Normally, web component styles are written **inside the component**.
		- Using **native CSS module scripts**, a CSS file can be **imported like a JavaScript module**.
		- The imported CSS can be applied to the component using **`adoptedStyleSheets`**, which is a special way to attach styles directly to a shadow DOM.
		- **Benefits:**
			- CSS is **separate** from JavaScript, keeping code cleaner.
			- The same stylesheet can be **shared across multiple components**, so changes are easy to maintain.
		- **Example:**
			- Create a CSS file as a module:
				- ```css
				  /* styles.css */
				  :host {
				    display: block;
				    border: 2px solid black;
				    padding: 10px;
				  }
				  p {
				    color: blue;
				  }
				  ```
			- Import the CSS in the web component using a module script:
				- ```html
				  <script type="module">
				    import styles from './styles.css' assert { type: 'css' };
				  
				    class MyCard extends HTMLElement {
				      constructor() {
				        super();
				        const shadow = this.attachShadow({ mode: 'open' });
				        shadow.adoptedStyleSheets = [styles]; // Apply the imported CSS
				        shadow.innerHTML = `<p>Hello from the card!</p>`;
				      }
				    }
				  
				    customElements.define('my-card', MyCard);
				  </script>
				  
				  <my-card></my-card>
				  ```
	-
- ## JS Libs
	-