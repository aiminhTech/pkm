- https://github.com/realpha/eitherway
- Ein Tool , das sich mit Problemen im Zusammenhang mit der Fehlerbehandlung in der Softwareentwicklung befasst.
- Der Fokus liegt darauf, die Fehlerbehandlung expliziter und benutzerfreundlicher zu gestalten, 
  unabhängig von den Erfahrungsniveaus und Kontexten der Benutzer.
-
- ## Installation
	- ### Deno
		- ```deno.json
		    "imports": {
		      "eitherway": "https://deno.land/x/eitherway@0.10.0/mod.ts"
		    },
		  ```
- ## Task
	- https://deno.land/x/eitherway@0.9.2/mod.ts?s=Task
	- is a composeable extension of `Promise<Result<T,E>>`
	- It is a `Promise` sub-class, which never rejects, but always resolves.
	  Either with an `Ok<T>` or an `Err<E>`
	- ```typescript
	  import { Result, Task } from "https://deno.land/x/eitherway@0.9.2/mod.ts";
	  
	  interface FailedReq {
	    ok: boolean;
	    foo: number;
	    err: any;
	  }
	  
	  let res: Task<Response, FailedReq> = Task.fromPromise(
	    fetch("https://localhost//api/people/1"),
	    (e) => ({
	      ok: false,
	      foo: 1,
	      err: e,
	    }),
	  );
	  
	  console.log(res);
	  
	  let j: Task<any, FailedReq> = res.andThen((res) =>
	    Task.fromPromise(res.json(), (_e) => ({
	      ok: false,
	      foo: 2,
	    }))
	  );
	  
	  console.log(await j.unwrap());
	  ```
	-
	- Interface `FailedReq`: enthält Eigenschaften `ok` (boolean), `foo` (number) und `err` (any).
	- Es wird eine Task `res` definiert, die mithilfe von `Task.fromPromise` eine asynchrone Anfrage an `https://localhost//api/people/1` sendet. Falls ein Fehler auftritt, wird im Error-Fall ein Objekt mit `ok: false`, `foo: 1` und dem Fehler `err` erstellt.
	- Danach wird eine weitere Task `j` definiert, die das vorherige Ergebnis `res` über `andThen` verwendet, um die JSON-Repräsentation des Ergebnisses zu erhalten. Falls dabei ein Fehler auftritt, wird ein Objekt mit `ok: false` und `foo: 2` erstellt.
	- Das Ergebnis von `j` wird schliesslich mit `await j.unwrap()` ausgegeben, das den Inhalt des Ergebnisses darstellt.