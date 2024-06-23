tags:: [[TypeScript]]

- https://frontendmasters.com/courses/typescript-practice/ #frontentmaster
- https://www.typescript-training.com/course/making-typescript-stick
-
- ## Type challenges
	- https://github.com/type-challenges/type-challenges/tree/main?tab=readme-ov-file
	- ### Round 1
		- #### `If<C, T, F>`
		  collapsed:: true
			- Implement a type that evaluates to `T` if the type `C` is `true` or `F` if `C` is `false`
			- ```ts
			  // @errors: 2344
			  type Expect<T extends true> = T
			  type Equal<X, Y> =
			  (<T>() => T extends X ? 1 : 2) extends
			  (<T>() => T extends Y ? 1 : 2) ? true : false
			  
			  type NotEqual<X, Y> = true extends Equal<X, Y> ? false : true
			  
			  // ---cut---
			  
			  // Implement this type
			  type If<C, T, F> = C extends true ? T : F
			  
			  // Tests
			  type cases = [
			    Expect<Equal<If<true, "apple", "pear">, "apple">>,
			    Expect<Equal<If<false, "orange", 42>, 42>>
			  ]
			  ```
		- #### `LengthOfTuple<T>`
			- Implement a type that evaluates to a numeric type literal, equivalent to the length of a specified tuple type `T`
			- ```ts
			  // @errors: 2344
			  type Expect<T extends true> = T
			  type Equal<X, Y> =
			  (<T>() => T extends X ? 1 : 2) extends
			  (<T>() => T extends Y ? 1 : 2) ? true : false
			  
			  type NotEqual<X, Y> = true extends Equal<X, Y> ? false : true
			  
			  // ---cut---
			  
			  // Implement this type
			  type LengthOfTuple<T extends readonly any[]> = T['length'];
			  
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
		-