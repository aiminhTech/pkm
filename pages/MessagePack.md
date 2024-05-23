tags:: [[Deno]]

- https://msgpack.org/
- MessagePack is an efficient binary serialization format.
- It lets you  exchange data among multiple languages like JSON. But it's faster and 
  smaller.
- Small integers are encoded into a single byte, and typical short strings require only one extra byte in addition to the strings themselves.
-
- ## Deno
	- ```ts
	  import * as mod from "https://deno.land/std@0.224.0/msgpack/mod.ts";
	  ```
	- ### decode
		- https://deno.land/std@0.224.0/msgpack/mod.ts?s=decode
		- Decode a value from the MessagePack binary format.
		- ```ts
		   import { decode } from "https://deno.land/std@0.224.0/msgpack/decode.ts"; 
		  ```
	- ### encode
		- https://deno.land/std@0.224.0/msgpack/mod.ts?s=encode
		- Encode a value to MessagePack binary format.
		- ```ts
		  import { encode } from "https://deno.land/std@0.224.0/msgpack/encode.ts";
		  
		  const string = {
		    str: "abc"
		  }
		  
		  const encoded = encode(string)
		  ///console.log
		  [ 129, 163, 115, 116, 114, 163,  97,  98, 99 ]
		  ```