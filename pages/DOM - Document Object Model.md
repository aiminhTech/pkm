-
- The **DOM** is like a map of your webpage.
- It shows all the HTML elements (like `<div>`, `<p>`, `<button>`) as objects that JavaScript can **see and change**.
- ```html
  <p>Hello!</p>
  ```
- In the DOM, JavaScript can do:
	- ```js
	  document.querySelector('p').textContent = "Hi!";
	  ```
-
- ## Light DOM
	- **Light DOM** is just the **normal HTML you write** in your page.
	- It's what you see in your HTML file and in the browser’s DOM inspector.
	- **Example**:
		- The `<p>` inside `<my-card>` is in the **light DOM**.
		- ```html
		  <my-card>
		    <p>Content here</p>
		  </my-card>
		  
		  ```
-
- ## Shadow DOM
	- **Shadow DOM** is like a **hidden mini-DOM** inside a component.
	- It **hides its HTML and CSS** so outside code can't mess with it.
	- **Example:**
		- Now, `<p>Shadow content</p>` is **in the shadow DOM**, not light DOM.
		- **Why use it?**
			- Encapsulation: Styles and scripts inside shadow DOM **won’t affect the rest of the page**.
		- ```js
		  const card = document.querySelector('my-card');
		  const shadow = card.attachShadow({ mode: 'open' });
		  shadow.innerHTML = `<p>Shadow content</p>`;
		  ```
-
- ## Summary
	- |Type|Definition|Example|
	  |--|--|--|
	  |DOM|Whole page map|`document.body`|
	  |Light DOM|Normal HTML|`<p>Hello</p>`|
	  |Shadow DOM|Hidden mini-DOM inside a tag|Custom component HTML & CSS|