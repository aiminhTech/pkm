tags:: [[Java]]

- ## Java
	- ```java
	  public class Main {
	    public static void main(String[] args) {
	      // User Input
	      Scanner scanner = new Scanner(System.in);
	      
	      //User prompt
	      System.out.println("Enter your name: ");
	      
	      //store user's input
	      String name = scanner.nextLine();
	      
	      //print
	      System.out.println("Hello " + name);
	    } 
	  }
	  ```