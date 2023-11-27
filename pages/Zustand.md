tags:: [[Typescript]], [[Javascript]], [[Web Storage]], [[LRN-205: Technology Repition]]

- https://docs.pmnd.rs/zustand/getting-started/introduction
- A small, fast, and scalable bearbones state management solution.
- Zustand has a comfy API based on hooks. It isn't boilerplatey or opinionated,
  but has enough convention to be explicit and flux-like.
-
- ## Installation
	- `npm install zustand`
	- `yarn add zustand`
- ## persisting store data
	- https://docs.pmnd.rs/zustand/integrations/persisting-store-data
	- The Persist middleware enables you to store your Zustand state in a storage
	  (e.g., [[localStorage]], [[AsyncStorage]], [[IndexedDB]], etc.), thus persisting its data.
	- `store.ts`
		- ```typescript
		  export interface State {
		    addresses: Address[];
		  }
		  
		  export interface Actions {
		    add: (data: Address) => void;
		    delete: (id: Id) => void;
		  }
		  
		  const initializer: StateCreator<State & Actions, [], []> = (set, get) => ({
		    addresses: [],
		    add: (address: Address) =>
		      set({ addresses: addAddress(get().addresses, address) }),
		    delete: (id: Id) => {
		      set({ addresses: removeAddress(get().addresses, id) });
		    },
		  });
		  
		  export const useStore = create(
		    persist(initializer, {
		      name: "address-storage",
		    }),
		  );
		  ```
		- **initializer Function**:
			- This function is used to initialize the state and actions. It's of type `StateCreator<State & Actions, [], []`, which means it's responsible for creating and managing the state, and it has access to `set` and `get` functions.
			- `set` is used to update the state.
			- `get` is used to retrieve the current state.
		- **useStore**:
			- An instance of a Zustand store created with the `create` function.
			- The `persist` function is applied to the `initializer` to enable data persistence.
			- Data persistence is a way to store the state's data, so it can be retrieved even after the application is closed and reopened.
- ## how to use in the aplication?
	- ```typescript
	  const data = useStore((state) => state.addresses);
	  const addData = useStore((state) => state.add);
	  const deleteData = useStore((state) => state.delete);
	  ```
	-