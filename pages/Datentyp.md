tags:: MySQL, Datenbank

- # Ganzzahlen
  collapsed:: true
	- https://dev.mysql.com/doc/refman/8.0/en/numeric-type-overview.html
	- ![Bildschirmfoto 2023-06-21 um 19.50.14.png](../assets/Bildschirmfoto_2023-06-21_um_19.50.14_1687369816477_0.png)
	- ==INT(11)== hat keinen Einfluss auf die Grösse der gespeicherten Zahl!
	- 11 ist die «display width» => wie viele Stellen sollen angezeigt werden
- # Kommazahlen
  collapsed:: true
	- https://dev.mysql.com/doc/refman/8.0/en/problems-with-float.html
	- ![Bildschirmfoto 2023-06-21 um 19.52.19.png](../assets/Bildschirmfoto_2023-06-21_um_19.52.19_1687369942979_0.png)
	-
- # Textformate
  collapsed:: true
	- https://dev.mysql.com/doc/refman/8.0/en/char.html
	- ![Bildschirmfoto 2023-06-21 um 19.52.49.png](../assets/Bildschirmfoto_2023-06-21_um_19.52.49_1687369973389_0.png)
		- Es gibt zwei sehr wichtige Text-Datentypen:
			- ==CHAR== (Länge) - hat eine festgelegte Länge, die immer voll verwendet wird.
			- ==VARCHAR== (Länge) - hat eine flexible Länge bis zum Maximum und nutzt nur so viel Platz wie nötig.
			- **Beispiel**: Textwert
			  «Peter» in eine Spalte
			- Mit **char (10)**:      «Peter_____» (wird aufgefüllt da fix,also String hat 10 Zeichen)
			- Mit **varchar (10)**: «Peter» (flexibel, jedoch maximal 10 Zeichen möglich) è platzsparender
			- ==CHAR== nimmt man nur bei festgelegten Grössen, wenn die Werte in der Spalte wirklich nur diese Anzahl Zeichen haben. Z.B.: Länderabkürzungen oder PLZ.
			- Name, Städte, etc. hat nicht die  gleiche Grösse also ==VARCHAR==.
- # Date / Time
  collapsed:: true
	- https://dev.mysql.com/doc/refman/8.0/en/date-and-time-types.html
	- ![Bildschirmfoto 2023-06-21 um 19.56.06.png](../assets/Bildschirmfoto_2023-06-21_um_19.56.06_1687370168655_0.png)
		-
	-
- # Weitere Datentypen
  collapsed:: true
	- ## BOOL
		- Gleich wie TINYINT(1) => 0 ist **false**, der Rest ***true***
	- ## ENUM
		- Liste von möglichen Werten
		- https://dev.mysql.com/doc/refman/8.0/en/enum.html
	- ## BLOB
		- Dateien (z.B. Bilder)
		- https://dev.mysql.com/doc/refman/8.0/en/blob.html
		-