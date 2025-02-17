tags:: [[Effect TS]], [[Zod]], [[Quicktype]]

- https://effect.website/docs/schema/introduction/
- A library for **defining and using schemas to validate and transform data** in TypeScript.
-
- ## Learning
	- Crash Course: [https://www.youtube.com/watch?v=nQA_JsCozU4](https://www.youtube.com/watch?v=nQA_JsCozU4)
	- Compare with Zod: [https://github.com/Effect-TS/effect/blob/main/schema/comparisons.md](https://github.com/Effect-TS/effect/blob/main/schema/comparisons.md)
- ## Defining a schema
	- https://effect.website/docs/schema/getting-started/#defining-a-schema
	- One common way to define a `Schema` is by ultilizing the `Struct` constructor. This allows to create a new schema that outlines an object with specific properties.
		- ```ts
		  const Foo = S.Struct({
		    id: S.Positive,
		    name: S.NonEmptyString.pipe(S.pattern(/.*ooo$/)),
		    url: S.URL
		  })
		  
		  type Foo = typeof Foo.Type
		  ```
-
- ## Encode
	- Encoding is the process of **transforming structured TypeScript values** into another format, often for serialization *(sending data to an API, database, or UI)*
- ## Decode
	- Decoding is the process of **validating and transforming** input data *(user input, API repsonse*) into a strongly typed Typescript value.
	- ### decodeUnknown
		- Eine Funktion, die es ermöglicht, **beliebige unbekannte Daten (`unknown`) in ein spezifisches Schema zu dekodieren und zu validieren**
		- Daten aus externen Quellen (z. B. API-Responses oder Formulareingaben) haben oft unbekannte Typen. `decodeUnknown` nimmt ein beliebiges `unknown`-Eingangsobjekt und validiert es gegen das definierte Schema.
		- **Example**
			- ```ts
			  import Schema as S from "@effect/schema";
			  
			  // Definiere ein Schema
			  const UserSchema = S.struct({
			    id: S.number,
			    name: S.string,
			  });
			  
			  // Beispiel-JSON (z.B. API Response)
			  const input: unknown = { id: 123, name: "Alice" };
			  
			  // 3decodeUnknown aufrufen
			  const result = S.decodeUnknown(UserSchema)(input);
			  
			  console.log(result);
			  // Wenn das input den Anforderungen des Schemas entspricht, wird ein Success-Wert mit den typisierten Daten zurückgegeben.
			  /*
			  Success({ id: 123, name: "Alice" })
			  */
			  
			  -----------------------------------------------------------------------------------------------------------------------------
			  const invalidInput: unknown = { id: "foo", name: "Alice" };
			  
			  const result2 = S.decodeUnknown(UserSchema)(invalidInput);
			  
			  console.log(result2);
			  // Da id hier eine String statt einer Nummer ist, schlägt die Validierung fehl.
			  /*
			  Failure(["id must be a number"])
			  
			  ```
			-