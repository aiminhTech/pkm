tags:: Structured Query Language, Datenbanksprachen, Datenbank

- alias:: DCL
- wird verwendet, um Benutzer und deren Rechte zu administrieren
- # Benutzer
	- ## Erstellen
	  collapsed:: true
		- ```sql
		  CREATE USER benutzer@hostname IDENTIFIED BY password;
		  ```
		- ```sql
		  CREATE USER hr_manager@localhost IDENTIFIED BY 'secret';
		  ```
			- User hr_manager wird nur für den **lokalen** Host erstellt = Zugriff nur vom lokalen Host aus möglich.
		- ```sql
		  CREATE USER hr_manager@'%' IDENTIFIED BY 'secret';
		  ```
			- User *hr_manager* wird für alle Hosts erstellt = Zugriff von jedem Host aus möglich.
			- Das ==%== ist ein Platzhalter, gleiche Bedeutung wie ==*==.
			- ==%== => entspricht beliebig vielen Charakteren
			- ==_== (Underline) => entspricht genau einem Charakter
	- ## Löschen
		- ### Benutzer mit **DROP** löschen
			- ```sql
			  DROP USER benutzer@hostname;
			  
			  DROP USER hr_manager@localhost;
			  ```
		- ### Datensatz in der Tabelle **[MYSQL.]USER** löschen
			- ```sql
			  DELETE FROM [MYSQL.]USER
			  WHERE user = benutzername;
			  
			  DELETE FROM [MYSQL.]USER
			  WHERE user = "hr_manager";
			  ```
- # Zugriffsrechte
	- ## Vergeben
	  collapsed:: true
		- ==* . *==
		  collapsed:: true
			- Rechte gelten für alle DBs und allen Tabellen
		- ==Datenbank.*==
			- Rechte gelten für alle Tabellen einer bestimmten DB
		- ==Datenbank.Tabelle==
			- Rechte gelten für die angegebene Tabelle
		- Standardmässig kann nur *root* Rechte vergeben
		- ```sql
		  GRANT rechteliste ON db.tabelle TO benutzer@hostname;	
		  GRANT ALL ON firma.mitarbeiterTO hr_manager@localhost;
		  ```
	- ## Entziehen
	  collapsed:: true
		- Rechte können jederzeit wieder mit **REVOKE** entzogen werden
		- ```Sql
		  REVOKE rechteliste ON 
		  db.tabelle 
		  FROM benutzer@hostname;
		  
		  REVOKE ALL ON 
		  firma.mitarbeiter
		  FROM hr_manager@localhost;
		  
		  ```