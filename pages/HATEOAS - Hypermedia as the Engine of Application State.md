tags:: [[HTMX]]

- The server tells the browser what the user can do next by sending links, buttons or forms
- **Example:**
	- You open a page -> server sends HTML with btns -> you click one -> server sends back new HTML with the next possible actions
	-
- HATEOAS means **the server drives the app by sending HTML with links/actions**. htmx makes it **easy and modern** to build apps this way.
  background-color:: blue
-
- ### How is it different  from traditional way?
	- **Traditional:** The Browser (or JS) has most of the rules. The HTML is just a shell
	- **HATEOAS way:** The server decides the rules. The HTML itself has the “next steps” built in.
-
- ### Layers of State in Web App
	- Think of a web app as having **3 layers of memory**
		- **Server state** → data on the server (e.g. your account info in a database).
		- **Client state** → data in your browser (cookies, local storage, etc.).
		- **UI state** → what you actually *see* on the screen right now (HTML).
-
-