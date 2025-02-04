tag:: [[GIBB]] 
module:: 183

- ## Injection
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