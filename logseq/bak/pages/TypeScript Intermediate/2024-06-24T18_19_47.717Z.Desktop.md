tags:: [[TypeScript]]

-
- ## Learncourse
  collapsed:: true
	- https://frontendmasters.com/courses/intermediate-typescript-v2/  #frontentmaster
		- https://www.typescript-training.com/course/intermediate-v2
- ##
- ## Declaration Merging
  collapsed:: true
	- The process by which TypeScript *combines multiple declarations of the same identifier into a single entity*
	- *Allows for enhanced flexibility and the merging of various types, namespaces, functions, and interfaces.*
	- ### Identifiers
	- ### Namespaces
	- ### Classes
- ## Top & Bottom Types
  collapsed:: true
	- ### Top Types
		- A **top type** ((\top)) refers to a type that can describe any possible value allowed by the system. In TypeScript, the top types are `any` and `unknown`.
		- #### `any`
		  collapsed:: true
			- *Is the most permissive type, allowing any value and bypassing all type checks. It provides maximum flexibility but at the cost of type safety.*
			- ```ts
			  let flexible: any = 4;
			  flexible = "Download some more RAM";
			  flexible = window.document;
			  flexible = setTimeout
			  ```
			- **Advantages**: Useful in scenarios where type information is unavailable or dynamic.
			- **Disadvantages**: Loses all the benefits of TypeScript's type safety.
			- **Example**:
			  
			  ``` ts
			  let flexible: any = 14;
			  flexible.it.is.possible.to.access.any.deep.property; // No type errors
			  
			  ```
		- #### `unknown`
		  collapsed:: true
			- *Like `any`, `unknown` can hold any value. However, unlike `any`, it restricts usage until the type is narrowed down.*
				- ```ts
				  let flexible: unknown = 4;
				  flexible = "Download some more RAM";
				  flexible = window.document;
				  flexible = setTimeout;
				  ```
			- **Key Property**: Must be narrowed down via type guards before usage.
				- ```ts
				  let myUnknown: unknown = 14;
				  if (typeof myUnknown === "string") {
				    myUnknown; // TypeScript recognizes this block as string
				  } else if (typeof myUnknown === "number") {
				    myUnknown; // TypeScript recognizes this block as number
				  } else {
				    myUnknown; // Type would still be unknown
				  }
				  
				  ```
	- ### Almost Top Types
		- #### `object`
		  collapsed:: true
			- *Represents all possible non-primitive values*
			- ```ts
			  let val: object = { status: "ok" };
			  val = "foo"; // Type 'string' is not assignable to type 'object'.
			  ```
		- ### `{}`
		  collapsed:: true
			- *Represents all possible values except `null` and `undefined`*
			- ```ts
			  let val2: {} = 4;
			  val2 = "abc";
			  val2 = new Date();
			  
			  ```
	- ### Bottom Type
		- A **bottom type** ((\bot)) is a type that describes no possible values. In TypeScript, the bottom type is `never`.
		- #### `never`
		- *Used to indicate values that should never occur*
		- **Primary use case**: Exhaustive checks in conditional statemens
			- ```ts
			  class Car { drive() { console.log("vroom"); } }
			  class Truck { tow() { console.log("dragging something"); } }
			  type Vehicle = Truck | Car;
			  
			  let myVehicle: Vehicle = obtainRandomVehicle();
			  
			  if (myVehicle instanceof Truck) {
			    myVehicle.tow(); // Truck
			  } else if (myVehicle instanceof Car) {
			    myVehicle.drive(); // Car
			  } else {
			    const neverValue: never = myVehicle;
			  }
			  
			  ```
		- ### Unit Types
			- *Are types that represent a set of exactly one value*
			- **Literal types**:
				- ```ts
				  let num: 65 = 65; // Represents the set { 65 }
				  ```
			- **`null` and `undefined`**:
				- ```ts
				  let myNull: null = null;
				  let myUndefined: undefined = undefined;
				  ```
			- **`void` type (almost unit type)**:
				- ```ts
				  let myVoid: void = (function() {})(); // Invoking a void-returning IIFE
				  ```
