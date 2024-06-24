tags:: [[TypeScript]], [[TypeScript Intermediate]], [[jQuery]]

- https://frontendmasters.com/courses/typescript-practice/ #frontentmaster
- https://www.typescript-training.com/course/making-typescript-stick
-
- ## Type challenges
	- https://github.com/type-challenges/type-challenges/tree/main?tab=readme-ov-file
	- ### Round 1 - Easy
	  id:: 6679114e-5f4a-44c5-a125-47d7ab0f97b6
	  collapsed:: true
		- #### `If<C, T, F>`
		  collapsed:: true
			- **Implement a type that evaluates to `T` if the type `C` is `true` or `F` if `C` is `false`**
			- ```ts
			  // Implement this type
			  type If<C, T, F> = C extends true ? T : F //conditional type
			  
			  // Tests
			  type cases = [
			    Expect<Equal<If<true, "apple", "pear">, "apple">>,
			    Expect<Equal<If<false, "orange", 42>, 42>>
			  ]
			  ```
		- #### `LengthOfTuple<T>`
		  collapsed:: true
			- **Implement a type that evaluates to a numeric type literal, equivalent to the length of a specified tuple type `T`**
			- ```ts
			  // Implement this type
			  type LengthOfTuple<T> = T extends readonly any[] ? T['length'] : never;
			  
			  // Tests
			  const Fruits = ["cherry", "banana"] as const
			  type cases = [
			    Expect<Equal<LengthOfTuple<[1, 2, 3]>, 3>>,
			    Expect<NotEqual<LengthOfTuple<[1, 2, 3]>, 2>>,
			    Expect<Equal<LengthOfTuple<typeof Fruits>, 2>>,
			    Expect<Equal<LengthOfTuple<[]>, 0>>
			  ]
			  ```
			- The `readonly` modifier in the type definition `T extends readonly any[]` is used to ensure that `T` can be either a regular tuple or a readonly tuple. This is important because in TS, tuples created using `as const` are treated as readonly tuples
		- #### `EndsWith<A, B>`
		  collapsed:: true
			- **Implement a type that evaluates to `true` if the type `A` ends with the type `B`, otherwise false.**
			- ```ts
			  // Implement this type
			  type EndsWith<A extends string, B extends string> = 
			  	A extends `${any}${B}` 
			  	? true 
			  	: false
			  
			  // Tests
			  type cases = [
			    Expect<Equal<EndsWith<"ice cream", "cream">, true>>,
			    Expect<Equal<EndsWith<"ice cream", "chocolate">, false>>
			  ```
			- **`A extends string`**: this means `A` must be a string
			- **`B extends string`**: this means `B` must be a string
			- **`${any}${B}`**: this represents a *template literal type*. The `${any}` part means "any string", and the `${B}` part means "the string type B"
		- #### `Concat<A, B>`
		  collapsed:: true
			- **Implement a type that concatenates two tuple types `A`, and `B`**
			- ```ts
			  // Implement this type
			  type Concat<A extends any[], B extends any[]> = [...A, ...B]
			  
			  // Tests
			  type cases = [
			    Expect<Equal<Concat<[], []>, []>>,
			    Expect<Equal<Concat<[], ["hello"]>, ["hello"]>>,
			    Expect<
			      Equal<Concat<[18, 19], [20, 21]>, [18, 19, 20, 21]>
			    >,
			    Expect<
			      Equal<
			        Concat<[42, "a", "b"], [Promise<boolean>]>,
			        [42, "a", "b", Promise<boolean>]
			      >
			    >
			  ]
			  ```
	- ### Round 2 - Medium
	  collapsed:: true
		- #### `ReturnOf<F>`
		  collapsed:: true
			- **Implement a type that emits the return type of a function type `F`**
			- **Tests**
				- ```ts
				  // Tests
				  
				  const flipCoin = () =>
				    Math.random() > 0.5 ? "heads" : "tails"
				  const rockPaperScissors = (arg: 1 | 2 | 3) => {
				    return arg === 1
				      ? ("rock" as const)
				      : arg === 2
				      ? ("paper" as const)
				      : ("scissors" as const)
				  }
				  
				  type cases = [
				    // simple 1
				    Expect<Equal<boolean, ReturnOf<() => boolean>>>,
				    // simple 2
				    Expect<Equal<123, ReturnOf<() => 123>>>,
				    Expect<
				      Equal<ComplexObject, ReturnOf<() => ComplexObject>>
				    >,
				    Expect<
				      Equal<
				        Promise<boolean>,
				        ReturnOf<() => Promise<boolean>>
				      >
				    >,
				    Expect<Equal<() => "foo", ReturnOf<() => () => "foo">>>,
				    Expect<
				      Equal<"heads" | "tails", ReturnOf<typeof flipCoin>>
				    >,
				    Expect<
				      Equal<
				        "rock" | "paper" | "scissors",
				        ReturnOf<typeof rockPaperScissors>
				      >
				    >
				  ]
				  
				  type ComplexObject = {
				    a: [12, "foo"]
				    bar: "hello"
				    prev(): number
				  }
				  ```
			- **Code**
				- ```ts
				  // Implement this type
				  type ReturnOf<F> = F extends {(...arg: any[]): infer RT} ? RT : never
				  ```
				- **Type Param** `F` is a generic type param that represents a function type
				- **`F extends {(...arg: any[]): infer RT}`**: this part check id `F` is a function
					- `(...arg: any[])`: this part indicates that the functoin can have any number of arguments and of any type
					- `infer RT`: this part means, if `F` is indeed a function, `infer RT` will capture the return type of that function and assigns it to `RT`
		- #### `Split<S, SEP>`
			- **Implement a type that splits a string literal type `S` by a delimiter `SEP`, emitting
			  a tuple type containing the string literal types for all of the “tokens”**
			- **Tests**
				- ```ts
				  // Tests
				  
				  type cases = [
				    Expect<
				      Equal<
				        Split<"Hi! How are you?", "z">,
				        ["Hi! How are you?"]
				      >
				    >,
				    Expect<
				      Equal<
				        Split<"Hi! How are you?", " ">,
				        ["Hi!", "How", "are", "you?"]
				      >
				    >,
				    Expect<
				      Equal<
				        Split<"Hi! How are you?", "">,
				        [
				          "H",
				          "i",
				          "!",
				          " ",
				          "H",
				          "o",
				          "w",
				          " ",
				          "a",
				          "r",
				          "e",
				          " ",
				          "y",
				          "o",
				          "u",
				          "?"
				        ]
				      >
				    >,
				    Expect<Equal<Split<"", "">, []>>,
				    Expect<Equal<Split<"", "z">, [""]>>,
				    Expect<Equal<Split<string, "whatever">, string[]>>
				  ]
				  ```
			- **Code**
				- ```ts
				  ```
				- LATER todo
		- #### `IsTuple<T>`
		  collapsed:: true
			- **Implement a type `IsTuple`, which takes an input type `T` and returns whether
			  `T` is tuple type.**
			- ==Notes==:
				- **`number[]`**: Can have any length (including zero).
				- **`[number]`**: Always has exactly one element.
			- ```ts
			  // Implement this type
			  type IsTuple<T> = T extends readonly any[] 
			    ? ([...T, any]['length'] extends T['length'] 
			      ? false 
			      : true)
			    : false
			  // Tests
			  type cases = [
			    Expect<Equal<IsTuple<[]>, true>>,
			    Expect<Equal<IsTuple<[number]>, true>>,
			    Expect<Equal<IsTuple<readonly [1]>, true>>,
			    Expect<Equal<IsTuple<{ length: 1 }>, false>>,
			    Expect<Equal<IsTuple<number[]>, false>>
			  ]
			  ```
			- **`T extends readonly any[]`**: checks if T is an array or a readonly array
			- **`([...T, any]['length'] extends T['length'] ? false : true)`**: this part of the type definition becomes active id `T` is indeed an array or readonly array. It tries to differentiate between a fixed-length tuple and a dynamic-length array
				- `[...T, any]['length']`
					- The spread operator creates a new type by appending `any` to the end of `T`
					- For example, if `T` is a tuple like `[number]`, spreading it with `any` results in a new tuple type `[number,any]`. If `T` is a generic array like `number[]`, spreading it with `any` results in `number[]` still being a generic array, effectively representing `number[]` with plus one possible element of `any` type
				- `[...T, any]['length'] extends T['length']`
					- If the original `T` has a dynamic length (like `number[]`), then appending an element would effectively keep the length dynamic
					- If `T` is a tuple with a fixed length, appending an element would result in a new length that is one more than the original
					- Therefore, if `T` was indeed a tuple, `[...T, any]['length']` would be `T['length'] + 1`, and the condition will return `false`, indicating it is a tuple
	- ### Round 3 - Hard
	  collapsed:: true
		- ####  `TupleToNestedObject<P, V>`
			- **Given a tuple type `T` that only contains string type, and a type `U`, build an object recursively.**
			- ```ts
			  // Implement this type
			  type TupleToNestedObject<P extends any[], V> =  P extends [infer First, ...infer Rest] 
			      ? { [K in First & string]: TupleToNestedObject<Rest, V> } 
			      : V;
			  
			  // Tests
			  
			  type cases = [
			    Expect<
			      Equal<TupleToNestedObject<["a"], string>, { a: string }>
			    >,
			    Expect<
			      Equal<
			        TupleToNestedObject<["a", "b"], number>,
			        { a: { b: number } }
			      >
			    >,
			    Expect<
			      Equal<
			        TupleToNestedObject<["a", "b", "c"], boolean>,
			        { a: { b: { c: boolean } } }
			      >
			    >,
			    Expect<Equal<TupleToNestedObject<[], boolean>, boolean>>
			  ]
			  
			  ```
			- **`P extends [infer First, ...infer Rest]`**: If the tuple `P` has at least one element (i.e., it can be split into `First` and `Rest`), proceed with creating the nested object
			- LATER todo
		- #### `IndexOf<T, U>`
			- LATER todo