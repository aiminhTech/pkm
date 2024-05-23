tags:: [[Deno]], [[CSV]]

- https://deno.land/std@0.224.0/csv/mod.ts
  title:: std/csv
-
- ## stringify()
	- https://deno.land/std@0.224.0/csv/stringify.ts?s=stringify
	- Write data using CSV encoding.
	-
	- ```js
	  import { stringify } from "https://deno.land/std@0.224.0/csv/stringify.ts";
	  
	  const columns = [
	    { prop: "name" },
	    { prop: "age" },
	    { prop: "gender" },
	  ];
	  
	  const data = [ { name: "foo", age: 10, gender: "male" } ]
	  
	  const csv = stringify(data, {columns})
	  
	  ///console.log
	  "name,age,gender\r\nfoo,10,male\r\n"
	  ```
- ## parse()
	- https://deno.land/std@0.224.0/csv/parse.ts?s=parse
	- CSV parse helper to manipulate data.
	- `parse(input: string): string[][]`
	- ```js
	  parse(csv)
	  
	  ///console.log
	  [ [ "name", "age", "gender" ], [ "foo", "10", "male" ] ]
	  
	  
	  ```
	-