- ## Nullish Values
  collapsed:: true
	- Although `null`, `void` and `undefined` are all used to describe “nothing” or “empty”,
	  they are independent types in TypeScript.
	- ### `null`
	  collapsed:: true
		- It means that there is a value, and that value is *nothing*
		- This *nothing* is very much a defined value, and is certainly a presence — not an absence — of information.
		- ```ts
		  const userInfo = {
		    name: "Mike",
		    email: "mike@example.com",
		    secondaryEmail: null, // user has no secondary email
		  }
		  ```
	- ### `undefined`
	  collapsed:: true
		- It means the value isn’t available (yet?)
		- `undefined` is an unambiguous indication that there *may be something different there in the future*
		- ```ts
		  interface FormInProgress {
		    createdAt: Date
		    data: FormData
		    completedAt?: Date
		  }
		  const formInProgress: FormInProgress = {
		    createdAt: new Date(),
		    data: new FormData(),
		  }
		  function submitForm() {
		    formInProgress.completedAt = new Date()
		  }
		  ```
	- ### `void`
	  collapsed:: true
		- should exclusively be *used to describe that a function’s return value should be ignored*
		-
	- ### Non-null assertion operator `(!.)`
		- Is used to cast away the possibility that a value might be `null` or `undefined`.
		- The value could still be `null` or `undefined`, this operator just tells TypeScript to ignore that possibility.
		- ```ts
		  type GroceryCart = {
		    fruits?: { name: string; qty: number }[];
		  };
		  
		  const cart: GroceryCart = {};
		  cart.fruits!.push({ name: "kumkuat", qty: 1 }); 
		  // Assertion: fruits is not undefined
		  
		  ```
	- ### Definite assignment assertion `(!:)`
	  collapsed:: true
		- Used in class properties to tell TypeScript that a property will be initialized later.
		- ```ts
		  class ThingWithAsyncSetup {
		    isSetup!: boolean;
		  
		    constructor() {
		      this.setupPromise = this.initializeSetup();
		    }
		  
		    private async initializeSetup() {
		      this.isSetup = false;
		      // async operations
		      this.isSetup = true;
		    }
		  }
		  
		  ```
	- ### Optional chaining  `(?.)`
	  collapsed:: true
		- Enables safe access to deeply nested properties.
		- *If any part of the chain is `null` or `undefined`, it returns `undefined`.*
		- ```ts
		  type ResponseData = {
		    customers?: Customer[]; //could be undefined
		  };
		  
		  function getLastPayment(data: ResponseData): number | undefined {
		    return data?.customer?.lastInvoice?.lastPayment?.amount;
		  }
		  
		  ```
	- ### Nullish coalescing  `(??)`
	  collapsed:: true
		- Ensures default values for `null` or `undefined` without the common pitfalls of logical OR (`||`), which checks for truthiness.
		- ```ts
		  type PlayerConfig = {
		    volume?: 0 | 25 | 50 | 75 | 100;
		  };
		  
		  function initializePlayer(config: PlayerConfig): void {
		    const volume = config.volume ?? 50; 
		    // Defaults to 50 if volume is null/undefined
		    // If we use "config.volume || 50", TS will make a true-false check and 
		    // ignore the value 0
		  }
		  
		  ```
