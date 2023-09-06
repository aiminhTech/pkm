tags:: [[C#]], [[Java]]

- ## C#
	- ### Private Variablen
	  collapsed:: true
		- ```C#
		  private int _number;
		  ```
	- ### Konstanten
	  collapsed:: true
		- ![Bildschirmfoto 2023-05-19 um 16.52.13.png](../assets/Bildschirmfoto_2023-05-19_um_16.52.13_1684507935321_0.png)
		- Im Gegensatz zu **const**, können **readonly** Felder im Konstruktor initialisiert werden.
		- Der Wert einer readonly Variable kann nur bei der Deklaration oder im Konstruktor gesetzt werden.
		- Const kann nicht im Konstruktor initialisiert werden
	- ### Operatoren
	  collapsed:: true
		- ### Vergleiche
		  collapsed:: true
			- ==   <   >   <=   >=   !=
		- ### Arithmetisch
		  collapsed:: true
			- +  -   *  /
			- %  (modulo)
			- Math.Pow(x, y)
		- ### Zuweisung
		  collapsed:: true
			- =  +=  -=   *=   /=    %=   &=
			- |=  ^=  <<=  >>=  ++  --
		- ### Bitweise
		  collapsed:: true
			- & |  ^   ~  <<  >>
		- ### Logical
		  collapsed:: true
			- && ||  &  |   ^   !
	- ### If Statement
	  collapsed:: true
		- ```C#
		  if (a == b) {
		     Console.WriteLine("a == b");
		  } else {
		     Console.WriteLine("a != b");
		  }
		  
		  int c = a > b ? a : b;
		  ```
	- ### Methoden
	  collapsed:: true
		- ```C#
		  //Main method
		  public static void Main(string[] args) {}
		  ```
	- ### String
	  collapsed:: true
		- #### Strings formatieren
		  collapsed:: true
			- ```C#
			  int answer = 42; 
			  string s = string.Format("{0} is the answer", answer);
			  Console.WriteLine(s);
			  	> 42 is the answer
			  
			  
			  
			  //Interpolation
			  
			  int answer = 42; 
			  string s  = $"{answer} is the answer";
			  Console.WriteLine(s);
			  	> 42 is the answer
			  
			  ```
		- #### StringBuilder
		  collapsed:: true
			- ```C#
			  StringBuilder buffer = new StringBuilder("zwei "); 
			  buffer.Append("drei "); 
			  buffer.Insert(0, "eins "); 
			  buffer.Replace("zwei", "ZWEI"); 
			  
			  Console.WriteLine(buffer); 
			  	> eins ZWEI drei 
			  
			  ```
	- ### Loops
	  collapsed:: true
		- ```C#
		  while (i < 10) 
		  i++;
		  
		  
		  for (i = 2; i <= 10; i ++) 
		  Console.WriteLine(i);
		  
		  
		  do  
		  i++; 
		  while (i < 10);
		  
		  
		  foreach (int i in numArray)  
		  sum += i;
		  
		  
		  foreach (Object o in list)
		  Console.WriteLine(o);
		  ```
	- ### Array
	  collapsed:: true
		- ```C#
		  int[] nums = {1, 2, 3};
		  for (int i = 0; i < nums.Length; i++)
		    Console.WriteLine(nums[i])
		    
		    
		  string[] names = new string[5];
		  names[0] = "David";
		  
		  
		  float[,] twoD = new float[rows, cols];
		  twoD[2,0] = 4.5f; 
		  ```
	- ### Enumaration
	  collapsed:: true
		- ```C#
		  enum Action {
		     Start, 
		     Stop, 
		     Rewind, 
		     Forward
		  }
		  
		  Action a = Action.Stop;
		  if (a != Action.Start)
		    Console.WriteLine(a);  // prints Stop 
		  
		  Console.WriteLine((int)a);  // prints 1 
		  
		  ```
	- ### Properties
	  collapsed:: true
		- ```C#
		  public class Human
		  {
		     /// <summary>
		     /// Gets or sets the name of the human.
		     /// </summary>
		     /// <value>
		     /// The name of the human.
		     /// </value>
		     public string Name { get; set; }
		  }
		  
		  ```
		- ### Setter & Getter
		  collapsed:: true
			- ```C#
			  public class Human {
			     private string _name;
			  
			     public string Name {
			        get { return _name; }
			        set {
			           if (value == string.Empty) {
			              throw new InvalidHumanException("Empty string is not a valid human name");
			           }
			           _name = value;
			        }
			     }
			  }
			  
			  ```
		- ### Main-Programm
		  collapsed:: true
			- ![Bildschirmfoto 2023-05-19 um 17.06.29.png](../assets/Bildschirmfoto_2023-05-19_um_17.06.29_1684508790965_0.png)
			- Es wird automatisch erkannt, wenn ein Wert gesetzt oder gelesen wird und die entsprechenden get bzw. set-Methoden werden aufgerufen.
- ## Java
	- ### Operators
	  collapsed:: true
		- #### Logical
		  collapsed:: true
			- Java supports the three logical operators `&&` (AND), `||` (OR), and `!` (NOT).
		- #### Ternary
		  collapsed:: true
			- A lightweight, compact alternative for simple *if/else* statements.
			- Usually used in (but not restricted to) return statements, it needs just one single line to make the decision, returning the left value if the expression is `true` and the right value if `false`
			- ```java
			  boolean expr = 0 != 200;
			  
			  // Ternary statement
			  int value = expr ? 22 : 33;
			  // => 22
			  ```
	- ### If statement
	  collapsed:: true
		- ```java
		  int val;
		  
		  if(val == 9) {
		      // conditional code
		  }
		  ```
		- ```java  
		  if(val == 10) {
		      // conditional code
		  } else if(val == 17) {
		      // conditional code
		  } else {
		      // executes when val is different from 10 and 17
		  }
		  ```
	- ### Switch statement
	  collapsed:: true
		- ```java
		  int val;
		  
		  // switch statement on variable content
		  switch(val) {
		      case 1:
		          // conditional code
		          break;
		      case 2: case 3: case 4:
		          // conditional code
		          break;
		      default:
		          // if all cases fail
		          break;
		  }
		  ```
	- ### For-Each Loops
	  collapsed:: true
		- ```java
		  char[] vowels = { 'a', 'e', 'i', 'o', 'u' };
		  
		  for(char vowel:vowels) {
		      // Output the vowel
		      System.out.print(vowel);
		  }
		  
		  // => aeiou
		  ```
	- ### For Loops
	  collapsed:: true
		- ```java
		  char[] vowels = { 'a', 'e', 'i', 'o', 'u' };
		  
		  for (int i = 0; i < 3; i++) {
		      // Output the vowel
		      System.out.print(vowels[i]);
		  }
		  
		  // => aei
		  ```