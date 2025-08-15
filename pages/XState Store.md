tags:: [[State Management in React & Next.js]]

- https://www.npmjs.com/package/@xstate/store
-
- A **state machine** or **statechart** that keeps track of our app's state and how it changes over time
- Instead of just storing data like a simple variable, XState stores:
	- The current state (`loading`, `success`, `error`)
	- The rules for moving between states (called *transition*)
	- What to do when a state changes (actions, effects)
- We can think of it like a **flowchart that lives in code**
	- We define what events can happen in each state
	- We run it and XState makes sure the app only moves between states in valid ways
-