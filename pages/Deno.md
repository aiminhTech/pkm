tags:: [[JavaScript]], [[TypeScript]], [[Deno Web APIs]], [[JSR]], [[Deno 2.0]]

- https://deno.com/
- A runtime for [[JavaScript]] and [[TypeScript]]
- [[Deno Deploy]]
-
- ## Standard Library
	- https://deno.land/std@0.224.0
	  collapsed:: true
		- The Standard Library has been moved to [JSR](https://jsr.io/@std). See [the blog post](https://deno.com/blog/std-on-jsr) for details.
	- https://docs.deno.com/runtime/manual/basics/standard_library
- ## Quick Start
	- ```bash
	  deno init
	  ```
- ## Safe `deno.json`
	- ```deno.json
	    "compilerOptions": {
	      "noImplicitThis": true,
	      "noImplicitReturns": true,
	      "noImplicitOverride": true,
	      "noUncheckedIndexedAccess": true,
	      "useUnknownInCatchVariables": true,
	      "allowUnreachableCode": false,
	      "noUnusedLocals": true,
	      "noUnusedParameters": true
	    }
	  ```
-
- ## Runtime flags
	- ### Permission flags
		- https://docs.deno.com/runtime/fundamentals/security/
		- Permisson flags in Deno are an integral part of security model, allowing us to explicitly control what actions our scripts are permitted to perform. By default, Deno scripts run in a sandboxed environment with no permissions, making them secure by default.
		- Necessary permissions can be granted explicitly using various flags
			- #### `--allow-read`
				- Grants read accecss to the file system.
				-
	- ### `--v8-flags`