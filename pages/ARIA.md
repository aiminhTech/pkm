tags:: [[HTML]], [[Web Accessibility]]

- alias:: Accessible Rich Internet Applications
- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA
- **Accessible Rich Internet Applications** is a set of roles and attributes that define ways to make web content and web applications (especially those developed with JavaScript) more accessible to people with disabilities.
-
- ## ARIA Labels
	- Is an attribute used in HTML to **provide an accessible name** for elements that don't have visible text. It helps screen readers **announce the purpose of the element**
	- Often used on **buttons, icons, or interactive elements** that only have images or symbols
	- Use `aria-label` **only when visible text isn’t available**. If the element already has text, prefer that instead.
	- ```html
	  <button aria-label="Close menu">✖</button>
	  ```
-
- ## ARIA Roles