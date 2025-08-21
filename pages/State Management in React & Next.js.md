parent:: [[State Management at Scale]]

- https://frontendmasters.com/courses/react-nextjs-state/
-
- ## React State Anti-patterns
  collapsed:: true
	- It means **common mistakes or bad habits when using React state**  which often lead to problems in our app
	- **State**: the data the components keep track of and use to render the UI
	- **Anti-pattern**: a way of doing somthing that looks okay at first but causes bugs
	- ### Deriving State
		- Means calculating some info based on other data we already have instead of storing that info seperately in state. Instead of keeping extra state for something that **can be calculated from props or other state**, we can compute it inside the render func or in a helper
		- ==**RULES**==:
			- **Don’t store data you can calculate** (derive) from existing state or props
			- Avoid syncing derived data with `useState` + `useEffect`
			- Instead, calculate derived values directly during render or with `useMemo` if expensive
		- **Benefits**: fewer bugs, simpler state, always in sync
		- **Example**: calculate total cost from items directly instead of storing it
			- ```tsx
			  // Before
			  function TripSummary() {
			    const [tripItems] = useState([
			      { name: 'Flight', cost: 500 },
			      { name: 'Hotel', cost: 300 },
			    ]);
			    const [totalCost, setTotalCost] = useState(0); // ❌ Unnecessary state
			  
			    useEffect(() => {
			      setTotalCost(tripItems.reduce((sum, item) => sum + item.cost, 0)); // ❌ Sync effect
			    }, [tripItems]);
			  
			    return <div>Total: ${totalCost}</div>;
			  }
			  
			  ----------------------------------------------------------------------------------------------
			  // After 
			  function TripSummary() {
			    const [tripItems] = useState([
			      { name: 'Flight', cost: 500 },
			      { name: 'Hotel', cost: 300 },
			    ]);
			  
			    // ✅ Derive the value directly
			    const totalCost = tripItems.reduce((sum, item) => sum + item.cost, 0);
			  
			    return <div>Total: ${totalCost}</div>;
			  }
			  ```
	- ### Refs vs State
		- ==**RULES:**==
			- Use `useRef` for values that dont impact rendering (timers, DOM nodes)
			- Avoid using `useState` for mutable values that dont need to trigger re-renders
			- `useRef` updates dont cause re-renders, unlike `useState`
			- **Example:** store timer IDs in `useRef` instead of state
			- ```tsx
			  // Before
			  function Timer() {
			    const [timeLeft, setTimeLeft] = useState(60);
			    const [timerId, setTimerId] = useState<NodeJS.Timeout | null>(null); // ❌ Causes re-renders
			  
			    const startTimer = () => {
			      const id = setInterval(() => {
			        setTimeLeft((prev) => prev - 1);
			      }, 1000);
			      setTimerId(id); // ❌ Triggers unnecessary re-render
			    };
			  
			    useEffect(() => {
			      return () => timerId && clearInterval(timerId);
			    }, [timerId]); // ❌ Effect runs every time timerId changes
			  
			    return <div>{timeLeft}s remaining</div>;
			  }
			  
			  ----------------------------------------------------------------------------------------------
			  // After
			  function Timer() {
			    const [timeLeft, setTimeLeft] = useState(60);
			    const timerIdRef = useRef<NodeJS.Timeout | null>(null); // ✅ No re-renders
			  
			    const startTimer = () => {
			      const id = setInterval(() => {
			        setTimeLeft((prev) => prev - 1);
			      }, 1000);
			      timerIdRef.current = id; // ✅ No re-render triggered
			    };
			  
			    useEffect(() => {
			      return () => timerIdRef.current && clearInterval(timerIdRef.current);
			    }, []); // ✅ Effect runs only once
			  
			    return <div>{timeLeft}s remaining</div>;
			  ```
	- ### Redundant State
		- ==**RULES**==
			- Store each piece of data only once
			- Avoid duplicating data across multiple states
			- Store minimal info (IDs instead od whole objects) and derive the rest
			- Prevent bugs from out-of-sync data and complex updates
			- **Example**: store selected item’s ID, then find the full object when needed.
			- ```tsx
			  // Before
			  function HotelSelection() {
			    const [hotels] = useState([
			      { id: 'h1', name: 'Grand Hotel', price: 200 },
			      { id: 'h2', name: 'Budget Inn', price: 80 },
			    ]);
			    const [selectedHotel, setSelectedHotel] = useState<Hotel | null>(null); // ❌ Stores entire object
			  
			    const handleSelect = (hotel: Hotel) => {
			      setSelectedHotel(hotel); // ❌ Duplicates data from hotels array
			    };
			  
			    return (
			      <div>
			        {selectedHotel && (
			          <div>
			            {selectedHotel.name} - ${selectedHotel.price}
			          </div>
			        )}
			      </div>
			    );
			  }
			  
			  // After
			  function HotelSelection() {
			    const [hotels] = useState([
			      { id: 'h1', name: 'Grand Hotel', price: 200 },
			      { id: 'h2', name: 'Budget Inn', price: 80 },
			    ]);
			    const [selectedHotelId, setSelectedHotelId] = useState<string | null>(null); // ✅ Store only ID
			  
			    const handleSelect = (hotelId: string) => {
			      setSelectedHotelId(hotelId); // ✅ Store minimal data
			    };
			  
			    // ✅ Derive the full object when needed
			    const selectedHotel = hotels.find((h) => h.id === selectedHotelId);
			  
			    return (
			      <div>
			        {selectedHotel && (
			          <div>
			            {selectedHotel.name} - ${selectedHotel.price}
			          </div>
			        )}
			      </div>
			    );
			  }
			  ```
