tags:: [[Datenbank]]

- ## Relationales Datenbankmanagementsystem RDBMS
  collapsed:: true
	- Oft wird der Begriff SQL-Datenbanken als Synonym für relationale Datenbanken oder RDBMS verwendet. Das ist nicht korrekt, denn SQL ist eine Datenbanksprache und kein Datenbanksystem.
	- In einer relationalen Datenbank werden die Daten in Tabellen gespeichert. Jede Tabelle enthält Datensätze (Tupel, Zeilen) und jeder Datensatz besteht aus Attributen (Merkmale, Spalten). Eine Relation besteht aus Datensätzen und Attributen und kann folgende Ausprägungen annehmen:
	  collapsed:: true
		- Alle Datensätze einer Tabelle
		- Einige Datensätze einer Tabelle
		- Alle Datensätze aus einem Tabellenverbund von 2 oder mehr Tabellen
		- Einige Datensätze aus einem Tabellenverbund von 2 oder mehr Tabellen
		- wobei
			- Alle Attribute angezeigt werden
			- Nur ein Teil der Attribut angezeigt werden
		- Die Beziehungen zwischen den Tabellen werden durch Primär- und Fremdschlüssel hergestellt.
	- ### Wichtigste Grundsätze:
		- Möglichst wenig Redundanzen (erreicht durch den Normalisierungsprozess)
		- Keine Inkonsistenzen (erreicht durch referentielle Integrität)
- ## ACID-Prinzip
	- Die Datenintegrität in einem Mehrbenutzersystem wird mit dem ACID-Prinzip sichergestellt: Änderungen dürfen erst sichtbar gegen aussen werden, wenn alle Integritätsbedingungen erfüllt sind.
	- ### Transaktionskonzept
		- ==**A**tomicity (Atomarität)==:
			- Eine Transaktion wird entweder komplett durchgeführt oder gar nicht
		- ==**C**onsistency (Konsistenz):==
			- Eine Transaktion muss nach Beendigung einen konsistenten Datenbankzustand hinterlassen
		- ==**I**solation:==
			- Jede Transaktion wird von parallel ablaufenden Transaktionen isoliert, läuft also ab wie in einer Einbenutzerumgebung
		- ==**D**urability (Dauerhaftigkeit):==
			- Garantie, dass Daten nach dem erfolgreichen Abschluss einer Transaktion dauerhaft in der Datenbank gespeichert sind
	- ### Use Case
		- In Branchen wie dem Finanzwesen, dem Gesundheitswesen und der staatlichen Verwaltung weit verbreitet. => Dank der ACID-Konformität müssen sich die Kunden einer Bank beispielsweise keine Sorgen machen, dass ihre Kontostände falsch angezeigt werden, da eine ACID-konforme Datenbank immer über aktuelle Daten verfügt.
		- Auch viele kleine bis mittlere Unternehmen nutzen ACID-konforme Datenbanken wegen ihrer Benutzerfreundlichkeit und Stabilität.
	- ### Welche Datenbanken verwenden ACID?
		- **Alle SQL-Datenbanken**: Oracle, MySQL, MariaDB, PostgreSQL, SQL Server, usw.
		- Es gibt NoSQL-Datenbanken, die mit ACID funktionieren, z.B. Neo4j oder Couchbase.
		- Es gibt NoSQL-Datenbanken, die als BASE und ACID konfiguriert werden können, z.B. MongoDB.
		- Der Grossteil der NoSQL-Datenbanken jedoch arbeitet ausschliesslich mit dem BASE-Prinzip.