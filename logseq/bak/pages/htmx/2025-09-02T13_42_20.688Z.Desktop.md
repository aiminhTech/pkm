related:: [[HTML]], [[HATEOAS - Hypermedia as the Engine of Application State]]
homepage:: https://htmx.org/

- https://templ.guide/
-
- A small JS-lib lets us make our web pages more dynamic without writing a lot of JS. **htmx = a helper tool for HTML apps**.
- HTMX lets us:
	- Load or update parts of a page without reloading everything.
	- React to events (like clicks, form submits).
	- Do redirects smoothly.
- Best part → you write **less JavaScript**, use more **plain HTML**.
  background-color:: yellow
-
- **Cources**
	- https://frontendmasters.com/courses/htmx/
-
- ## DOM Updates
	- **`hx-target`:** Specifies **which element** on the page should be updated with the server response
	- **`hx-swap`:** Controls **how** the new content is inserted (`innerHTML`, `outerHTML`, etc.)
	- **`hx-swap-oob`:**  Allows updating elements outside the requesting element (out-of-band updates)
	- **Example**
	  background-color:: red
		- Clicking the button sends a **GET** request to `/quote`
		- The response replaces the inner HTML of the `#quotes` div
		- ```html
		  <button hx-get="/quote" hx-target="#quote" hx-swap="innerHTML">
		    Get Quote
		  </button>
		  
		  <div id="quote">Click to see a quote</div>
		  ```
	-
	- ### What is Out-of-Band (OOB)
		- In HTMX, OOB updates allow the server to update **elements outside the element that triggered the request**
		- Normally, when we click a button or submit a form with HTMX:
			- The request ist sent to the server
			  logseq.order-list-type:: number
			- The response replaces or updates a specific element (`hx-target`) that triggered the request
			  logseq.order-list-type:: number
		- With OOB, the server can target other elements on the page, even if they aren't part of the original request. This is useful for things like:
			- Notifications
			- Updating a global counter
			- Updating sidebars or headers
		- **OOB Example**
		  background-color:: red
			- Even if the request came from a different button, the `#notifications` div is updated.
			- ```html
			  <div id="notifications"></div>
			  
			  <!-- Server responds with: -->
			  <div id="notifications" hx-swap-oob="beforeend">
			    New notification!
			  </div>
			  ```
-
- ## `hx-post` - Form Submission
  id:: 68b55885-7fe9-48ce-86a7-4f0c528efa48
	- Sends form data to a server endpoint via **POST** without a full page reload
	- The server responds with HTML (partial or full), which HTMX inserts into the page automatically
	- ```html
	  <form hx-post="/contacts" hx-target="#contacts-list">
	    <input type="text" name="name" placeholder="Name">
	    <input type="email" name="email" placeholder="Email">
	    <button type="submit">Add Contact</button>
	  </form>
	  
	  <div id="contacts-list">
	    <!-- New contacts will appear here -->
	  </div>
	  ```
- ## `hx-delete` - Deleting Records
	- Sends a **DELETE** request to server endpoint
	- Can update or remove elements from the DOM after deletion
	- **Example**
	  background-color:: red
		- Clicking the button sends a DELETE request to `/contacts/1`.
		- The server confirms deletion, and HTMX removes the contact div from the page.
		- ```html
		  <button hx-delete="/contacts/1" hx-target="#contact-1" hx-swap="outerHTML">
		    Delete
		  </button>
		  
		  <div id="contact-1">John Doe</div>
		  ```
-
- ## `hx:beforeSwap` - Error Handling
	- Lets us **intercept HTMX updates** before they are apllied
	- Commonly used to handle errors or customize UI behavior for responses like HTTP 422
	- **Example**
	  background-color:: red
		- If the server returns a **422 error**, the errors div is updated instead of swapping the whole form.
		- ```html
		  <form hx-post="/contacts" 
		        hx-target="#form-errors" 
		        hx-on="htmx:beforeSwap: checkErrors(event)"
		  >
		    <input type="text" name="name" required>
		    <button type="submit">Add</button>
		  </form>
		  
		  <div id="form-errors"></div>
		  
		  <script>
		  function checkErrors(event) {
		    if(event.detail.xhr.status === 422) {
		      event.detail.shouldSwap = true; // Update errors div
		    }
		  }
		  </script>
		  
		  ```
	-
- ## `hx-push-url` - URL & Navigation
	- Updates the browser URL **without a full reload**
	- Useful for infinite scrolling or filtering, while keeping the page state in history
	- **Example**
	  background-color:: red
		- Clicking "Load More" fetches page 2 content and updates the URL to reflect the current page
		- ```html
		  <div hx-get="/page/2" hx-trigger="click" hx-target="#content" hx-push-url="true">
		    Load More
		  </div>
		  
		  <div id="content"></div>
		  ```
- ## `hx-indicator` - Indicators & Delays
	- `hx-indicator`: Shows a loading element while HTMX request is in progress
	- **Swap delays**: Delays DOM updates to make trasitions smooth
	- **Example**
	  background-color:: red
		- While the server responds, `#loading` is visible
		- Once the response arrives, HTMX hides `#loading` and updates `#data`
		- ```html
		  <div id="loading" style="display:none;">Loading...</div>
		  
		  <button hx-get="/data" hx-target="#data" hx-indicator="#loading">
		    Fetch Data
		  </button>
		  
		  <div id="data"></div>
		  ```
-