- ## AI State Modeling
  collapsed:: true
	- Modeling is a way to map out the incidental complexity, so that there are no suprises when we start building. Goal is to separate the incidental complexity from the accidental complexity.
	- ### Complexity
		- #### Incidental Complexity
			- Complexity that aries not from the inherent nature of te problem, but from the **tools**, **environment** or **processes** we use to solve it (**==unavoidable==**)
			- It is caused by the **implementation approach**, **development environment** or **technology choices** not by the problem itself
			- **Example:**
				- Using a poorly designed framework that requires a lot of boilerplate code
				- Complex build and deployment systems
				- Unnecessary overhead in configuration or integration
			- ==**GOAL**: Reduce incidental complexity by choosing better tools, frameworks, libraries or simplifying processes==
		- #### Accidental Complexity
			- The complexity that comes from the way we implement the solution (**==avoidable, self-inflicted==**)
			- **Example:**
				- Writing a lot of glue code to make components interact
				- Managing low-level infrastructure details manually rather than using managed services
			- ==**GOAL**: Minimize accidental complexity to focus more on the essential problem-solving part==
	- ### Essential Modeling Diagrams #[[Modeling Diagram]]
		- **Entity Relationship Diagram**: What data does our applicationmanage?
		- **Sequence Diagram**: How do different parts of our system interact?
		- **State Diagram**: What are the possible states and transitions in our application?
		- **Benefits**:
			- Clearer understanding of system relationships and boundaries
			- Easier onboarding for new team members
			- Better communication with stakeholders
			- Reduced bugs through upfront thinking
			- Faster development once you understand the problem
- ## State Optimization
  collapsed:: true
	- ### Best Practices
		- **Events are the truth** → Record what happened, don’t just change the state.
		- **Pure & immutable** → Update state with clean functions and never change it directly.
		- **Framework-free logic** → Keep state logic separate so it works anywhere.
		- **State machines** → Only allow valid states and valid transitions.
		- **Declarative effects** → Describe side effects (like API calls) separately from your state logic.
	- ### Finite State
		- Means our system or component can only be in **one of a limited set of allowed states** at any time, no more - no less
		- We define:
			- All valid states (the finite set)
			- Allowed transitions between those states
		- **Example:** Flight Booking Status
			- **Possible states:**
				- `idle` → nothing is happening yet
				- `loading` → fetching flight data
				- `success` → data loaded successfully
				- `error` → failed to load data
			- **Transitions:**
				- `idle` → (`FETCH`) → `loading`
				- `loading` → (`RESOLVE`) → `success`
				- `loading` → (`REJECT`) → `error`
				- `error` → (`RETRY`) → `loading`
			- ```tsx
			  // ❌ Boolean flags can create impossible states
			  const [isLoading, setIsLoading] = useState(false);
			  const [error, setError] = useState(null);
			  const [data, setData] = useState(null);
			  
			  // ✅ Type states prevent impossible combinations
			  type State =
			    | { status: 'idle' }
			    | { status: 'loading' }
			    | { status: 'error'; error: string }
			    | { status: 'success'; data: FlightData };
			  
			  const [state, setState] = useState<State>({ status: 'idle' });
			  ```