-
- ## Generics Scopes and Constraints
  collapsed:: true
	- ### Generic Contrainst
		- https://www.typescriptlang.org/docs/handbook/2/generics.html#generic-constraints
		- Allow us to *write classes, methods and interfaces that can operate with any data type*
		- This means we can create a single class or method that works with different types, rather than duplicating code
		- #### Why use Constraints?
			- **Type Safety:** Ensures that the operations on the generic type are valid
			- **Access to Members:** Allows access to methods, properties or members that are defined in the constraints
		- #### Describing the constraint
			- Using the `extends`keyword.
			- ```ts
			  - function listToDict(list: HasId[]): Dict<HasId> {
			  + function listToDict<T extends HasId>(list: T[]): Dict<T> {
			  ```
			- Note that our “requirement” for our argument type (`HasId[]`) is now represented in two places:
				- `extends HasId` as the constraint on `T`
				- `list: T[]` to ensure that we still receive an array
	- ### Scopes and TypeParams
		- When working with function parameters, we know that **inner scopes**have the ability to access **outer scopes** but not vice versa:
			- ```ts
			  function receiveFruitBasket(bowl) {
			    console.log("Thanks for the fruit basket!")
			    // only `bowl` can be accessed here
			    eatApple(bowl, (apple) => {
			      // both `bowl` and `apple` can be accessed here
			    })
			  }
			  ```
		- Type params work a similar way:
			- ```ts
			  // outer function
			  function tupleCreator<T>(first: T) {
			    // inner function
			    return function finish<S>(last: S): [T, S] {
			      return [first, last]
			    }
			  }
			  const finishTuple = tupleCreator(3)
			  
			  const t1 = finishTuple(null)
			  // const t1: [number, null]
			  
			  const t2 = finishTuple([4, 8, 15, 16, 23, 42])
			  // const t2: [number, number[]]
			  ```
-
- ## Conditional Types
  collapsed:: true
	- https://www.typescriptlang.org/docs/handbook/2/conditional-types.html
	- *Provide a similar mechanism for types*
		- ```ts
		  class Grill {
		    startGas() {}
		    stopGas() {}
		  }
		  class Oven {
		    setTemperature(degrees: number) {}
		  }
		   
		  type CookingDevice<T> = T extends "grill" ? Grill : Oven;
		   
		  let device1: CookingDevice<"grill">;
		  // device1 is of type Grill
		  
		  let device2: CookingDevice<"oven">;
		  // device2 is of type Oven
		  
		  ```
	- **The conditional type has the form:**
		- ```ts
		  type TypeName<T> = T extends ConditionType ? TrueType : FalseType;
		  ```
	- **Example**
		- ```ts
		  type IsLowNumber<T> = T extends 1 | 2 ? true : false;
		  
		  type TestOne = IsLowNumber<1>; // true
		  type TestTwo = IsLowNumber<2>; // true
		  type TestTen = IsLowNumber<10>; // false
		  type TestTenWithTwo = IsLowNumber<10 | 2>; // boolean
		  
		  ```
			- **T = 1**: Evaluates to `true`
			- **T = 2**: Evaluates to `true`
			- **T = 10**: Evaluates to `false`
			- **T = 10 | 2**: Evaluates to `boolean` because the union includes a type that meets the condition and one that does not.
- ## Inference with conditional types
  collapsed:: true
	- The **`infer`** keyword offers a powerful mechanism for type manipulation. *By capturing parts of existing types, it allows you to extract or infer new type parameters*
	-
- ## Ultity Types
  collapsed:: true
	- https://www.typescriptlang.org/docs/handbook/utility-types.html
	- ### Extract and Exclude Utility Types
		- **Extract**
		  collapsed:: true
			- Extracts types from a union that are assignable to another type
			- ```ts
			  type FavoriteColors = "dark sienna" | "van dyke brown" | "yellow ochre" | "sap green" | "titanium white" | "phthalo green" | "prussian blue" | "cadium yellow" | [number, number, number] | { red: number; green: number; blue: number };
			  
			  type StringColors = Extract<FavoriteColors, string>;
			  // StringColors = "dark sienna" | "van dyke brown" | "yellow ochre" | "sap green" | "titanium white" | "phthalo green" | "prussian blue" | "cadium yellow"
			  
			  ```
		- **Exclude**
		  collapsed:: true
			- Excludes types from a union that are assignable to another type
			- ```ts
			  type NonStringColors = Exclude<FavoriteColors, string>;
			  // NonStringColors = [number, number, number] | { red: number; green: number; blue: number }
			  
			  ```
		- **Implementation of Extract and Exclude**
			- ```ts
			  type Exclude<T, U> = T extends U ? never : T;
			  type Extract<T, U> = T extends U ? T : never;
			  ```
	- ### Partial<Type>
		- https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype
		- *This utility will return a type that represents all subsets of a given type*
	- ### Record<Keys, Type>
		- https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type
	- ### Pick<Types, Keys>
		- https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys
