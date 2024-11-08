tags:: [[JavaScript]]

- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals
- They are feauture in JS that allow for easier string manipulation and interpolation. Unlike regular strings, which are enclosed by single or double quotes, template literals are enclosed by **backticks (``)**
-
- ## String Interpolation
	- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#string_interpolation
	- Embed expressions within a template literal using the **`${}`** syntax
	- The expression inside the curly braces is evaluated, and its result is included in the string
	- ```javascript
	  const name = 'John'
	  const message = `Hello, ${name}`
	  
	  console.log(message) //Output: Hello, John
	  ```
- ## Multiline Strings
	- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#multi-line_strings
	- Span multiple lines without the need for escape characters
	- ```javascript
	  const multilineString = `This is a string
	  that span multiple
	  lines`
	  ```
- ## Tagged Templates
	- https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#tagged_templates
	- Template literals can be **tagged** with a function
	- It allows us to **parse a template literal with a custom function**
	- This feature can be useful for various applications, such as *formatting strings*  or *escaping data for security* within our application
	- ### Basic Concept
		- When we use a tagged template, we prefix a function name to the TL. The function processes the TL and its interpolated expressions
		- ```javascript
		   //`strings` is an array containing the literal strings within the template
		   // `values` are the values interpolated `${}` placeholders
		  
		  function currency(strings, ...values) {
		    return strings.reduce((result, str, i) => {
		      const value = values[i] !== undefined ? values[i].toFixed(2) : "";
		      return result + str + (value ? `$${value}` : "");
		    }, "");
		  }
		  
		  const price1 = 29.99;
		  const price2 = 5.5;
		  const total = 35.49;
		  
		  const formattedPrices = currency`Price 1: ${price1}, Price 2: ${price2}, Total: ${total}.`;
		  console.log(formattedPrices);
		  ```
			- **Function Definition**: The `currency` function takes `strings` and `values` as input, similar to previous examples.
			- **Formatting**: Inside the function, we use `reduce` to iterate over `strings`. For each value in `values`, if it is defined, we convert it to a fixed decimal format (e.g., `29.99`) and prefix it with a dollar sign (`$`).
			- **Result Construction**: The function constructs the result string by appending each static string segment (`str`) and the formatted value. If no values are left (`values[i]` is `undefined`), only the string segment is appended.
	- ### Advaned Use
		- Can also be used to create very sophisticated implementations, such as compiling a template literal into a different language or format, like SQL queries or HTML components.
	- ### Benefits
		- **Flexibility**: They give you the power to interpret and manipulate any part of the string including interpolated values.
		- **Security**: They are ideal for building utilities that handle string inputs securely.
		- **Domain-Specific Languages**: They can be used to create DSLs for more intuitive configurations or writing logic.