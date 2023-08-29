tags:: Structured Query Language, Datenbanksprachen, Datenbank

- alias:: DQL
- Grundfunktionen zum Auslesen der Daten einer Tabellen verwenden
- # SELECT
	- ## Alle Attribute aus einer Tabelle
	  collapsed:: true
		- ```sql
		  SELECT * FROM tabellen_name; 
		  ```
	- ## Einzelne Attribute aus einer Tabelle
	  collapsed:: true
		- ```sql
		  SELECT spaltename_X [, spaltename_Y, …] 
		  FROM tabellen_name;
		  
		  ```
	- ## Gezieltes Auslesen
	  collapsed:: true
		- Einzelne Entitäten können direkt angesprochen werden
		- ID oder Inhalt eines Attributes in der Bedingung angeben
		- ```sql
		  SELECT spaltename_X [, spaltename_Y, …]
		  FROM tabellen_name WHERE bedingung;
		  ```
	- ## Verknüpfungen
	  collapsed:: true
		- Eine Query kann sich aus mehreren Bedingungen zusammensetzen
		- **AND** und **OR** sind die beiden Kombinationsmöglichkeiten
		- ```sql
		  SELECT spaltename_X, …
		  FROM tabellen_name WHERE bedingung
		  AND bedingung2
		  OR bedingung3;
		  
		  --Bsp
		  SELECT vorname FROM mitarbeiter
		  WHERE vorname = "Max"
		  OR vorname = "Lisi"
		  ```
	- ## Geordnetes Auslesen
	  collapsed:: true
		- Die Entitäten werden selten in einer brauchbaren Reihenfolge eingegeben
		- **ORDER BY** sortiert die Entitäten für die Ausgabe
		- ```sql
		  SELECT spaltename_X, …
		  FROM tabellen_name
		  ORDER BY spaltename_X ASC|DESC;
		  
		  --bsp
		  SELECT vorname FROM mitarbeiter
		  ORDER BY vorname;
		  ```
	- ## WHERE … IN / NOT IN
	  collapsed:: true
		- **IN** = In der Liste / Spalte
		- **NOT IN** = Nicht in der Liste / Spalte
		- ```sql
		  SELECT vorname, name
		  FROM mitarbeiter
		  WHERE vorname IN (’Kurt‘,‘Melanie‘);
		  
		  ```
		- Geht auch mit verschachtelten Abfragen (Unterabfragen / Subqueries)
		- ```sql
		  SELECT name FROM firma
		  WHERE id NOT IN(select firma_id from mitarbeiter);
		  
		  ```
		-
	- ## LIKE / NOT LIKE
	  collapsed:: true
		- **LIKE** wird verwendet, um nach einer bestimmten Zeichenkette/Pattern zu suchen
		- ```sql
		  SELECT f.name AS firma
		  FROM firma AS f
		  WHERE f.name LIKE ‘%a%’;
		  ```
		- Das **%** wird als Platzhalter für null oder mehrere beliebige Zeichen eingesetzt
	- ## BETWEEN
	  collapsed:: true
		- Zwischen Wert *x* und *y*
		- Zahlen, Text oder Daten
		- ```sql
		  SELECT vorname, name
		  FROM mitarbeiter
		  WHERE vorname BETWEEN ‘K‘ AND ‘P‘;
		  *'K' inklusiv
		  *'P' exklusiv
		  ```
		-
	- ## Gruppieren nach Werten
		- **GROUP BY** => gruppiert Werte anhand einer Spalte (Attribut)
		- **HAVING** => erlaubt es die berechneten Werte weiter zu vergleichen/filtern
		- ```sql
		  SELECT f.name AS firma, COUNT(*) AS mitarbeiter
		  FROM mitarbeiter AS m
		  JOIN firma AS f ON m.firma_id=f.id
		  GROUP BY f.name
		  HAVING COUNT(*)>2;	 
		  ```