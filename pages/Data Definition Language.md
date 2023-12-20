tags:: Structured Query Language, Datenbanksprachen Datenbank

- alias:: DDL
- Grundfunktionen zum Erstellen einer Datenbank mit Tabellen verwenden
  collapsed:: true
	- **CREATE** – Erstellen
	- **EXPLAIN**– Anzeigen
	- **ALTER** – Verändern
	- **DROP** – Löschen
- ## CREATE
  collapsed:: true
	- ### DATABASE
		- #### Erstellen einer DB
			- ```sql
			  CREATE DATABASE datenbank_name;
			  ```
		- #### DB anzeigen
			- ```sql 
			  SHOW DATABASES;
			  ```
			- ==Dieser Befehl ist nur mit MySQL verfügbar==
		- #### DB wählen
			- ```sql
			  USE datenbank_name;
			  ```
	- ## TABELLE
	  collapsed:: true
		- Beim Erstellen der Tabellen auf die Reihenfolge achten:
		  collapsed:: true
			- 1. Tabellen ohne Fremdschlüssel  => bsp. (Tabelle *firma*)
			- 2. Tabellen mit Fremdschlüssel  => bsp. (Tabelle *mitarbeiter*)
		- ## Tabelle erstellen
		  collapsed:: true
			- ```sql
			  CREATE TABLE tabellen_name (
			    id INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
			    spalte_name_XY datentyp,
			    ...,
			    ...
			  ); 
			  ```
				- **PRIMARY KEY**	=> Primärschlüssel
				- **AUTO_INCREMENT** => Der Wert vom Attribut wird automatisch hochgezählt
				- **NOT NULL** => Die Eingabe eines Wertes wird erzwungen
				- **DEFAULT**	=>  Standardwert wird definiert
		- ## Fremdschlüssel erzeugen
		  collapsed:: true
			- ```sql
			  CREATE TABLE mitarbeiter (
			    id INT PRIMARY KEY AUTO_INCREMENT,
			    firma_id INT NOT NULL,
			    FOREIGN KEY (firma_id) REFERENCES firma (id));
			  
			  ```
			- Fremdschlüssel werden mit **FOREIGN KEY** definiert
			- Attribute des Primär- und Fremdschlüssels müssen vom gleichen Datentyp sein.
		- ## Fremdschlüssel Referenzaktionen
			- Was soll passieren, falls dieser Datensatz gelöscht oder der PK dieses Datensatzes verändert wird?
			- ### SET NULL
				- Alle Werte, die keine Referenz mehr haben, werden auf **null** gesetzt
				- Nicht ideal, da referenzielle Integrität verletzt wird
				- Datenbank ist in undefiniertem Zustand
				- Fehler bei Abfragen, Suchen, …
				- ```sql 
				  CREATE TABLE mitarbeiter (
				    id INT PRIMARY KEY AUTO_INCREMENT,
				    firma_id INT,
				    FOREIGN KEY (firma_id) REFERENCES firma (id)
				    ON DELETE SET NULL ON UPDATE SET NULL);
				  ```
			- ### CASCADE
				- Bei Änderung oder Löschung in der Elterntabelle werden auch alle dazugehörigen Werte in der Kindtabelle gelöscht, respektive geändert
				- Achtung: Daten werden automatisch gelöscht
				- Datenbank behält die referenzielle Integrität
				- ```sql
				  CREATE TABLE mitarbeiter (
				    id INT PRIMARY KEY AUTO_INCREMENT,
				    firma_id INT,
				    FOREIGN KEY (firma_id) REFERENCES firma (id) 
				    ON DELETE CASCADE ON UPDATE CASCADE);
				  ```
			- ### NO ACTION
				- in MySQL **default**:
				- Das Ändern oder Löschen eines Schlüssels wird verhindert, solange noch Abhängigkeiten bestehen
				- Der Benutzer kann keine Daten versehentlich löschen, wenn noch Abhängigkeiten bestehen
				- Datenbank behält die referenzielle Integrität
				- ```sql
				  CREATE TABLE mitarbeiter (
				    id INT PRIMARY KEY AUTO_INCREMENT,
				    firma_id INT NOT NULL,
				    FOREIGN KEY (firma_id) REFERENCES firma (id) 
				    ON DELETE NO ACTION ON UPDATE NO ACTION);
				  ```
