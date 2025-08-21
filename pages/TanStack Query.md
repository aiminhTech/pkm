tags:: [[State Management at Scale]]

- https://tanstack.com/query/latest
-
- TanStack Query (formerly known as React Query) is a powerful library for managing **server state** in your React (and other) applications.
- It helps you fetch, cache, synchronize, and update data from APIs easily — without the need to write lots of boilerplate code for loading states, errors, caching, or refetching.
-
- ## Key Features
	- **Server State Management**: Fetch and cache data from backend APIs efficiently
	- **Automatic Caching**: Data is cached and automatically kept fresh with background updates
	- **Refetching**: Can automatically refetch data on window focus, network reconnect or after a set of time
	- **Built-in Support:** Handles pagination, infinite scroll, mutations (POST/PUT/DELETE), and more out of the box.
	- **DevTools:** Comes with great debugging tools to visualize your queries and cache
-
- ## Why Use?
	- No need to manually track loading, errors or cache updates
	- Efficient caching and avoiding unnecessary requests
	- Debugging tools and automatic updates
	- Also supports [[React Native]] , [[Vue]], [[Angular]], and more.
-
- ## Core Concepts
	- **Query:** A request for data, e.g., `useQuery(['todos'], fetchTodos)` fetches a list of todos.
	- **Mutation:** An operation that changes data (like POST or DELETE).
	- **QueryClient:** The central manager that handles queries and caching.
	- **Query Keys:** Unique keys (often arrays) that identify queries for caching and updating.
	- **Basic Example** (in React):
		- ```jsx
		  import { useQuery, QueryClient, QueryClientProvider } from '@tanstack/react-query';
		  
		  const queryClient = new QueryClient();
		  
		  function Todos() {
		    const { data, error, isLoading } = useQuery(['todos'], () =>
		      fetch('/api/todos').then(res => res.json())
		    );
		  
		    if (isLoading) return 'Loading...';
		    if (error) return 'Error!';
		  
		    return (
		      <ul>
		        {data.map(todo => (
		          <li key={todo.id}>{todo.title}</li>
		        ))}
		      </ul>
		    );
		  }
		  
		  export default function App() {
		    return (
		      <QueryClientProvider client={queryClient}>
		        <Todos />
		      </QueryClientProvider>
		    );
		  }
		  
		  ```