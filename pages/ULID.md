alias::  Universally Unique Lexicographically Sortable Identifier

- A type of identifier that is designed to be **unique**, **sortable**, and **human-readable** .
- ULIDs are 128-bit identifiers that are **composed of a timestamp and random bits**, which make them unique across different systems.
  
  Some key features of ULIDs are:
-
-
-
- ULIDs are often used in distributed systems, databases, and applications where unique identifiers that are easily sortable based on time of creation are required.
- ## Installation
  collapsed:: true
	- ### Deno
		- https://deno.land/std@0.224.0/ulid/mod.ts
		- ```deno.json
		  import * as mod from "https://deno.land/std@0.224.0/ulid/mod.ts";
		  ```
	- ### npm
		- ```bash
		  npm i ulid
		  ```
	- ### bun
		- ```bash
		  bun add ulid
		  ```