- ## Managing FormData & Complex State
  collapsed:: true
	- Use `FormData` + server actions instead of multiple useState hooks for form handling. This reduces boilerplate, improve safety, supports progressive enhancement, and works with file uploads.
	- ### FormData Instead of Multiple useState
		- Use `FormData` and server actions instead of managing multiple `useState` hooks. Let `FormData` automatically capture form values and use server actions for processing
		- **==Benefits==**: automatic data collection, fewer handlers, web standard, file support
		- **Example**:
			- ```jsx
			  // Before (anti-pattern)
			  // This becomes unwieldy with larger forms and requires careful state synchronization.
			  const [firstName, setFirstName] = useState('');
			  const [lastName, setLastName] = useState('');
			  // ...more state + handlers
			  
			  // Multiple handlers
			  const handleFirstNameChange = (e) => setFirstName(e.target.value);
			  const handleLastNameChange = (e) => setLastName(e.target.value);
			  
			  ----------------------------------------------------------------------------------------------
			  // After (best practice)
			  function handleSubmit(formData) {
			    const firstName = formData.get('firstName');
			    const lastName = formData.get('lastName');
			    // All form data captured automatically
			  }
			  ```
	- ### Server Actions in Next.js
		- Instead of creating seperate API routes, call server functions directly
		- **==Benefits==:** type safety, no extra API routes, works without JS.
		- ```jsx
		  // actions.ts
		  'use server';
		  export async function submitForm(formData) {
		    const name = formData.get('name');
		    // validate, save, etc.
		  }
		  
		  // Component
		  <form action={submitForm}>
		    <input name="name" />
		    <button>Submit</button>
		  </form>
		  ```
	- ### `useActionState` for UI State
		- Manages pending/loading state + server response automatically
		- **==Benefits==:** automatic pending state, error handling, UI revalidation
		- ```jsx
		  const [state, submitAction, isPending] = useActionState(serverAction, initialState);
		  
		  <form action={submitAction}>
		    {isPending && <p>Loading...</p>}
		  </form>
		  ```
	- ### When to Use FormData vs useState
		- **### Use FormData when:**
			- Building traditional forms with submit buttons
			- Working with server actions/mutations
			- Need progressive enhancement
			- Forms have many fields
			- File uploads are involved
			- Working with Next.js app router
		- **### Use useState when:**
			- Building real-time/interactive UIs
			- Need immediate validation on every keystroke
			- Complex client-side logic between fields
			- Building search/filter interfaces
			- Need granular control over individual field updates
			- Working with controlled components that need precise state
	- ### `useReducer` for Complex State Logic
		- #### React Context for Shared State
			- Avoid **prop drilling** - use **Context Providers**  for state needed across components
			- **==Benefits==**: Eliminates prop drilling, centralizes logic, cleaner components.
			- ```jsx
			  // Before (anti-pattern):
			  <App bookingState={state} setBookingState={setState} />
			  ----------------------------------------------------------------------------------------------
			  
			  // After (best practice):
			  const BookingContext = createContext();
			  function BookingProvider({ children }) {
			    const [state, dispatch] = useReducer(bookingReducer, initialState);
			    return (
			      <BookingContext.Provider value={{ state, dispatch }}>
			        {children}
			      </BookingContext.Provider>
			    );
			  }
			  function FlightForm() {
			    const { state, dispatch } = useBooking();
			  }
			  
			  ```
		- #### Custom Context Hooks
			- Use `useReducer` for complex state logic with clear actions and transitions
			- **==Benefits==**: prevents misuse, adds derived state, keeps components clean
			- ```jsx
			  function useBooking() {
			    const context = use(BookingContext);
			    if (!context) throw new Error('useBooking must be used within BookingProvider');
			    return context;
			  }
			  ```
			-
