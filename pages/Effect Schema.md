tags:: [[Effect TS]], [[Zod]], [[Quicktype]]

- https://effect.website/docs/schema/introduction/
- A library for defining and using schemas** to validate and transform data in TypeScript.
-
- ## Learning
	- Compare with Zod: [https://github.com/Effect-TS/effect/blob/main/schema/comparisons.md](https://github.com/Effect-TS/effect/blob/main/schema/comparisons.md)
	-
- ## Defining a schema
	- https://effect.website/docs/schema/getting-started/#defining-a-schema
-
-
- ## Example
	- ```ts
	  /*
	  const c1 = CompetenceArea.make({ id: CompetenceAreaId.make(22), area: "foo", description: "bar" })
	  
	  for (const key in c1) {
	  
	    if (Object.prototype.hasOwnProperty.call(c1, key)) {
	  
	      const element = c1[key];
	      console.log(key, element);
	  
	    }
	  }
	  
	  const Foo = S.Struct({
	    id: S.Positive,
	    name: S.NonEmptyString.pipe(S.pattern(/.*ooo$/)),
	    url: S.URL
	  })
	  
	  type Foo = typeof Foo.Type
	  
	  const parseFoo = S.decodeUnknownEither(Foo)
	  
	  console.log(parseFoo({ id: 3, name: "barfooo", url: "http://foo" }));
	  
	  const parseScore = S.decodeUnknownEither(Score)
	  
	  //console.log(Score.make({ id: 1, rating3: "foo", rating: "" }));
	  console.log(parseScore({ id: 1, rating: "aaa" })); */
	  
	  ```