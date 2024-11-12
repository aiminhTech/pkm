tags:: [[SQL]], [[GIBB]]
type:: M165

- [[RDBMS (SQL Datenbank)]]
- [[Big Data]]
-
- ## BASE-Prinzip
  collapsed:: true
	- Das Transaktionskonzept ACID von RDBMS kann bei den meisten NoSQL-Datenbanken nicht erfüllt werden, man verabschiedet sich bewusst davon.
	- Oft kommt das BASE-Prinzip zur Anwendung:
		- ==**B**asically **A**vailable==: Anstatt die sofortige Konsistenz zu erzwingen, gewährleisten NoSQL-Datenbanken jederzeit die Verfügbarkeit der Daten, indem diese über mehrere Knoten des Datenbank-Clusters verteilt und repliziert werden.
		- ==**S**oft State==: Der Zustand der Daten kann ohne Interaktion ändern, weil das System die Daten oft verzögert in einen konsistenten Zustand bringt.
		- ==**E**ventually Consistent==: Auf Transaktionsebene gibt es keine Konsistenzgarantie. Auch solange die Daten noch nicht auf allen Knoten identisch (d.h. konsistent) sind, kann von diesen Knoten gelesen werden. Die Daten sind dabei möglicherweise nicht aktuell.
	- In NoSQL-Datenbanken, die grosse Datenmengen verarbeiten und deshalb stark horizontal skalieren, ist die Aufrechterhaltung des ACID-Prinzips extrem kostspielig. Transaktion erstrecken sich möglicherweise über Dutzende von Instanzen. Aus diesem Grund verwenden diese Datenbanken meist das BASE-Transaktionsmodell.
	- ### Welche Datenbanken verwenden BASE?
		- Die meisten NoSQL-Datenbanken: Redis, Cassandra, MongoDB, CouchDB, usw.
		- MongoDB kann auch als ACID-konforme Datenbank konfiguriert werden.
		- Alle SQL-Datenbanken (RDBMS) funktionieren nach dem ACID-Prinzip. In Ausnahmefällen - bei stark verteilten Datenbanken - kann jedoch davon abgewichen werden.
- ## CAP-Theorem
  collapsed:: true
	-
- ## Stores
  collapsed:: true
	- ### Key-Value Stores
		- #Redis
	- ### Wide-Column Stores
		- #Cassandra
		- ist eine Datenbankstruktur, die entwickelt wurde, um grosse Menge von Daten effizient zu speichern und abzufragen.
	- ### Document Database
		- #MongoDB
		- eine Art von Datenbank, die zur Speicherung, Organisation und Abfrage von unstrukturierten oder halbstrukturierten Daten verwendet wird, die als Dokumente bezeichnet werden.
		- Diese Dokumente können in verschiedenen Formaten wie JSON, XML oder Binärdateien vorliegen und können Text, Bilder, Videos oder andere Arten von Daten enthalten.
	- ### Graph Stores
		- #Neo4j