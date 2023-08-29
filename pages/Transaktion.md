tags:: Datenbank

- # Was ist eine Transaktion?
	- Eine Transaktion fasst mehrere Arbeitsschritte zusammen und sorgt dafür, dass diese
	  alle zusammen ausgeführt werden, oder alle zusammen nicht ausgeführt werden
	  (Alles-oder-nichts-Prinzip)
	- Bespiel : Wenn man Geld von seinem Konto auf ein anderes überweisen.
		- ```sql
		  UPDATE konto SET saldo = saldo – 500 WHERE konto_nr = 786345343;
		  UPDATE konto SET saldo = saldo + 500 WHERE konto_nr = 123325932; 
		  ```
		- ==Das Geld wäre aber verloren, wenn es nicht auf das zweite Konto gebucht werden könnte, da die Kontonummer nicht gültig ist==
-
- # ACID-Kriterien
	- ## Atomic
		- ==Unteilbarkeit==: Alles-oder-nichts-Prinzip
	- ## Consistent
		- ==Konsistenz==: Wenn das System vor der Transaktion in einem gültigen Zustand war,
		  dann ist es dies auch nachher
	- ## Isolated
		- ==Isolierung==: Transaktionen laufen ungestört von anderen Transaktionen ab (es
		  können nicht die selben Daten von verschiedenen Transaktionen bearbeitet
		  werden)
	- ## Durable
		- ==Dauerhaftigkeit==: Mit Commit abgeschlossene Änderungen sind persistent
-
- # Transaction Control Language
	- **TCL** wird verwendet, um Transaktionen zu kontrollieren
	- ```sql
	  START TRANSACTION - Transaktion beginnen
	  COMMIT / ROLLBACK – Transaktion bestätigen / abbrechen
	  ```
- # Die Lösung
	- https://dev.mysql.com/doc/refman/8.0/en/commit.html
	- ```sql
	  START TRANSACTION;
	  UPDATE konto SET saldo = saldo – 500 WHERE konto_nr = 786345343;
	  UPDATE konto SET saldo = saldo + 500 WHERE konto_nr = 123325932;
	  COMMIT;
	  -- oder
	  ROLLBACK;
	  
	  ```
	- ==INSERT-, UPDATE-, DELETE-Anweisung== in einer Transaktion zusammenfassen
	- Mit ==COMMIT== bestätigen oder mit ==ROLLBACK== wieder Ursprungzustand herstellen
	- Fallunterscheidung nicht direkt mit SQL, sondern in darüber liegenden Programmschicht
-