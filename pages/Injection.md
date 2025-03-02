tags:: [[Applikationsicherheit implementieren]]

- In der Informatik bezeichnet **Injection** eine Technik, bei der **unerwünschte oder schädliche Daten in ein System eingefügt** werden.
- Sie passiert, wenn ein User Eingaben macht, die nicht nur als Daten behandelt werden, sordern vom System als ==Code== geführt. Dadurch kann ein Angreifer Funktionen auf dem Server ausführen, die eigentlich nicht erlaubt sind. Das Problem entsteht, weil das Programm Eingaben eines Nutzers direkt in **Interpretern** oder Systemkommandos verwendet, ohne sie zu überprüfen oder abzusichern.
- ### Grundstruktur einer Injektion:
	- Der **fest programmierte Teil** (z. B. ein SQL-Befehl oder ein Kommando) ist fix und wird vom Entwickler definiert.
	- Der **variable Teil** kommt aus Benutzereingaben, z. B. durch ein Eingabefeld.
	- Wenn diese Eingaben nicht sicher verarbeitet werden, kann ein Angreifer bösartigen Code einschleusen, der dann als Teil des Programms ausgeführt wird.
- ### Beispiele für verwundbare Systeme:
	- **Datenbanken (SQL)**: Einschleusen von SQL-Befehlen, um auf geschützte Daten zuzugreifen.
	- **Browser (XSS)**: Einfügen von JavaScript, um Benutzerdaten zu stehlen.
	- **Dateisysteme (Directory Traversal)**: Zugriff auf Dateien außerhalb des erlaubten Bereichs.
	- **Betriebssysteme (Command Injection)**: Ausführen von Systembefehlen.
	- **Libraries**: Angriffe über schlecht abgesicherte Drittanbieter-Bibliotheken (z. B. Logging, XML).
- ### Fazit
	- Jedes System, das Benutzereingaben entgegennimmt und weiterverarbeitet, ist potenziell angreifbar. Entwickler müssen sicherstellen, dass Eingaben **geprüft und bereinigt** werden, bevor sie in kritischen Bereichen wie Datenbanken oder Interpretern genutzt werden.
-
- ## Shell Injection
- ## XSS Injection
- ## SQL Injection
	- Eine Art von Angriff, bei dem ein Angreifer schädlichen SQL-Code in eine DB-Abfrage einschleust, um um unerlaubt auf Daten zuzugreifen oder die Datenbank zu manipulieren. Eine Webanwendung übergibt Nutzereingaben oft direkt an eine SQL-Datenbank. Wenn diese Eingaben nicht richtig überprüft werden, kann ein Angreifer SQL-Befehle einschleusen.
	- ### Beispiele
		- #### Zugriff auf alle Daten
			- ```sql
			  --Ein unsicheres Login-System könnte folgenden SQL-Befehl nutzene:
			  SELECT * FROM users WHERE username = '$eingabe' AND password = '$passwort';
			  
			  --Ein Angreifer könnte als Benutzername eingeben:
			  ' OR '1'='1
			  
			  --Dann sieht die SQL-Abfrage so aus:
			  SELECT * FROM users WHERE username = '' OR '1'='1' AND password = '$passwort';
			  
			  --Da 1=1 immer wahr ist, kann sich der Angreifer ohne gültiges Passwort 
			  anmelden.
			  ```
		- ####  Daten aus einer anderen Tabelle auslesen
			- Mit `UNION SELECT` kann ein Angreifer Daten aus einer anderen Tabelle abrufen.
			- ```sql
			  99999' UNION SELECT name, tel FROM customer; #
			  ```
			- Falls die Tabelle `users` keinen Eintrag mit `id = 99999` hat, liefert die Datenbank stattdessen Namen und Telefonnummern aus der Tabelle `customer`.
	- ### Schutz vor SQL Injection:
		- **Prepared Statements verwenden** (z. B. mit `?` als Platzhalter)
		- **Eingaben validieren und escapen**
		- **Minimale Rechte für die Datenbankbenutzer vergeben**