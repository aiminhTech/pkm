- #Datenbank
- SQL Abfragen über mehrere Tabellen
- Beispiel Tabellen
  collapsed:: true
	- ![Bildschirmfoto 2023-06-21 um 21.12.22.png](../assets/Bildschirmfoto_2023-06-21_um_21.12.22_1687374745507_0.png)
- # Tabellen verbinden
  collapsed:: true
	- ## Variante 1 - WHERE
	  collapsed:: true
		- ```Sql
		  SELECT mitarbeiter.name, firma.name 
		  FROM mitarbeiter, firma
		  WHERE mitarbeiter.firma_id=firma.id;
		  
		  ```
		- ![image.png](../assets/image_1687374862611_0.png)
		- ```sql
		  *Attributnamen mit Alias
		  SELECT mitarbeiter.name AS name, firma.name AS firma 
		  FROM mitarbeiter, firma
		  WHERE mitarbeiter.firma_id=firma.id;
		  
		  SELECT m.name AS name, f.name AS firma 
		  FROM mitarbeiter AS m, firma AS f
		  WHERE m.firma_id=f.id;
		  ```
		- ![image.png](../assets/image_1687374954963_0.png)
	- ## Variante 2 - JOIN
		- ### INNER JOIN
		  collapsed:: true
			- Den PK und FK von Tabellen in einem **JOIN** (INNER JOIN) verbinden
			- ```sql
			  SELECT m.name AS name, f.name AS firma 
			  FROM mitarbeiter AS m
			  JOIN firma AS f ON m.firma_id=f.id;
			  
			  ```
		- ### LEFT JOIN
		  id:: 64934d26-4ab3-4f52-82c9-9a125797bf80
		  collapsed:: true
			- Die **linke** Tabelle wird vollständig ausgegeben
			- Links im Sinn von: Links vom JOIN
			- ```sql
			  SELECT m.name AS name, f.name AS firma 
			  FROM mitarbeiter AS m
			  LEFT JOIN firma AS f ON m.firma_id=f.id;	
			  ```
			- ![image.png](../assets/image_1687375219234_0.png)
		- ### RIGHT JOIN
		  collapsed:: true
			- Die **rechte** Tabelle wird vollständig ausgegeben
			- Rechts vom JOIN
			- ```sql
			  SELECT n.name AS name, f.name AS firma 
			  FROM mitarbeiter AS m
			  RIGHT JOIN firma AS f ON m.firma_id=f.id;
			  
			  ```
			- ![image.png](../assets/image_1687375310628_0.png)
			-
- # Aggregatsfunktion
  collapsed:: true
	- ## COUNT
	  collapsed:: true
		- Zum Rechnen, Zählen und Vergleichen
		- ```sql
		  SELECT COUNT(*) AS anzahl
		  FROM mitarbeiter
		  WHERE name BETWEEN ‘S’ AND ‘T’;
		  ```
		- ![image.png](../assets/image_1687375398922_0.png)
		- ![image.png](../assets/image_1687375403954_0.png)
	- ## Weitere Aggregatsfunktionen
	  collapsed:: true
		- ![Bildschirmfoto 2023-06-21 um 21.23.49.png](../assets/Bildschirmfoto_2023-06-21_um_21.23.49_1687375431031_0.png)
		- https://dev.mysql.com/doc/refman/8.0/en/func-op-summary-ref.html
		- https://dev.mysql.com/doc/refman/8.0/en/group-by-functions.html