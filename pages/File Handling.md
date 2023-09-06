tags:: [[Java]]

- [File Handling - Fundamentals Of Object-Oriented Programming: Java and IntelliJ [Video]](https://learning.oreilly.com/videos/fundamentals-of-object-oriented/9781837635702/9781837635702-video3_12/) #[[Fundamentals of object-oriented Programming Java]]
- ## Opening or Creating a File
  collapsed:: true
	- ```java
	  File file = new File("example.txt");
	  ```
- ## Reading from a File
  collapsed:: true
	- ```java
	  try (BufferedReader reader = new BufferedReader(new FileReader("example.txt"))) {
	      String line;
	      while ((line = reader.readLine()) != null) {
	          System.out.println(line);
	      }
	  } catch (IOException e) {
	      e.printStackTrace();
	  }
	  ```
- ## Writing to a File
  collapsed:: true
	- ```java
	  try (BufferedWriter writer = new BufferedWriter(new FileWriter("example.txt"))) {
	      writer.write("Hello, world!");
	  } catch (IOException e) {
	      e.printStackTrace();
	  }
	  ```
- ## Closing the File
  collapsed:: true
	- ```java
	  try (BufferedWriter writer = new BufferedWriter(new FileWriter("example.txt"))) {
	      writer.write("Hello, world!");
	  } catch (IOException e) {
	      e.printStackTrace();
	  }
	  ```
- ## Deleting a File
	- ```java
	  File file = new File("example.txt");
	  if (file.delete()) {
	      System.out.println("File deleted");
	  }
	  ```