- ## EXPLAIN
	- ### Tabellen erklären
	  collapsed:: true
		- ```sql
		  EXPLAIN tabellen_name;
		  ```
		- Mit **EXPLAIN** können die definierten Attribute angezeigt werden
- ## ALTER
	- ### DATABASE
		- #### Löschen
			- Das Löschen einer Datenbank wird beinahe gleich wie das Löschen einer Tabelle gemacht
			- ```sql
			  DROP DATABASE datenbank_name; 
			  ```
	- ### TABELLEN
		- Einzelne Attribute können mit **ALTER** nachträglich zu der Tabelle hinzugefügt oder gelöscht werden
		- #### Attribute hinzufügen
		  collapsed:: true
			- ```sql
			  ALTER TABLE tabellen_name
			  ADD COLUMN spalten_name datentyp [FIRST|AFTER column_name_2];
			  ```
		- #### Attribute ändern
		  collapsed:: true
			- ``` sql
			  ALTER TABLE tabellen_name
			  CHANGE COLUMN spalten_name spalten_name_neu datentyp_neu;
			  ```
		- #### Attribute löschen
		  collapsed:: true
			- Dieser Befehl sollte eigentlich bei einer guten Planung nie gebraucht werden
			- Löscht ohne zu fragen die Tabelle **inkl. Inhalt**!
			- ``` sql
			  ALTER TABLE tabellen_name
			  DROP COLUMN spalten_name;
			  ```
		- #### Fremdschlüssel hinzufügen
		  collapsed:: true
			- ```sql
			  ALTER TABLE <Tabelle1> 
			  	ADD CONSTRAINT <Constraint> 
			      FOREIGN KEY (<Fremdschlüssel>) 
			      REFERENCES <Tabelle2> (Primärschlüssel) 
			  	ON DELETE [NO ACTION], [CASCADE], [SET NULL], [SET DEFAULT];
			  ```
				-
		- #### Fremdschlüssel löschen
		  collapsed:: true
			- ```sql 
			  ALTER TABLE <Tabelle> 
			  	DROP FOREIGN KEY <Constraint>;
			  ```
		- #### Eindeutiger Schlüssel hinzufügen
		  collapsed:: true
			- (z.B. darf jeder Fremdschlüsselwert max. 1x vorkommen):
			- ```sql 
			  ALTER TABLE <Tabelle> 
			  	ADD UNIQUE (<Spalte>);
			  ```
		- #### Eindeutiger Schlüssel löschen:
		  collapsed:: true
			- ```sql 
			  ALTER TABLE <Tabelle> 
			  	DROP CONSTRAINT <Constraint>;
			  ```
		- #### Standardwert festlegen
			- wenn ein Datensatz eingefügt und dieses Attribut weggelassen wird, dann wird der Standardwert eingesetzt):
			- ```sql 
			  ALTER TABLE <Tabelle> 
			  	ALTER <Spalte> SET DEFAULT <Wert>;
			  ```
		- #### Standardwert löschen
			- ```sql 
			  ALTER TABLE <Tabelle> 
			  	ALTER <Spalte> DROP DEFAULT;
			  ```
		- #### Wertebereich festlegen:
			- ```sql 
			  ALTER TABLE <Tabelle> 
			  	ADD CONSTRAINT <Constraint> 
			      CHECK (Ausdruck);
			  ```
			- Ein Ausdruck, der den Wertebereich festlegt. Beispiel: (PLZ >= 1000 AND PLZ <= 9999)
		- #### Wertebereich löschen:
		  collapsed:: true
			- ```sql 
			  ALTER TABLE <Tabelle> 
			  	DROP CHECK <Constraint>;
			  ```
	-