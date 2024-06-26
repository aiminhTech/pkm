tags:: [[IGE]], Typescript, Deno Fresh, TailwindCSS

- Trademark Browser App
- https://issues.ipip.ch/browse/LRN-197
- https://git.ipip.ch/users/quach/repos/tmb/browse
- ## Official links:
	- http://database.ipi.ch/public/apidocs
	- https://git.ipip.ch/projects/IPI/repos/public-frontend/browse/public-frontend-register/public-frontend-register-web/src/main/java/ch/ipi/frontend/register/web/resources
-
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
- ## Third party
	- Icons: https://tabler-icons-tsx.deno.dev/
- ## Import
	- ACE Editor:
		- [https://github.com/ajaxorg/ace-builds](https://github.com/ajaxorg/ace-builds)
		- https://github.com/ajaxorg/ace
-