- ## Mapped Types
- ## Key Remapping in Mapped Types
  collapsed:: true
	- *Dynamically transform keys in mapped types.*
	- ```ts
	  type Colors = "red" | "green" | "blue";
	  type ColorSelector = {
	    [K in Colors as `select${Capitalize<K>}`]: () => void;
	  }
	  
	  const cs: ColorSelector = {} as any;
	  cs.selectRed();  // Valid
	  cs.selectGreen();  // Valid
	  cs.selectBlue();  // Valid
	  
	  ```
	- In this example, the keys of `ColorSelector` are dynamically generated as `selectRed`, `selectGreen`, and `selectBlue`
	-
-
- ## Template Literal Types
	- *Create dynamic types using string literals.*
	- In this example, the `Statistics` type has optional properties `meanValue` and `medianValue`
		- ```ts
		  type Statistics = {
		    [K in `${"median" | "mean"}Value`]?: number;
		  }
		  
		  const stats: Statistics = {};
		  stats.meanValue;  // This is valid
		  stats.medianValue;  // This is valid
		  
		  ```
	-
	- **Extracting Keys with Patterns**
		- *Use patterns to extract keys with `Extract` and template literals*
		- ```ts
		  let winFns: Extract<keyof Window, `set${any}`> = "" as any;
		  
		  // winFns can be "setInterval" or "setTimeout"
		  
		  ```
		- This extracts keys from the `Window` type that start with "set"
	- **Changing Case with Utility Types**
		- *Use `Capitalize`, `Uppercase`, and `Lowercase` within template literals to modify string case.*
		- Provides utility types to change the case of string literals within template literal types
		- ```ts
		  type T1 = `send${Capitalize<"mouse" | "keyboard">}Event`;
		  // T1 is "sendMouseEvent" | "sendKeyboardEvent"
		  
		  type T2 = `send${Uppercase<"mouse" | "keyboard">}Event`;
		  // T2 is "sendMOUSEEvent" | "sendKEYBOARDEvent"
		  
		  type T3 = `send${Lowercase<"Mouse" | "keyBoard">}Event`;
		  // T3 is "sendmouseEvent" | "sendkeyboardEvent"
		  
		  ```
- ## Checked Index Access
	- *Use the `noUncheckedIndexAccess` compiler flag to enforce safe property access in index signatures*
	- When working with index signatures in TypeScript, there is a risk of accessing properties that may be `undefined`. Previously, it was advised to explicitly handle this by defining types that include `undefined`
	- ```ts
	  type Dict<T> = { [K: string]: T | undefined };
	  
	  const d: Dict<string[]> = {};
	  d.rhubarb?.join(", ");  // Safe access, using optional chaining
	  
	  ```
	- To enforce this more strictly, TypeScript introduced the `noUncheckedIndexAccess` compiler flag. When enabled, this flag makes the compiler check that index accesses are safe
	- ```ts
	  // Enable this flag in tsconfig.json
	  {
	    "compilerOptions": {
	      "noUncheckedIndexAccess": true
	    }
	  }
	  
	  type Dict<T> = { [K: string]: T };
	  
	  const d: Dict<string[]> = {};
	  d.rhubarb.join(", ");  // Error: 'd.rhubarb' is possibly 'undefined'.
	  
	  ```
	- With `noUncheckedIndexAccess` enabled, you are alerted if there is a possibility of accessing an `undefined` property