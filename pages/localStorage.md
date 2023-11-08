tags:: [[Web Storage]]

- https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage?retiredLocale=de
  :LOGBOOK:
  CLOCK: [2023-11-07 Tue 08:59:49]
  :END:
-
- A web storage mechanism that allows web applications to store data with **no expiration date**.
- Data stored in `localStorage` persists even after the browser is closed and reopened. It remains available until explicitly removed by the web application or the user.
	- Data stored in `localStorage` **is shared across browser tabs and windows from the same origin** (i.e., the same protocol, domain, and port).
	- It has a larger storage capacity compared to cookies, typically allowing web applications to store around 5-10 MB of data.
- Is often used for persisting user preferences, caching data, or storing data that should be available across different sessions.