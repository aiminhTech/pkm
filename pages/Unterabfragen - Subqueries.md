tags:: Datenbank

- # DISTINCT
  collapsed:: true
	- DISTINCT = eindeutig
	- Falls nur eindeutige Werte verlangt sind, ist ein **DISTINCT** die bessere Lösung
	- DISTINCT wird häufig bei Unterabfragen verwendet, um die Performance zu verbessern, damit nicht über doppelte Werte Abfragen getätigt werden.
	- Mit **DISTINCT** können Werte so gefiltert werden, dass diese nur einmal in der Ausgabe vorkommen
	- ```sql
	  SELECT DISTINCT(geburtsjahr) FROM katze;
	  ```
	- ![image.png](../assets/image_1687770800955_0.png)
	-
- # GROUP BY
  collapsed:: true
	- Falls für diese eindeutigen Werte noch die Anzahl (COUNT) verlangt wird, muss mit einem **GROUP BY ** gearbeitet werden
	- ```sql
	  SELECT geburtsjahr, COUNT(geburtsjahr)
	  FROM katze
	  GROUP BY geburtsjahr;
	  ```
	- ![image.png](../assets/image_1687770865064_0.png)
	-
- # IN
  collapsed:: true
	- Ermöglicht mehrere Vergleiche gleichzeitig
	- ```sql
	  SELECT vorname FROM mitarbeiter
	  WHERE nachname IN ('Berger', 'Blaser', 'Cartman');
	  ```
	- Anderseits müssten wir folgendes schreiben
	- ```sql
	  SELECT vorname FROM mitarbeiter
	  WHERE nachname = 'Berger' OR
	        nachname = 'Blaser' OR
	        nachname = 'Cartman';
	  ```
- # NOT IN
  collapsed:: true
	- Ermöglicht mehrere  **NOT** Vergleiche gleichzeitig
	- ```sql
	  SELECT vorname FROM mitarbeiter
	  WHERE nachname NOT IN ('Berger', 'Blaser', 'Cartman');
	  ```
	- Anderseits müssten wir folgendes schreiben
	- ```sql
	  SELECT vorname FROM mitarbeiter
	  WHERE nachname != 'Berger' AND
	        nachname != 'Blaser' AND
	        nachname != 'Cartman';
	  ```
- # UNTERABFRAGEN
	- ## Beispiel Datenbank
	  collapsed:: true
		- ![Bildschirmfoto 2023-07-08 um 19.50.17.png](../assets/Bildschirmfoto_2023-07-08_um_19.50.17_1688838620468_0.png)
	- ## Welche Zutaten werden am meisten verwendet?
		- ### Schritt 1
		  collapsed:: true
			- ![Bildschirmfoto 2023-07-08 um 20.04.10.png](../assets/Bildschirmfoto_2023-07-08_um_20.04.10_1688839452775_0.png)
		- ### Schritt 2
		  collapsed:: true
			- ![Bildschirmfoto 2023-07-08 um 20.04.48.png](../assets/Bildschirmfoto_2023-07-08_um_20.04.48_1688839489760_0.png)
		- ### Schritt 3
		  collapsed:: true
			- ![Bildschirmfoto 2023-07-08 um 20.06.54.png](../assets/Bildschirmfoto_2023-07-08_um_20.06.54_1688839616694_0.png)
		- ### Schritt 4
		  collapsed:: true
			- ![Bildschirmfoto 2023-07-08 um 20.02.47.png](../assets/Bildschirmfoto_2023-07-08_um_20.02.47_1688839369153_0.png)
		- ### Schritt 5
		  collapsed:: true
			- ![Bildschirmfoto 2023-07-08 um 20.07.28.png](../assets/Bildschirmfoto_2023-07-08_um_20.07.28_1688839650593_0.png)
		- ### Schritt 6
		  collapsed:: true
			- ![Bildschirmfoto 2023-07-08 um 20.08.10.png](../assets/Bildschirmfoto_2023-07-08_um_20.08.10_1688839696799_0.png)
		- ### Schritt 7
		  collapsed:: true
			- ![Bildschirmfoto 2023-07-08 um 20.08.37.png](../assets/Bildschirmfoto_2023-07-08_um_20.08.37_1688839719280_0.png)
		- ### Schritt 8
		  collapsed:: true
			- ![Bildschirmfoto 2023-07-08 um 20.09.25.png](../assets/Bildschirmfoto_2023-07-08_um_20.09.25_1688839767660_0.png)
			- ![Bildschirmfoto 2023-07-08 um 20.10.53.png](../assets/Bildschirmfoto_2023-07-08_um_20.10.53_1688839854766_0.png)
			-
				-