- ## External State Management Libraries
  collapsed:: true
	- Use an external state library when oujr app is **large, complex**, or needs **predictable, testable and scalable state**
	- **==Benefits==**:
		- Single source of truth (means that **there’s only one place in your application where a particular piece of data “lives”**, and every part of your app that needs it reads from — and updates — that same place.)
		- Better performance
		- Dev tools for debugging
		- Works across frameworks
		- Middleware & persistence built-in
	- ### Popular Libraries
		- **Zustand** – minimal, simple store API #Zustand
		- **Jotai** – atomic, composable #Jotai
		- **Redux Toolkit** – opinionated, robust dev tools #[[Redux Toolkit]]
		- **XState Store** – state machines for predictable flows #[[XState Store]]
	- ### Problems at Scale with React’s Built-ins
		- Prop Drilling
		  logseq.order-list-type:: number
			- ```tsx
			  // ❌ Passing state through many layers
			  function App() {
			    const [user, setUser] = useState(null);
			    return <Header user={user} />;
			  }
			  function Header({ user }) { /* ... */ }
			  
			  ```
		- ** State Sync Issues** — duplicated or stale data in multiple components.
		  logseq.order-list-type:: number
			- ```tsx
			  // ❌ Any update triggers re-render for ALL consumers
			  const AppContext = createContext({ user: null, cart: [] });
			  ```
		- Context Perf Problems
		  logseq.order-list-type:: number
		- ** Scattered Business Logic** — hard to test, no single source of truth.
		  logseq.order-list-type:: number
	- ### Stores vs. Atoms
		- **Store-based** (Zustand, Redux Toolkit, XState Store)
			- Centralized state, predictable updates
			- Best for complex relationships, team projects
			- ```tsx
			  const useBookingStore = create<BookingStore>(...);
			  
			  ```
		- **Atomic** (Jotai, Recoil)
			- Independent pieces of state, fine-grained control
			- Best for UI-specific or independent data
			- **Hybrid** → store for core logic, atoms for UI state.
			- ```tsx
			  const themeAtom = atom<'light' | 'dark'>('light');
			  ```
- ## Data Normalization
  collapsed:: true
	- Normalize data by flattening nested structures into seperate collections linked by IDs, avoiding deeply nested objects
	- ### Problems with Deeply Nested Data
		- **Example:** complex nested update when deleting a todo inside a destination
			- ```ts
			  destinations: state.destinations.map(dest =>
			    dest.id === action.destinationId
			      ? { ...dest, todos: dest.todos.filter(todo => todo.id !== action.todoId) }
			      : dest
			  );
			  ```
	- ### Benefits of Normalization
		- Store entities separately, e.g., `destinations` and `todos` as distinct collections keyed by ID
		- Use ID references to link entities
		- ```stylus
		  case 'DELETE_TODO':
		    return {
		      ...state,
		      todos: state.todos.filter(todo => todo.id !== action.todoId)
		    };
		  ```
