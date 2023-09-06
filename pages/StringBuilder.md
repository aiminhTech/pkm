tags:: [[Java]]

- [StringBuilder - Fundamentals Of Object-Oriented Programming: Java and IntelliJ [Video]](https://learning.oreilly.com/videos/fundamentals-of-object-oriented/9781837635702/9781837635702-video2_4/) #[[Fundamentals of object-oriented Programming Java]]
- is a class in Java that provides a more efficient way to work with strings when you need to perform multiple operations like concatenation or modification
- ```java
  StringBuilder sb = new StringBuilder("Hello");
  
  // Append additional text
  sb.append(", World");
  
  // Insert text at a specific position
  sb.insert(5, " Awesome");
  
  // Replace a portion of the string
  sb.replace(6, 13, "Wonderful");
  
  System.out.println(sb.toString()); // Output: "Hello, Wonderful World"
  ```