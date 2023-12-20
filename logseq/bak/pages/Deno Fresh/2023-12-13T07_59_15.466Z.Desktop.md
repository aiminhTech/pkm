tags:: Javascript, Typescript

- https://fresh.deno.dev
- A full stack modern web framework for [[JavaScript]] and [[TypeScript]] developers, designed to make it trivial to create high-quality, performant, and personalized web applications
- # Create a project
  collapsed:: true
	- https://fresh.deno.dev/docs/getting-started/create-a-project
	- ```terminal
	  deno run -A -r https://fresh.deno.dev
	  cd fresh-project
	  deno task start
	  ```
- # Updating
  collapsed:: true
	- https://fresh.deno.dev/docs/concepts/updating
	- ``` terminal  
	  deno run -A -r https://fresh.deno.dev/update .
	  ```
	- ## Migrating existing projects with Plugins
		- https://fresh.deno.dev/docs/concepts/ahead-of-time-builds
		- `fresh.config.ts`
			- ```typescript
			  import { defineConfig } from "$fresh/server.ts";
			  import twindPlugin from "$fresh/plugins/twind.ts";
			  import twindConfig from "./twind.config.ts";
			  export default defineConfig({plugins: [twindPlugin(twindConfig)],});	
			  ```
		- `main.ts`
			- ``` typescript
			  import { start } from "$fresh/server.ts";
			  import manifest from "./fresh.gen.ts";
			  import config from "./fresh.config.ts";
			  await start(manifest, config);
			  ```
		- `dev.ts`
			- ```typescript
			  import dev from "$fresh/dev.ts";
			  import config from "./fresh.config.ts";
			  await dev(import.meta.url, "./main.ts", config);
			  ```
- # Fresh 1.4
  id:: 64e36a9c-0749-4539-8b6b-1ff8de3eb87a
	- https://deno.com/blog/fresh-1.4
	- ## Page Load
	  collapsed:: true
		- Faster page loads with **ahead-of-time** compilation
		- a pre-compile solution that results in assets being served **~45-60x** faster for a cold start of a serverless function, with minimal impact on deployment times.
		- opt into AOT compilation for deployments
			- https://fresh.deno.dev/docs/concepts/ahead-of-time-builds
			- `deno task build` => run as task
			- `deno run -A dev.ts build` => invoke manually
	- ## Layout
	  collapsed:: true
		- sharing parts of the layout across route
		- can put in any route folder
		- option to opt-out of that
			- ```typescript 
			  export const config: RouteConfig = {
			    skipAppWrapper: true, // Disable rendering app wrapper
			    skipInheritedLayouts: true, // Disable already inherited _layout templates
			  };
			  ```
	- ## HTML Tags
	  collapsed:: true
		- allow us to render the HTML document ourself
		- the `<html>` , `<head>` and `<body>`-tag can be set directly on the server.
		- ```typescript
		  // routes/_app.tsx
		  import { AppProps } from "$fresh/server.ts";
		  
		  export default function App({ Component }: AppProps) {
		    return (
		      <html lang="de">
		        <head>
		          <title>My Fresh App</title>
		        </head>
		        <body>
		          <Component />
		        </body>
		      </html>
		    );
		  }
		  ```
	- ## Route groups
	  collapsed:: true
		- is a folder inside the routes dir
		- allow to have different _layout and _middleware files for routes on the same segment
	-