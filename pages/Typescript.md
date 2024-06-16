tags:: [[JavaScript]], [[Volta]]

- ## Declaration
	- #+BEGIN_QUOTE
	  The "d.ts" file is used to provide typescript type information about an API that's written in JavaScript. The idea is that you're using something like jQuery or underscore, an existing javascript library. You want to consume those from your typescript code.
	  #+END_QUOTE
	  https://stackoverflow.com/questions/21247278/about-d-ts-in-typescript
	- https://www.typescriptlang.org/docs/handbook/module-resolution.html
- ## Learncourse
	- https://frontendmasters.com/courses/typescript-v4/
		- https://www.typescript-training.com/course/fundamentals-v4
		- https://github.com/mike-north/typescript-courses/tree/main?tab=readme-ov-file
- ## Types
  collapsed:: true
	- ### Extract a type from an array
	  id:: 6638eb09-42c1-4e4f-aada-59c13006ceb8
		- ```ts
		  type Unpacked<T> = T extends (infer U)[] ? U : T;
		  
		  type InnerCacheType = Unpacked<CacheType>; // Event | User
		  ```
- ## Ultity Types
  collapsed:: true
	- ### Partial<Type>
		- https://www.typescriptlang.org/docs/handbook/utility-types.html#partialtype