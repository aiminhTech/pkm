tags:: deno, fresh, session

- https://github.com/Octo8080X/fresh-session
- # Install / Import
	- ``` 
	    "imports": {
	      "fresh-session": "https://deno.land/x/fresh_session@0.2.2/mod.ts"
	    },	
	  ```
- `shared/types/State.ts`
	- ``` typescript
	  import { WithSession } from "fresh-session";
	  
	  export type GlobalState = Record<string, unknown>;
	  export type State = GlobalState & WithSession;
	  ```
- # Create a root middleware
	- https://fresh.deno.dev/docs/concepts/middleware
	- `routes/_middleware.ts`
		- ``` typescript
		  import { MiddlewareHandlerContext } from "$fresh/server.ts";
		  import { cookieSession } from "fresh-session";
		  import { State } from "../shared/types/State.ts";
		  
		  const session = cookieSession();
		  
		  function sessionHandler(req: Request, ctx: MiddlewareHandlerContext<State>) {
		    return session(req, ctx);
		  }
		  
		  function incrementer(_req: Request, ctx: MiddlewareHandlerContext<State>) {
		    const { session } = ctx.state;
		    const counter: number | undefined = session.get("counter");
		    session.set("counter", (counter ?? 0) + 1);
		    return ctx.next();
		  }
		  
		  export const handler = [
		    sessionHandler,
		    incrementer,
		  ];
		  
		  ```
- `routes/foo.tsx`
	- ``` typescript
	  import { Head } from "$fresh/runtime.ts";
	  import { Handlers, PageProps } from "$fresh/server.ts";
	  import { State } from "../shared/types/State.ts";
	  
	  export type Data = { session: Record<string, string> };
	  
	  export const handler: Handlers<Data, State> = {
	    GET(_req, ctx) {
	      const { session } = ctx.state;
	  
	      return ctx.render({
	        session: session.data,
	      });
	    },
	  };
	  
	  export default function Foo({ data }: PageProps<Data>) {
	    return (
	      <>
	        <Head>
	          <title>Foo</title>
	        </Head>
	        <div>
	          <pre>{JSON.stringify(data)}</pre>
	        </div>
	      </>
	    );
	  }
	  
	  ```