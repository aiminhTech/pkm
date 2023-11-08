tags:: [[C#]], [[Java]] [[Javascript]]

- ## C#
  collapsed:: true
	- ### Primitive Data Types
	  collapsed:: true
		- ![Bildschirmfoto 2023-05-19 um 16.49.07.png](../assets/Bildschirmfoto_2023-05-19_um_16.49.07_1684507749682_0.png)
	- ###  Reference Types
	  collapsed:: true
		- ![Bildschirmfoto 2023-05-19 um 16.51.18.png](../assets/Bildschirmfoto_2023-05-19_um_16.51.18_1684507885058_0.png)
- ## Java
  collapsed:: true
	- ### Primitive Data Types
	  collapsed:: true
		- https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html
		- #### Integer (int)
			- numbers with no digits behind the decimal separator (whole numbers). Examples are `-6`, `0`, `1`, `25`, `976` and `-500000`.
			- An ==int==  is a 32-bit integer
		- #### Double (double)
			- numbers with zero or more digits behind the decimal separator. Examples are `-20.4`, `0.1`, `2.72`, `16.984025` and `1024.0`.
			- A ==double== is a 64-bit floating-point number.
		- #### Boolean
			- Booleans in Java are represented by the `boolean` type, which values can be either `true` or `false`.
			- Boolean operators:
				- `!` (NOT): negates the boolean
				- `&&` (AND): takes two booleans and results in true if they're both true
				- `||` (OR): results in true if any of the two booleans is true
				- ```
				  true || false // => true	
				  false || false // => false
				  false || true // => true
				  true && false // => false
				  true && true // => true
				  !true // => false
				  !false // => true
				  ```
				- The `&&` and `||` operators use **short-circuit evaluation**, which means that the right-hand side of the operator is only evaluated when needed.
				- `!` is sometimes classified as a bitwise operation in the documentation but it has the conventional *NOT* semantics.
	- ### String
	  collapsed:: true
		- an object that represents immutable text as a sequence of Unicode characters (letters, digits, punctuation, etc.)
		- ```java
		  String fruit = "Apple";
		  ```
	- ### Array
	  collapsed:: true
		- Data structures that can hold zero or more elements are known as *collections*.
		- An **array** is a collection that has a fixed size/length and whose elements must all be of the same type. Elements can be assigned to an array or retrieved from it using an index.
			- ```java
			  // Declare array with explicit size (size is 2)
			  int[] twoInts = new int[2];
			  
			  // Assign second element by index
			  twoInts[1] = 8;
			  
			  // Retrieve the second element by index and assign to the int element
			  int element = twoInts[1];
			  ```
		- Arrays can also be defined using a shortcut notation that allows you to both create the array and set its value.
			- ```java
			  // Two equivalent ways to declare and initialize an array (size is 3)
			  int[] threeIntsV1 = new int[] { 4, 9, 7 };
			  int[] threeIntsV2 = { 4, 9, 7 };
			  ```
	-
- ## JavaScript
  collapsed:: true
	- Einfacher als bei Java
	- Es wird nicht zwischen Integer und Double unterschieden
	- ![Bildschirmfoto 2023-08-02 um 20.40.04.png](../assets/Bildschirmfoto_2023-08-02_um_20.40.04_1691001606909_0.png)
	- ### String
	  collapsed:: true
		- ```jsx
		  
		  let text = "John";                 // Datentyp: String
		  let text2 = text + " " + "Doe";
		  let text3 = `Hey ${text}`;	// Template String
		  let text4 = `overlay ${menu.isOpen ? "" : "hidden"}`;
		  let char = text[0]                 
		  let size = text.length;       
		  // Datentyp: Number
		  text = text.substring(2, 2) 
		  text = text.toUpperCase();
		  text = text.replace("John", "Sam");
		  
		  
		  ```