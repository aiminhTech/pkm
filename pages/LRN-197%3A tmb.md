tags:: [[IGE]], Typescript, Deno Fresh, TailwindCSS

- Trademark Browser App
- https://issues.ipip.ch/browse/LRN-197
- https://git.ipip.ch/users/quach/repos/tmb/browse
- ## Official links:
	- http://database.ipi.ch/public/apidocs
	- https://git.ipip.ch/projects/IPI/repos/public-frontend/browse/public-frontend-register/public-frontend-register-web/src/main/java/ch/ipi/frontend/register/web/resources
-
- ## Code explanation
	- ### manifest
		- `dp-tmb.yml`
			- #### Annotations Explanation
				- ```yaml
				  annotations:
				    dynatrace.com/inject: "false"
				    oneagent.dynatrace.com/inject: "false"
				    container.inject.dynatrace.com/tmb: "false"
				  ```
				- These annotations stop Dynatrace's monitoring agent from being added to your container. Dynatrace is a tool that monitors application performance, but in this case, you don't want its agent to be added.
			- #### `DENO_V8_FLAGS`  Environment Variable
				- This environment variable is used to set flags for the [[V8 JavaScript engine]], which is used by [[Deno]]
				- ```yaml
				  env:
				  	- name: POD_UID	
				      valueFrom:
				          fieldRef:
				          	fieldPath: metadata.uid
				      - name: DENO_V8_FLAGS
				      value: "--trace-gc,--trace-gc-ignore-scavenger,--no-trace-gc-verbose,--no-trace-gc-heap-layout,--max-heap-size=192"
				  ```
			-
			- `--trace-gc`: Enables tracing of garbage collection (GC) events. This can help developers understand how often the garbage collector is running and how much time it consumes.
			- `--trace-gc-ignore-scavenger`: Ignores trace logs for certain types of garbage collection, specifically "scavenger" GC events, which are a minor type of garbage collection that runs more frequently.
			- `--no-trace-gc-verbose`: Disables verbose logging of garbage collection. So, while `--trace-gc` will show when GC events occur, it won't include overly detailed information.
			- `--no-trace-gc-heap-layout`: Disables the detailed tracing of the layout of the heap during GC events, which can be verbose and is usually more information than necessary for basic GC tracing.
			- `--max-heap-size=192`: Sets the maximum heap size (memory allocated for dynamic allocations) for the V8 engine to 192 MB. This limits the memory usage of the JavaScript runtime, which can help to prevent memory overflows and enhance performance predictability.
	- `auth.ts`
	  collapsed:: true
		- Fetch Access-Token from [[IDP]].
			- ```
			  export async function getToken(
			    username: string,
			    password: string,
			  ): Promise<Token> {
			    return tokenResponse(
			      await fetch(
			        "https://idp.ipi.ch/auth/realms/egov/protocol/openid-connect/token",
			        {
			          method: "POST",
			          headers: {
			            "Content-Type": "application/x-www-form-urlencoded",
			          },
			          body: new URLSearchParams({
			            grant_type: "password",
			            client_id: "datadelivery-api-client",
			            username,
			            password,
			          }),
			        },
			      ),
			    );
			  }
			  ```
		- Helper functions
			- Calc remaining lifetime of a token in second
				- ```
				  interface TokenPayload {
				    exp: number;
				  }
				  
				  export function remainingLifetimeSeconds(tokenPayload: TokenPayload) {
				    const now = Math.ceil(Date.now() / 1000);
				    return tokenPayload.exp - now;
				  }
				  ```
			- Determine if a given authentication token needs to be refreshed
				- ```
				  export async function refreshTokenIfNecessary(token: Token): Promise<Token> {
				    const remaining = remainingLifetimeSeconds(decodeRefreshToken(token));
				  
				    if (remaining < 1) {
				      return token;
				    }
				  
				    if (remaining < token.refresh_expires_in * 0.5) {
				      return refreshToken(token);
				    } else {
				      return token;
				    }
				  }
				  ```
					- `if (remaining < 1) { return token; }`:
						- Checks if the remaining lifetime of the refresh token is less than 1sec.
						- If so => the token is about to expire
						- If not => returns the original token.
					- `if (remaining < token.refresh_expires_in * 0.5) { return refreshToken(token); } else { return token; }`:
						- Checks if the remaining lifetime of the refresh token is less than 50% of the `refresh_expires_in` time.
						- If so =>  it calls a function `refreshToken` to refresh the token, and then returns the refreshed token.
						- If not => returns the original token.
- ## datadelivery deployment
	- ssh jboss@ipieswi025.ipi.ch
	- Dev: http://ipieswi025.ipi.ch/logs/jboss/
	- Prod: http://ipipswi025.ipi.ch/logs/jboss/
- ## Third parties
	- Icons: https://tabler-icons-tsx.deno.dev/
- ## Import
	- ACE Editor:
		- [https://github.com/ajaxorg/ace-builds](https://github.com/ajaxorg/ace-builds)
		- https://github.com/ajaxorg/ace
-