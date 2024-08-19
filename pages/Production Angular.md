tags:: [[Angular]], [[Managing Complexity]], [[Nx Workspace]]

- https://frontendmasters.com/courses/production-angular/ #frontentmaster
- https://github.com/onehungrymind/fem-production-angular
-
- ## Managing Complexity
  collapsed:: true
	- Complexity consists of **managing of state**, **flow control** and **code volume**
	- It is the hardest part of software development. As applications grow, so does their complexity, often exponentially
	- **Kent Beck's Statement**:
	  collapsed:: true
		- Make it work
		- Make it know
		- Make it right
		- Make it fast
	- ***General rules***
	  collapsed:: true
		- **Single Responsibility:** Code should be fine grained meaning code should only do one thing. For example, functions should do one thing only. Refactor if you're doing more than one thing in a function.
		- **Self-documenting Code:** Code should be clear and easy to understand without extensive comments.
		- **Pure, Immutable Functions**: Favor functions that don’t alter state to reduce complexity.
		- **Abstractions**: They should reduce complexity and increase cohesion by logically grouping related functionality.
		- **Composition Over Inheritance**: Favor composition for code reuse and flexibility.
	- ***Team and Tactical Rules***
	  collapsed:: true
		- **Optimize for Team**: Be mindful of your entire team's skills and optimize around those.
		- **Consistency Over Righteousness**: Consistent coding practices within the team are more important than individual preferences.
		- **Follow Style Guides**: Adhere to established style guides, modifying them only when necessary.
	- ***Code Practices***
	  collapsed:: true
		- **Eliminate Hidden State**: Avoid state within functions that can lead to inconsistent results
		- **Avoid Nested Logic**: It’s hard to reason about and test
		- **Extract Methods**: Simplify complex functions by extracting methods and moving hidden state into parameters
		- **Code Comments**: If you have to clarify your code with comments, it’s likely too complex
		- **Good Tests for Good Code**: It’s impossible to write good tests for bad code
	- ### In Angular
		- ***Components***
		  collapsed:: true
			- **A component should only ever do two things**
			  collapsed:: true
				- Consume just enough data to satisfy its templates
				- Capture user events and delegate them upwards
			- **Should be**
			  collapsed:: true
				- as thin as possible
				- oblivious to business logic
				- oblivious to server communication
				  id:: 667aa3d7-19f2-4c65-835d-b76895175cb3
				- oblivious  to appication state
		- ***Server communication and state management should be decoupled***
		- ***Data models should be decoupled especially inside of a monorepo with client and API projects***
-
- ## Nx Workspace
	- {{embed [[Nx Workspace]]}}
-
- ## Testing
	- Writing good tests for bad code is nearly impossible
	- Focus on writing high-quality, low-complexity code to make testing easier. Use small, single-purpose functions
	- ### Environment Setup for Testing
		- #### Using TestBed
		  collapsed:: true
			- Create a controlled environment to instantiate and test your component without initializing the entire application
		- #### Configuration Steps
			- **Configure Testing Module**:
				- Use `TestBed.configureTestingModule` to set up module declarations and imports
				- Replace real modules with testing equivalents (e.g., `HttpClientTestingModule` instead of `HttpClientModule`)
				- ```ts
				  TestBed.configureTestingModule({
				      declarations: [WidgetComponent, ChildComponent1, ChildComponent2],
				      imports: [
				          HttpClientTestingModule,
				          RouterTestingModule,
				          NoopAnimationsModule  // Replaces Angular Material Animations
				      ],
				      providers: [MyService]
				  }).compileComponents();
				  
				  ```
			- **Create Component Fixture**
				- Instantiate the component within the test environment using `TestBed.createComponent`
				- ```ts
				  const fixture = TestBed.createComponent(WidgetComponent);
				  fixture.detectChanges();  // Run initial data binding
				  ```
			- **Access Component Instance**:
				- Get an instance of the component to test its properties and methods
				- ```ts
				  const componentInstance = fixture.componentInstance;
				  ```
			- **Debug Element**:
				- Access the component's template for testing DOM elements
				- ```ts
				  const debugElement = fixture.debugElement;
				  ```