- https://www.debuggex.com/
- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_expressions
- Are sequences of characters that define a search pattern. They are primarily used for string matching, searching, and text processing in 
  various programming languages and text editors.
- Regular expressions can be used to search, replace, and manage complex string patterns efficiently.
-
- ## Literal Characters
  collapsed:: true
	- Match the exact text.
	- **Pattern**: `cat`
	- **String**: "I have a cat."
	- **Match**: "cat"
- ## Character Classes
  collapsed:: true
	- Match any one character within brackets.
	- **Pattern**: `[aeiou]`
	- **String**: "hello"
	- **Match**: "e", "o"
- ## Quantifiers
  collapsed:: true
	- Specify the number of occurrences.
	- **Pattern**: `a{2,3}`
	- **String**: "caaandy"
	- **Match**: "aa"
- ## Wildcards
  collapsed:: true
	- Match any single character except a newline.
	- **Pattern**: `c.t`
	- **String**: "cat, cut"
	- **Match**: "cat", "cut"
- ## Anchors
  collapsed:: true
	- Match position within a string.
	- **Pattern**: `^hello`
	- **String**: "hello world"
	- **Match**: Matches "hello" only if at the start of the string.
- ## Escape Sequences
  collapsed:: true
	- Match special characters.
	- **Pattern**: `\.\*`
	- **String**: "I found .something interesting."
	- **Match**: ".*"
- ## Pattern `(.+?)`
  collapsed:: true
	- `.`: Matches any single character except for newline characters.
	- `+`: Matches one or more occurrences of the preceding element (in this case, any character).
	- `?`: Makes the preceding quantifier lazy (non-greedy), meaning it tries to match the smallest number of characters possible 
	  instead of the default greedy behavior (which matches as many charactersas possible).
	- `(.+?)` will match one or more characters but will stop as soon as it can satisfy the overall regular expression, making it the shortest possible match.
-
- ## Non-capturing group `(?:...)`
  id:: 674dc3d7-c7b1-483a-8e50-5e0c793f9fb1
	- Are used to group parts of a pattern without capturing the matched text. This is useful when you 
	  need to apply quantifiers or perform logical grouping, but don't need to reference or store the matched substring.
	- ### Example
		- ```javascript
		  const pattern = /(?:apple|orange)juice/g;
		  const text = "I like applejuice and orangejuice.";
		  
		  const matches = text.match(pattern);
		  console.log(matches); // Output: ['applejuice', 'orangejuice']
		  
		  ```
-
- ## Named capturing group `(?<name>...)`
	- Allow you to assign a name to a group of characters, making it easier to extract and reference specific parts of your match results by name, 
	  rather than by index. This feature improves code readability and helps in managing complex regular expressions.
	- ### Example
		- ```javascript
		  const r = /index-(?<mandant>.*)-processes-(?:[0-9]+)$/
		  const m = "index-ch-marke-geschaeftsprozesse-processes-000001"
		  
		  console.log(r.exec(m))
		  // Ouput: 
		  // [
		  //  "index-ch-marke-geschaeftsprozesse-processes-000002",
		  //  "ch-marke-geschaeftsprozesse",
		  //   index: 0,
		  //  input: "index-ch-marke-geschaeftsprozesse-processes-000002",
		  //  groups: [Object: null prototype] { mandant: "ch-marke-geschaeftsprozesse" }
		  // ]
		  
		  
		  console.log(r.exec(m).groups)
		  // Output: [Object: null prototype] { mandant: "ch-marke-geschaeftsprozesse" }
		  
		  
		  let {mandant} = r.exec(m).groups
		  console.log(mandant)
		  // Output: "ch-marke-geschaeftsprozesse"
		  
		  
		  ```
-