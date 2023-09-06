tags:: [[Java]]

- An exception is an event or condition that occurs during the execution 
  of a program and disrupts the normal flow of program execution.
- typically used to handle errors, exceptional situations, or unexpected events that may occur at runtime.
- [1.2 Learn the essential data types - Object-Oriented Programming with Java [Video]](https://learning.oreilly.com/videos/object-oriented-programming-with/9780136798163/9780136798163-OPJ1_01_01_02/) #[[Object-oriented Programming With Java]]
- ## Exception Handling
  collapsed:: true
	- ### Try-Catch Block
		- ```java
		  public class TryCatchExample {
		      public static void main(String[] args) {
		          try {
		              int result = divide(10, 0); // Attempt to divide by zero
		              System.out.println("Result: " + result); // This line will not be reached
		          } catch (ArithmeticException e) {
		              System.err.println("Error: " + e.getMessage()); // Handle the exception
		          }
		      }
		  
		      public static int divide(int dividend, int divisor) {
		          if (divisor == 0) {
		              throw new ArithmeticException("Division by zero is not allowed.");
		          }
		          return dividend / divisor;
		      }
		  }
		  ```
	- ### Throw Statement
		- ```java
		  public class ThrowExample {
		      public static void main(String[] args) {
		          int age = -5;
		          try {
		              if (age < 0) {
		                  throw new IllegalArgumentException("Age cannot be negative.");
		              }
		          } catch (IllegalArgumentException e) {
		              System.err.println("Error: " + e.getMessage());
		          }
		      }
		  }
		  ```
	- ### Finally Block
	  id:: 64f84a13-83f3-4efd-96c7-4294ed0f17db
		- ```java
		  public class FinallyExample {
		      public static void main(String[] args) {
		          try {
		              int result = divide(10, 2);
		              System.out.println("Result: " + result);
		          } catch (ArithmeticException e) {
		              System.err.println("Error: " + e.getMessage());
		          } finally {
		              System.out.println("Finally block executed."); // This will always execute
		          }
		      }
		  
		      public static int divide(int dividend, int divisor) {
		          if (divisor == 0) {
		              throw new ArithmeticException("Division by zero is not allowed.");
		          }
		          return dividend / divisor;
		      }
		  }
		  ```