tags:: [[Deno]]

- https://deno.com/blog/v2.0
-
- ## New Features
	- ### Backwards Compatibility with Node.js and `npm`
		- Supports `package.json` and `node_modules`
		- Enables seamless running of existing Node applications and npm modules
		- Robust support for advanced Node features like private npm registries and Node-API native addons
	- ### New Package Management Tools
		- `deno install`: install deps quickly, with performance 15% faster than npm (cold cache) and 90% faster (hot cache)
		- `deno add` and `deno remove`: add or remove packages
		- Direct imports using `npm` specifiers, eliminating the need for `node_modules` for smaller projects
	- ### Workspace and Monorepos
		- Support for hybrid projects combining Deno and npm packages
		- Better organization for larger codebases with shared and separte deps
		- Simply use the `workspace` attribute in your `deno.json` to list the member directories
		- ```deno.json
		  {
		    "workspace": ["./add", "./subtract"]
		  }
		  ```
- ## Enhanced Tooling
	- ### Improved Built-in Tools
		- `deno fmt`: now formats HTML, CSS and YAML
		- `deno lint`: includes Node-specific rules
		- `deno test`: supports Node test frameworks
		- `deno compile`: add features like code signing and icons dor executables
	- ### JavaScript Registry (JSR)
		- A modern alternative to `npm` with native TypeScript support and auto-generated documentation
- ## Performance
	- Remains fast and efficient, ith ongoing optimizations for real-world scenarios. Although a temporary change in V8's pointer compression made Deno 2.0 slightly slower in certain benchmarks, fixes are in progress.
- ## Deno 1.x to 2.x Migration Guide
	- https://docs.deno.com/runtime/reference/migration_guide/
	-
-