tags:: [[Java]]

- ## Java
	- import from `java.time` package
	- [DateTime - Fundamentals Of Object-Oriented Programming: Java and IntelliJ [Video]](https://learning.oreilly.com/videos/fundamentals-of-object-oriented/9781837635702/9781837635702-video1_9/) #[[Fundamentals of object-oriented Programming Java]]
	- ### LocalDate
	  collapsed:: true
		- Represents a date without a time component. It stores year, month, and day information.
		- ```java
		  LocalDate date = LocalDate.now(); // Current date
		  System.out.println("Current date: " + date);
		  // Log entry => Current date: 2023-09-06
		  ```
	- ### LocalTime
	  collapsed:: true
		- Represents a time without a date component. It stores hour, minute, second, and fractional seconds information.
		- ```java
		  LocalTime time = LocalTime.now();
		  System.out.println("Current time: " + time);
		  // Log entry => Current time: 10:30:15.123456789
		  ```
	- ### LocalDateTime
	  collapsed:: true
		- Combines date and time information into a single object.
		- ```java
		  LocalDateTime dateTime = LocalDateTime.now();
		  DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
		  String formattedDateTime = dateTime.format(formatter);
		  System.out.println("Formatted date and time: " + formattedDateTime);
		  // Log entry
		  // Formatted date and time: 2023-09-06 10:30:15
		  ```
	- ### ZonedDateTime
	  collapsed:: true
		- Combines date and time information into a single object.
		- ```java
		  ZoneId zoneId = ZoneId.of("America/New_York");
		  ZonedDateTime zonedDateTime = ZonedDateTime.now(zoneId);
		  System.out.println("New York time: " + zonedDateTime);
		  // Log entry
		  // New York time: 2023-09-06T10:30:15.123456-04:00[America/New_York]
		  ```
	- ### Date Difference
		- #### Period
			- To calculate the difference between two `LocalDateTime` objects and get the duration between them (in hours, minutes, seconds, etc.), you can use the `Duration` class.
			- ```java
			   public static void main(String[] args) {
			          // create dates
			          LocalDate firstDate = LocalDate.of(1999, Month.MARCH, 3);
			          LocalDate secondDate = LocalDate.of(2003, Month.SEPTEMBER, 20);
			  
			          // calc time between dates
			          Period period = Period.between(firstDate, secondDate);
			  
			          System.out.println(period.getYears() + " years");
			          System.out.println(period.getMonths() + " months");
			          System.out.println(period.getDays() + " days");
			      }
			  
			  // Log entry
			  // 4 years
			  // 6 months
			  // 17 days
			  ```