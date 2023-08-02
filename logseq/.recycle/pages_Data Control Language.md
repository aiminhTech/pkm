- #[[Structured Query Language]] #Datenbanksprachen
- alias:: DCL
- Grundfunktionen zum Auslesen der Daten einer Tabellen verwenden
- # SELECT
	- Alle Attribute aus einer Tabelle
		- ```sql
		  SELECT * FROM tabellen_name; 
		  ```
	- Einzelne Attribute aus einer Tabelle
		- ```sql
		  SELECT spaltename_X [, spaltename_Y, …] 
		  FROM tabellen_name;
		  
		  ```