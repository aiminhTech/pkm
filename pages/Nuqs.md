tags:: [[State Management in React & Next.js]]

- https://nuqs.47ng.com/
- https://nuqs.47ng.com/
-
- A React hook library designed to make syncing state with URL query parameters easy and reliable.
- ## Key Features
	- Sync state with URL params effortlessly
	- Works like `useState` but reads and writes from the URL
	- Handles serialization and deserialization automatically
	- Keeps URL as the single source od truth for our state
-
- ## Basic Example
	- ### What happens here?
		- Typing in the input updates the URL query param `?q=...`.
		- Reloading the page keeps the input filled from the URL.
		- Sharing the URL passes the current state.
		- Back and forward navigation updates the input accordingly.
	- ```tsx
	  import { useQueryState } from 'nuqs';
	  
	  function SearchForm() {
	    // 'search' state is synced with the URL param 'q'
	    const [search, setSearch] = useQueryState('q', '');
	  
	    const handleChange = (e) => setSearch(e.target.value);
	  
	    return (
	      <input
	        type="text"
	        value={search}
	        onChange={handleChange}
	        placeholder="Search..."
	      />
	    );
	  }
	  
	  ```