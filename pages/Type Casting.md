tags:: [[C#]], [[Java]]

- ## Java
	- [Type Casting - Fundamentals Of Object-Oriented Programming: Java and IntelliJ [Video]](https://learning.oreilly.com/videos/fundamentals-of-object-oriented/9781837635702/9781837635702-video2_5/) #[[Fundamentals of object-oriented Programming Java]]
	- In Java, there are two types of casting:
		- **Widening Casting** (automatically) - converting a smaller type 
		  to a larger type size
			- `byte` -> `short` -> `char` -> `int` -> `long` -> `float` -> `double`
		- **Narrowing Casting** (manually) - converting a larger type 
		  to a smaller size type
			- `double` -> `float` -> `long` -> `int` -> `char` -> `short` -> `byte`
	- ### Widening Casting
		- Widening casting is done automatically when passing a smaller size type to a 
		  larger size type:
		- ```java
		  public class Main {
		    public static void main(String[] args) {
		      int myInt = 9;
		      double myDouble = myInt; // Automatic casting: int to double
		  
		      System.out.println(myInt);      // Outputs 9
		      System.out.println(myDouble);   // Outputs 9.0
		    }
		  }
		  
		  ```
	- ### Narrowing Casting
		- Narrowing casting must be done manually by placing the type in parentheses 
		  in front of the value:
		- ```java
		  public class Main {
		    public static void main(String[] args) {
		      double myDouble = 9.78d;
		      int myInt = (int) myDouble; // Manual casting: double to int
		  
		      System.out.println(myDouble);   // Outputs 9.78
		      System.out.println(myInt);      // Outputs 9
		    }
		  }
		  
		  ```