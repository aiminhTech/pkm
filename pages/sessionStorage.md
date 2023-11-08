tags:: [[Web Storage]], [[localStorage]]

- https://developer.mozilla.org/en-US/docs/Web/API/Window/sessionStorage?retiredLocale=de
-
- `sessionStorage` is another web storage mechanism that allows web applications to store data, but it **has a shorter lifespan**.
	- Data stored in `sessionStorage` is available only for the duration of a page session. When the user closes the browser tab or the session ends, the data is automatically cleared.
	- Like `localStorage`, data stored in `sessionStorage` is accessible across the pages from the same origin.
	- It has a similar storage capacity as `localStorage, typically allowing web applications to store around 5-10 MB of data.
- Is often used for temporarily storing data needed within a single browsing session, such as data for multi-step forms or navigation history within a web application