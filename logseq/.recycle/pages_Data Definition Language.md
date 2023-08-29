- #[[Structured Query Language]] #Datenbanksprachen
- alias:: DML
- Mit der SQL Data Manipulation Language DML lassen sich folgende Aufgaben erledigen:
  id:: 64048b41-84fe-4c83-9827-2e8020d7745d
	- Daten erfassen **INSERT**
	- Daten ändern **UPDATE**
	- Daten löschen **DELETE**
	- Abfragen durchführen **SELECT**
- ## Befehle
	- **ALTER TABLE**
	- Attribute hinzufügen
	  background-color:: blue
		- ```Sql
		  ALTER TABLE <Tabelle> 
		  	ADD <Spalte> <Datentyp>;
		  ```
	- Attribute ändern
	  background-color:: blue
		- ``` sql
		  ALTER TABLE <Tabelle> 
		  	MODIFY COLUMN <Spalte> <Datentyp>;
		  ```
			-
	- Attribute löschen
	  background-color:: blue
	  collapsed:: true
		- ``` 
		  ALTER TABLE <Tabelle> 
		  	DROP COLUMN <Spalte>;
		  ```
		-
	- Fremdschlüssel hinzufügen:
	  background-color:: red
		- ```sql
		  ALTER TABLE <Tabelle1> 
		  	ADD CONSTRAINT <Constraint> 
		      FOREIGN KEY (<Fremdschlüssel>) 
		      REFERENCES <Tabelle2> (Primärschlüssel) 
		  	ON DELETE [NO ACTION], [CASCADE], [SET NULL], [SET DEFAULT];
		  ```
			-
	- Fremdschlüssel löschen:
	  background-color:: red
		- ```sql 
		  ALTER TABLE <Tabelle> 
		  	DROP FOREIGN KEY <Constraint>;
		  ```
	- Eindeutiger Schlüssel hinzufügen
	  background-color:: green
		- (z.B. darf jeder Fremdschlüsselwert max. 1x vorkommen):
		- ```sql 
		  ALTER TABLE <Tabelle> 
		  	ADD UNIQUE (<Spalte>);
		  ```
	- Eindeutiger Schlüssel löschen:
	  background-color:: green
		- ```sql 
		  ALTER TABLE <Tabelle> 
		  	DROP CONSTRAINT <Constraint>;
		  ```
	- Standardwert festlegen 
	  background-color:: purple
		- wenn ein Datensatz eingefügt und dieses Attribut weggelassen wird, dann wird der Standardwert eingesetzt):
		- ```sql 
		  ALTER TABLE <Tabelle> 
		  	ALTER <Spalte> SET DEFAULT <Wert>;
		  ```
	- Standardwert löschen
	  background-color:: purple
		- ```sql 
		  ALTER TABLE <Tabelle> 
		  	ALTER <Spalte> DROP DEFAULT;
		  ```
	- Wertebereich festlegen:
	  background-color:: yellow
		- ```sql 
		  ALTER TABLE <Tabelle> 
		  	ADD CONSTRAINT <Constraint> 
		      CHECK (Ausdruck);
		  ```
		- Ein Ausdruck, der den Wertebereich festlegt. Beispiel: (PLZ >= 1000 AND PLZ <= 9999)
	- Wertebereich löschen:
	  background-color:: yellow
		- ```sql 
		  ALTER TABLE <Tabelle> 
		  	DROP CHECK <Constraint>;
		  ```