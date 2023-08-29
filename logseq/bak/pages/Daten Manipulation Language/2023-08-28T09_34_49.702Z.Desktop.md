- #[[Structured Query Language]] #Datenbanksprachen #Datenbank
- alias:: DML
- Grundfunktionen zum Abfüllen der Tabellen mit Daten verwenden
  id:: 64048b41-84fe-4c83-9827-2e8020d7745d
  collapsed:: true
	- **INSERT**: Daten erfassen
	- **UPDATE**: Daten ändern
	- **DELETE**: Daten löschen
	- **SELECT**: Abfragen durchführen
	-
- # INSERT
	- Werte einfügen
	  collapsed:: true
		- ```sql
		  INSERT INTO tabellen_nameVALUES (
		    value1, value2, ...);
		    
		  
		  INSERT INTO tabellen_name(
		    column_name1, column_name2, ...)
		    VALUES (value1, value2, ...); 
		  
		  ```
	- Mehrere Werte einfügen
	  collapsed:: true
		- ```sql
		  INSERT INTO tabellen_nameVALUES 
		  (value1, value2, ...),
		  (value1, value2, ...),
		  (value1, value2, ...);	
		  ```
- # UPDATE
  collapsed:: true
	- ## Werte verändern
		- Wie beim **SELECT** wird auch hier mit **WHERE** und oft mit der ID gearbeitet
		- ```sql
		  UPDATE tabellen_name
		  SET spaltename_X = ‘neuer Wert’
		  [, spaltename_Y = ‘neuer Wert’,…]
		  WHERE spaltename_Z = ‘XYZ’;
		  	
		  ```
	- ## Werte löschen
		- Mit **DELETE** können einzelne Entitäten gelöscht werden
		- ```sql
		  DELETE FROM tabellen_name; 
		  --Achtung: Ohne WHERE werden alle Inhalte gelöscht!
		  
		  DELETE FROM tabellen_name WHERE bedingung;
		  
		  ```