- ## Event-Driven
  collapsed:: true
	- ### Avoiding Cascading Effects
		- The core idea is to tocus on why data changes (events) instead of when data changes (reactive updates). Avoid multiple cascading `useEffect` hooks that trigger one another, causing complexity, race conditions and debugging nightmares
		- #### Problems
			- Example of multiple cascading `useEffect`s:
			- ```tsx
			  // Effect 1: Trigger flight search when inputs change
			  useEffect(() => {
			    if (destination && startDate && endDate) setIsSearchingFlights(true);
			  }, [destination, startDate, endDate]);
			  
			  // Effect 2: Perform flight search
			  useEffect(() => {
			    if (!isSearchingFlights) return;
			    // flight search logic
			  }, [isSearchingFlights]);
			  
			  // Effect 3: Trigger hotel search after flight selected
			  useEffect(() => {
			    if (selectedFlight) setIsSearchingHotels(true);
			  }, [selectedFlight]);
			  
			  // Effect 4: Perform hotel search
			  useEffect(() => {
			    if (!isSearchingHotels) return;
			    // hotel search logic
			  }, [isSearchingHotels]);
			  
			  ```
			- **Issues**:
				- Logic flow is scattered and hard to follow
				- Race conditions & timing issues from async state updates
				- Debugging is difficult with unclear effect triggers
				- Cause multiple unnecessary re-renders and performance hits
	- ### Event-Driven Approach (Recommended)
		- Use a `useReducer` to **manage state transitions expliyitly via events, combined with a single `useEffect` for side effects**
		- **Example:**
			- ```tsx
			  type Action =
			    | { type: 'SET_INPUT'; inputs: Partial<SearchInputs> }
			    | { type: 'flightUpdated'; flight: Flight }
			    | { type: 'hotelUpdated'; hotel: Hotel }
			    | { type: 'SET_ERROR'; error: string };
			  
			  function reducer(state: BookingState, action: Action): BookingState {
			    switch (action.type) {
			      case 'SET_INPUT':
			        const inputs = { ...state.inputs, ...action.inputs };
			        return {
			          ...state,
			          inputs,
			          status: allInputsValid(inputs) ? 'searchingFlights' : state.status,
			        };
			      case 'flightUpdated':
			        return {
			          ...state,
			          status: 'searchingHotels',
			          selectedFlight: action.flight,
			        };
			      // other cases...
			    }
			  }
			  
			  useEffect(() => {
			    if (state.status === 'searchingFlights') {
			      searchFlights().then(flight => dispatch({ type: 'flightUpdated', flight }));
			    }
			    if (state.status === 'searchingHotels') {
			      searchHotels().then(hotel => dispatch({ type: 'hotelUpdated', hotel }));
			    }
			  }, [state.status]);
			  ```
		- **==Benefits==**
			- **Single source of truth:** all state lives in one reducer
			- **Predictable state transitions:** explicit action handling
			- **Simpler testing:** pure reducer functions
			- **Clear debugging:** concise action logs in React DevTools
			- **No race conditions:** synchronous state updates inside reducer
			- **Minimal effects:** only one effect handles async side-effects
	- ### Key Takeaways
		- Replace multiple cascading effects with a single reducer + effect
		- Model user/business actions as explicit events (actions)
		- Keep effects focused on external side effects, not state logic
		- Achieve predictable, maintainable, and performant UI state management
-
- ## Advanced Techniques
  collapsed:: true
	- ### State Management with URL Params
		- Simplifying URL State Sync: [[Nuqs]]
		- #### Why?
			- Users wont lose their inputs if they reload the page
			- Shareable URLs keep the same state for others who open the link
			- Back and forward buttons restore previous state seamlessly
			- Avoids frustating loss of data and keeps the Ui consistent
		- #### Challenges
			- Manually syncing React state with the URL can lead to:
				- Inconsistent state if updates are out of sync
				- Complex code to parse and update URL params
				- Risks of overwriting unrelated params
	- ### Use [[TanStack Query]]
		- TanStack Query keeps it fresh automatically
		- Handles fetching, caching, loading/error states, retries for you
		- Refetch on window focus, network reconnect, or intervals
		- Reuses data, updates in background (stale-while-revalidate)
		- POST/PUT/DELETE with automatic cache invalidation
	- ### Syning with External Store
		- React’s built-in way to subscribe to **external data sources** (Redux, Zustand, browser APIs, WebSockets, etc.).
		- Replaces the `useEffect` + `useState` dance.
		- Ensures **atomic updates** and **hydration safety** for SSR/CSR.
		- Optimized subscription management → fewer re-renders.
		- #### When to Use
			- Third-party or custom stores
			- Browser APIs (network, window size, geolocation)
			- Real-time data (WebSockets, SSE)
			- Global state outside React
		- **Example**
			- ```tsx
			  // Before (Anti-pattern)
			  // ❌ Problems: race conditions, hydration mismatches, extra renders, verbose cleanup.
			  useEffect(() => {
			    const on = () => setOnline(true);
			    const off = () => setOnline(false);
			    window.addEventListener('online', on);
			    window.addEventListener('offline', off);
			    setOnline(navigator.onLine);
			    return () => {
			      window.removeEventListener('online', on);
			      window.removeEventListener('offline', off);
			    };
			  }, []);
			  
			  ----------------------------------------------------------------------------------------------
			  // After (Best practice)
			  // ✅ Benefits: atomic updates, SSR-safe, cleaner, minimal re-renders.
			  const isOnline = useSyncExternalStore(
			    (cb) => {
			      window.addEventListener('online', cb);
			      window.addEventListener('offline', cb);
			      return () => {
			        window.removeEventListener('online', cb);
			        window.removeEventListener('offline', cb);
			      };
			    },
			    () => navigator.onLine, // client snapshot
			    () => true              // server snapshot
			  );
			  
			  ```