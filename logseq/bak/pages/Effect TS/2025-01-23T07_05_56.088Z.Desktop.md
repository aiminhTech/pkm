tags:: [[TypeScript]], [[bun]] 
type:: library

- https://effect.website/
-
- ## Overview
  collapsed:: true
	- Typescript Library
	- Useful primitives
		- functional programming data promitives: `Option`, `Either`, `Chunk`, `Queue`, etc.
		- type safe error handling
	- Helps build apps that are: **reliable**, **reuseable**, **testsable**, **maintainable**, **scalable**
- ## Learning
	- **Ethan Niser**
		- https://ethanniser.dev/blog/effect-best-practices/
		- Intro: [https://www.youtube.com/watch?v=fTN8BX5qj6s](https://www.youtube.com/watch?v=fTN8BX5qj6s)
		- Workshop: [https://www.youtube.com/watch?v=Lz2J1NBnHK4](https://www.youtube.com/watch?v=Lz2J1NBnHK4)
		- Exercises for Workshop: [https://github.com/ethanniser/effect-workshop](https://github.com/ethanniser/effect-workshop)
	- **Motivation: J. Schickling**
		- [https://www.youtube.com/watch?v=PxIBWjiv3og](https://www.youtube.com/watch?v=PxIBWjiv3og)
	- **Motivation: M. Arnaldi**
		- [https://www.youtube.com/watch?v=BHuY6w9ed5o](https://www.youtube.com/watch?v=BHuY6w9ed5o)
- ## Addtional Resources
  collapsed:: true
	- [Effect API Docs](https://effect-ts.github.io/effect/)
	- [Effect Docs](https://effect.website/)
	- [Effect Source](https://github.com/Effect-TS/effect)
	- [Effect Discord](https://discord.gg/effect-ts)
- ## Installation
  collapsed:: true
	- https://effect.website/docs/getting-started/installation/
	- ### Deno
		- interactive shell: `import * as Effect from "npm:effect"`
	- ### Bun
		- `bun add effect`
- ## VS Code Snippet
  collapsed:: true
	- ```json
	  {
	    "Gen Function $": {
	      "prefix": "gg",
	      "body": ["function* (_) {\n\t$0\n}"],
	      "description": "Generator function with _ input"
	    },
	    "Gen Function $ (wrapped)": {
	      "prefix": "egg",
	      "body": ["Effect.gen(function* (_) {\n\t$0\n})"],
	      "description": "Generator function with _ input"
	    },
	    "Gen Yield $": {
	      "prefix": "yy",
	      "body": ["yield* _($0)"],
	      "description": "Yield generator calling _()"
	    },
	    "Gen Yield $ (const)": {
	      "prefix": "cyy",
	      "body": ["const $1 = yield* _($0)"],
	      "description": "Yield generator calling _()"
	    }
	  }
	  ```
- ## Packages
	- https://effect-ts.github.io/effect/
	- [[Effect Platform]]
	- **SQL**
		- [[Effect SQL Sqlite Bun]]
	- [[Effect Schema]]
-
- ## The Effect Type
  collapsed:: true
	- https://effect.website/docs/getting-started/the-effect-type/
	- Is chatgeneric over 3 paramters which describe its behavior `Success`, `Error` and `Requirements`
	- `Success`: Represent **the success type**, indicates that an effect succeeds and return a value of type `Success`
	- `Error`: Represent **the error type**, indicates that an effect fails and return an error of type `Error`
	- `Requirements`: Represent **required dependencies**, indicates that an effect may need certain contextual dependencies of type `Requirements` to execute
	- ```typescript
	  type Effect<Success, Error, Requirements> = (
	    context: Context<Requirements>
	  ) => Error | Success
	  ```
	- *However, effects are not actually functions. They can model synchronous, asynchronous, concurrent, and resourceful computations.*
	-
- ## Creatings Effects
	- https://effect.website/docs/getting-started/creating-effects/
	- ### Why not throws errors?
	  collapsed:: true
		- Throwing errors in traditional programming has limitations, such as the inability of function type signatures to indicate potential exceptions
		- **Effect** introduces alternatives to improve error handling by explicitly representing **success** and **failure** in the type system
	- ### `succeed`
		- https://effect.website/docs/getting-started/creating-effects/#succeed
		- Creates an `Effect` that always succeeds with a specific value
		- ```typescript
		  // type: Effect<number, never, never>
		  const success = Effect.succeed(42)
		  
		  // The type of success is Effect<number, never, never>, which means:
		  //	It produces a value of type number.
		  //	It does not generate any errors (never indicates no errors).
		  //	It requires no additional data or dependencies (never indicates no requirements).
		  
		  
		  ```
	- ### `fail`
	  collapsed:: true
		- https://effect.website/docs/getting-started/creating-effects/#fail
		- Creates an `Effect` that represents an error that can be recovered from
		- ```typescript
		  // type: Effect<never, Error, never>
		  const failure = Effect.fail(new Error())
		  
		  // The type of failure is Effect<never, Error, never>, which means:
		  //  It never produces a value (never indicates that no successful result will be produced).
		  //  It fails with an error, specifically an Error.
		  //  It requires no additional data or dependencies (never indicates no requirements).
		  
		  ```
	- ### `sync` - Synchronous computations
	  collapsed:: true
		- https://effect.website/docs/getting-started/creating-effects/#sync
		- Creates an `Effect` that represents a synchronous side-effectful computation.
		- Use `Effect.sync` when you are sure the operation will not fail.
		- ```typescript
		  // type: Effect<void, never, never>
		  const log = (message: string) =>
		    Effect.sync(() => {
		      console.log(message); // side effect
		    });
		  
		  // Usage
		  const program = log("Hello, World!");
		  
		  // Type of program is Effect<void, never, never>, which means:
		  //	Produces no meaningful value (void).
		  //	Cannot fail (never errors).
		  //	No external dependencies (never).
		  
		  ```
	- ### `try` - Synchronous computations that could throw
	  collapsed:: true
		- https://effect.website/docs/getting-started/creating-effects/#try
		- Creates an `Effect` that represents a synchronous computation that might fail.
		- ```typescript
		  // type: Effect<any, Error, never>
		  const program = Effect.try({
		    try: () => JSON.parse(""),
		    catch: (_caughtError) => new Error("JSON.parse trrew an error")
		  })
		  
		  // You can think of this as a similar pattern to the traditional try-catch block in JavaScript
		  ```
	- ### `promise` - Asynchronous computations
	  collapsed:: true
		- https://effect.website/docs/getting-started/creating-effects/#promise
		- Creates an `Effect` that represents an asynchronous computation guaranteed to succeed.
		- Use `Effect.promise` when you are sure the operation will not reject.
		- ```typescript
		  // type: Effect<number, never, never>
		  const promise = Effect.promise(() => Promise.resolve(42))
		  ```
	- ### `async` for async callbacks
		- https://effect.website/docs/getting-started/creating-effects/#from-a-callback
		- TODO
	- ### Cheatsheet
	  collapsed:: true
		- https://effect.website/docs/getting-started/creating-effects/#cheatsheet
		- | API | Given | Result |
		  | ---- | ---- | ---- |
		  | `succeed` | `A` | `Effect<A>` |
		  | `fail` | `E` | `Effect<never, E>` |
		  | `sync` | `() => A` | `Effect<A>` |
		  | `try` | `() => A` | `Effect<A, UnknownException>` |
		  | `try` (overload) | `() => A`, `unknown => E` | `Effect<A, E>` |
		  | `promise` | `() => Promise<A>` | `Effect<A>` |
		  | `tryPromise` | `() => Promise<A>` | `Effect<A, UnknownException>` |
		  | `tryPromise` (overload) | `() => Promise<A>`, `unknown => E` | `Effect<A, E>` |
		  | `async` | `(Effect<A, E> => void) => void` | `Effect<A, E>` |
		  | `suspend` | `() => Effect<A, E, R>` | `Effect<A, E, R>` |
- ## Running Effects
	- https://effect.website/docs/getting-started/running-effects/
	- ```typescript
	  // type: Effect<number, never, never>
	  const programm = Effect.sync(() => {
	    console.log("Hello, World!")
	    return 1
	  })
	  // Output: <blank>
	  ```
	- ### `runSync` - for synchronous effects
		- https://effect.website/docs/getting-started/running-effects/#runsync
		- Executes an effect synchronously, running it immediately and returning the result.
			- returns `A` or throws `E`
			- throws if anything async
		- ```typescript
		  const result = Effect.runSync(program)
		  // Output: Hello, World!
		  
		  console.log(result)
		  // Output: 1
		  ```
	- ### `runPromise` - for asynchronous effects
		- https://effect.website/docs/getting-started/running-effects/#runpromise
		- Executes an effect and returns the result as a `Promise`
			- return `Promise<A>` that may reject with `E`
		- Use `Effect.runPromise` when you need to execute an effect and work with the result using `Promise` syntax, typically for compatibility with other
		  promise-based code.
		- ```typescript
		  // Running a Successful Effect as a Promise
		  
		  Effect.runPromise(Effect.succeed(1)).then(console.log)
		  // Output: 1
		  ----------------------------------------------------------------------
		  
		  // Handling a Failing Effect as a Rejected Promise
		  Effect.runPromise(Effect.fail("my error")).catch(console.error)
		  
		  /* 
		  Output:
		  (FiberFailure) Error: my error
		  */
		  ```
	- `runSyncExit` / `runPromiseExit` for getting the error as a value, instead of thrown
- ## Pipelines
	- https://effect.website/docs/getting-started/building-pipelines/
	  id:: 67506653-c438-46b8-9c03-1c8afd2f9340
	- A pipeline is a sequence of operations applied to an **Effect**, where the output of one operation is passed as input to the next.
	- **Using pipelines:**
		- You can combine synchronous and asynchronous computations
		- Errors and dependencies are seamlessly propagated through the pipeline
		- Intermediate results can be transformed or handled step-by-step
	- ### `pipe`
		- https://effect.website/docs/getting-started/building-pipelines/#pipe
		- ```typescript
		  const result = pipe(input, func1, func2, ..., funcN)
		  
		  // an illustration of how pipe works
		  ┌───────┐    ┌───────┐    ┌───────┐    ┌───────┐    ┌───────┐    ┌────────┐
		  │ input │───►│ func1 │───►│ func2 │───►│  ...  │───►│ funcN │───►│ result │
		  └───────┘    └───────┘    └───────┘    └───────┘    └───────┘    └────────┘
		  ```
		- ==It’s important to note that functions passed to `pipe` must have a **single argument** because they are only called with a single argument.==
		- ```typescript
		  const increment = (x: number) => x + 1
		  const double = (x: number) => x * 2
		  const subtractTen = (x: number) => x - 10
		  
		  // Sequentially apply these operations using `pipe`
		  const result = pipe(5, increment, double, subtractTen)
		  
		  console.log(result)
		  // Output: 2
		  ```
			- In the above example, we start with an input value of `5`. The `increment` function adds `1` to the initial value, resulting in `6`. Then, the `double` function doubles the value, giving us `12`. Finally, the `subtractTen` function subtracts `10` from `12`, resulting in the final output of `2`.
			- The result is equivalent to `subtractTen(double(increment(5)))`, but using `pipe` makes the code more readable because the operations are sequenced from left to right, rather than nesting them inside out.
	- ### `map` - transform the value of an effect
		- https://effect.website/docs/getting-started/building-pipelines/#map
		- Transforms the value inside an effect by applying a function to it
		- `Effect.map` takes a function and applies it to the value contained within an effect, creating a new effect with the transformed value.
		- ```typescript
		  // type: Effect<string, never, never>
		  const mappedEffect = pipe(
		  	Effect.succeed(1),
		  	// "x" type: number
		  	Effect.map((x) => String(x))
		  )
		  
		  console.log(Effect.runSync(mappedEffect))
		  // Output: "1"
		  ```
	- ### `flatMap` - transform the value of an effect into another effect
	  collapsed:: true
		- https://effect.website/docs/getting-started/building-pipelines/#flatmap
		- Chains effects to produce new `Effect` instances, useful for combining operations that depend on previous results.
		- ```typescript
		  // type: Effect<number, Error, never>
		  const flatMappedEffect = pipe(
		  	Effect.succeed({x: 5, y: 0}),
		  	Effect.flatMap(({x, y}) => 
		  		y === 0 ? Effect.fail(new Error("divide by zero")) : Effect.succeed(x/y)
		  	)
		  )
		  ```
	- ### `tap` - perform a side effect without changing the value
	  collapsed:: true
		- https://effect.website/docs/getting-started/building-pipelines/#tap
		- Runs a side effect with the result of an effect without changing the original value
		- Use `Effect.tap` when you want to perform a side effect, like logging or tracking,without modifying the main value. This is useful when you need to observe or record an action but want the original value to be passed to the next step.
		- ```typescript
		  const logNumber = (x: number) => Effect.log(x.toString())
		  
		  const program = pipe(
		  	Effect.succeed(5),
		  	Effect.tap((x) => logNumber(x)),
		  	// x is still available!
		  	Effect.map((x) => x + 1)
		  )
		  Effect.runSync(program) // 6
		  // Output:  5
		  ```
	- ### `all` - merge multiple effects into a single effect
	  collapsed:: true
		- https://effect.website/docs/getting-started/building-pipelines/#all
		- Combines multiple effects into one, returning results based on the input structure
		- ```typescript
		  const foo = Effect.succeed(42)
		  const bar = Effect.succeed("hello")
		  
		  // type: Effect<never, never, [number, string]>
		  const combinedEffect = Effect.all([foo, bar])
		  console.log(Effect.runSync(combinedEffect))
		  // Output: [42, "hello"]
		  ```
	- ### `andThen`
		- https://effect.website/docs/getting-started/building-pipelines/#andthen
		- Chains two actions, where the second action can depend on the result of the first
		-
	- ### Recap
	  collapsed:: true
		- Apply successive transformation with `pipe`
		- Modify the value with `map`
		- Modify the value or introduce errors with `flatMaps`
		- Use the value but ignore the result with `tap`
		- Combine the value of multiple effects with `all`
- ## Generators - async/await for Effect
	- https://effect.website/docs/getting-started/using-generators/
	- Alternativ syntax similar to `async/await`, completely optional
	- ```typescript
	  declare const inAnEffect: Effect<never, Error, number>
	  
	  // type: Effect<string, Error, never>
	  const program = Effect.gen(function* (_) {
	  	// type: number
	  	const valueOfEffect = yield* _(inAnEffect)
	  	return String(valueOfEffect)
	  })
	  ```
		- 1. **`inAnEffect`:**  
		     This is a predefined effect that can potentially fail with an `Error` or succeed with a `number`.
		- 2. **`Effect.gen`:**  
		     This function lets you write asynchronous code in a synchronous style using generators. You can think of it like a guide that helps manage these effects more elegantly.
		- 3. **Generator Function `function* (_)`**:
			- The `function*` part means it's a generator function, allowing the use of `yield`.
			- `_` is just a placeholder name for a helper that lets you run effects.
		- 4. **Inside the Generator:**
			- `yield* _(inAnEffect)`: This line runs the `inAnEffect` and waits for it to finish. It produces a `number`.
			- `const valueOfEffect = ...` stores this `number`.
		- 5. **Return Value:**
			- `return String(valueOfEffect)`: Converts the number to a `string` and returns it.
- ## Error Handing
	- ### Tagged Error
	  collapsed:: true
		- A **tagged error** is simply an error that includes a special identifier (a `_tag`) that tells you what kind of error it is. Instead of just using generic error messages, you can create custom error types with their own tags.
		- ```typescript
		  type DivideByZeroError = {
		  	readonly _tag = "DivideByZeroError"
		  }
		  
		  type HttpError = {
		  	readonly _tag: "HttpError",
		  	readonly statusCode: number
		  }
		  ```
	- ### `catchAll` - catching all errors
	  collapsed:: true
		- https://effect.website/docs/error-management/expected-errors/#catchall
		- Handles all errors in an effect by providing a fallback effect.
		- ```typescript
		  // type: Effect<string, never, never>
		  const caughtAll = mayError.pipe(
		  	// "error" type: DivideByZeroError | HttpError
		  	Effect.catchAll((error) => 
		  		Effect.succeed(`Recovering from any Error (${error._tag})`)
		     )
		  )
		  ```
	- ### `catchTag` - catching specific errors
	  collapsed:: true
		- https://effect.website/docs/error-management/expected-errors/#catchtag
		- Catches and handles specific errors by their `_tag` field, which is used as a discriminator.
		- ```typescript
		  // type: Effect<string, DivideByZeroError, never>
		  const caughtTag = mayError.pipe(
		  	// "error" type: HttpError
		  	Effect.catchTag(("HttpError", (httpError) => 
		  		Effect.succeed(`Recovering from httpError with status: ${httpError.statusCode}`)
		  	) 
		  )
		  ```
	- ### `catchTags`- multiple specific errors
		- https://effect.website/docs/error-management/expected-errors/#catchtags
		- TODO
	- ### `mapError` - transform the error of an effect
		- https://effect.website/docs/error-management/error-channel-operations/#maperror
		- TODO
	- ### `match` -  handle both cases
		- https://effect.website/docs/error-management/matching/#match
		- TODO
	- ### `either` - move the errror into success channel
	- ###
	- ###
- ## Adding Requirements (for Effect<R,E,A>)
	- https://effect.website/docs/requirements-management/services/#how-it-works
	- An Effect whose R isn't never cannot be run
	- ### Context Management
		- An Effect's third type param represents the *services* it requires before it can be run
		- **Service** are functionality whos type signature is seperate from the implementation
		- `Context.Tag ` created a placehold for a service that can be used in an effect as if it were the real thing
		- `provideService(Tag, implementation)` provide the service to the effect
		- `Layer`s are programs that create services and run before effects that require them
		- `provide(Tag, layer)` provides the layer to the effect
	- ### `Context.Tag<T>`
		- Creates a placeholder that we can use in our pipelines and adds `T` to the `R` field of the Effect
		- ```typescript
		  import {Effect, Context} from "effect"
		  
		  interface Random {
		    readonly _tag: "Random"
		    readonly next: Effect.Effect<never, never, number>
		  }
		  
		  const Random = Context.Tag<Random>("@app/Random")
		  
		  // type: Effect<void, never, Random>
		  const program = pipe(
		    Random,
		    Effect.flatMap((random) => random.next),
		    Effect.flatMap(
		      (randomNumber) => Effect.log(`random number: ${randomNumber}`)
		    )
		  ) 
		  
		  ```
	- ### `Effect.provideService`
		- Fills that placeholder
		- ```typescript
		  // type: Effect<void, never, Random>
		  const runable = program.pipe(
		    Effect.provideService(
		      Random,
		      Random.of({_tag: "Random", next: Effect.sync(() => Math.random())})
		    )
		  )
		  
		  Effect.runSync(runable)
		  // Output: random number: 0.81328123
		  ```
- ## Logging
	- https://effect.website/docs/observability/logging/
	- ### `log`
		- The `Effect.log` function allows you to log a message at the default `INFO` level.
		- ```typescript
		  // type: Effect<void, never, never>
		  const program = Effect.log("Application started")
		  
		  Effect.runSync(program)
		  
		  /*
		  Output;
		  timestamp=2023-07-05T09:14:53.275Z level=INFO fiber=#0
		  message="Application stared"
		  */
		  ```
		- | Annotation | Description |
		  | ---- | ---- | ---- |
		  | `timestamp` | The timestamp when the log message was generated. |
		  | `level` | The log level at which the message is logged (e.g., `INFO`, `ERROR`). |
		  | `fiber` | The identifier of the [fiber](https://effect.website/docs/concurrency/fibers/) executing the program. |
		  | `message` | The log message content, which can include multiple strings or values. |
		  | `span` | (Optional) The duration of a span in milliseconds, providing insight into the timing of operations. |
	- ### Log Levels
		- https://effect.website/docs/observability/logging/#log-levels
-