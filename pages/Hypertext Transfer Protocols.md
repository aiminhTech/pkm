tags:: Frontend

- ## Uniform Resource Locator (URL)
  collapsed:: true
	- Eine URL dient dazu, eine Ressource eindeutig zu kennzeichnen und zu adressieren. Clients können so spezifische Dokumente anfragen. Die allgemeine Form sieht wie folgt aus:
	- https://gitlab.com/ch-tbz-it/Stud/m293g/m293/-/raw/main/T3_Protokoll/x_gitressources/URL.png
	- **Schema**:
		- Immer notwendig und kennzeichnet das Protokoll.
		- ==*http*, *https*,  *mailto*, *ftp*== und andere sind auch möglich.
		- ==": / /"== (ohne Leerzeichen) --> das Protokoll von der Domäne
		- **Domäne**: Firstlevel-, Secondlevel- und Sub-Domain. Der DNS-Server wandelt die Domäne in eine IP-Adresse um.
	- **Port**:
		- Der Port wird normalerweise nicht angegeben und ist standardmässig 80 für *http* und 443 für *https*.
		- Es ist auch möglich, dass ein Webserver einen anderen Port verwenden (z. B. oft 8080). Dann muss der Port zwingend angegeben werden.
	- **Pfad**:
		- Alle Dateien werden auf dem Webserver in einer Ordner-Struktur abgelegt. Mit dem Pfad navigiert man zu der entsprechenden Datei.
	- **Argumente**:
		- Argumente sind ein Weg, Daten an den Server zu übermitteln.
		- Der Server muss aber so eingerichtet sein, dass die Daten auch empfangen werden. Wenn dies nicht der Fall ist, werden die Argumente einfach ignoriert.
		- Argumente werden immer in Schlüssel-Wert-Paaren übertragen, wobei diese mit dem kaufmännischen ==UND (*&*)== getrennt werden. Das Fragezeichen ==(*?*)== kennzeichnet den Start der Argumente.
	- **Anker**:
		- Ein Anker wird mit dem ==# -Tag== gesetzt.
		- Wenn der Anker auf der Seite existiert, wird direkt zu diesem Abschnitt gesprungen.
- ## Wie funktioniert HTTP?
  collapsed:: true
	- ### TCP-Kommunikation
	  collapsed:: true
		- HTTP ist auf TCP aufgebaut und verwendet ein Client-Server Kommunikationsmodell mit Anfragen (Request) und Antworten (Response).
		- Jeder Request und jede Response sendet Nachrichten mit einem Kopf- und einem Inhaltsteil (Header und Body).
		- https://gitlab.com/ch-tbz-it/Stud/m293g/m293/-/raw/main/T3_Protokoll/x_gitressources/RequestResponse.png
	- ### HTTP-Kommunikation
	  collapsed:: true
		- Während auf der TCP-Schicht ganz allgemein Nachrichten (Messages) geschickt werden, definiert die Applikationsschicht (HTTP), welche Inhalte die Nachrichten haben.
		- Im Header der Nachricht (grün) wird Protokoll-Informationen und der HTTP Header verschickt, wie in folgendem Beispiel gezeigt wird. Der Nachrichten-Header (TCP-Schicht) entspricht also nicht dem HTTP-Header (Applikationsschicht), aber der HTTP-Header ist ein Teil des Nachrichten-Headers.
		- https://gitlab.com/ch-tbz-it/Stud/m293g/m293/-/raw/main/T3_Protokoll/x_gitressources/RequestResponseExample.png{:height 272, :width 520}
- ## HTTP Statuscode
  collapsed:: true
	- Liste von Statuscode: https://www.rfc-editor.org/rfc/rfc9110.html#name-status-codes
	- Sendet jede Response einen **Status-Code**, der aussagt, ob die Anfrage erfolgreich war und wenn nicht, welcher Fehler aufgetreten ist.
	- Jeder Status-Code wird mit einer **Status-Nachricht** zurückgeschickt. Die wichtigsten Status-Codes sind:
		- **200 OK**: Die Anfrage war erfolgreich
		- **404 Not Found**: Die Ressource wurde nicht gefunden. Evtl. wurde ein falscher Pfad mitgeliefert.
		- **500 Internal Server Error**: Dieser Fehler kann auftreten bei dynamischen Seiten, die Fehler verursachen.
	-
- ## Request-Methoden
  collapsed:: true
	- HTTP definiert ein Set von Methoden, die bei Anfragen verwendet werden. Die Methoden geben einen Hinweis darauf, was eine Anfrage erreichen möchte.
	- Gesteuert werden die Methoden auf der Seite des Servers. Der Client kann zwar jede URL mit einer beliebigen Methode aufrufen, aber der Server wird nicht auf alle Methoden antworten.
	- Die wichtigsten Methoden:
		- ==GET:==
			- Daten von einer Ressource fordern. Daten vom Browser können **nur** in der URL übermittelt werden, der Request-Body ist leer.
		- ==POST==:
			- Damit sendet der Browser Daten im Request-Body an einen Server, um eine Ressource zu erstellen oder zu ändern.
			- POST ist sicherer als GET, weil die Parameter nicht in der Browser History oder in Web Server Logs gespeichert werden und die gesendeten Daten nicht sichtbar sind.
		- ==PUT==:
			- Wird verwendet, um ein Objekt zu erstellen oder zu aktualisieren.
			- Auch hier wird der Request-Body für die Datenübertragung verwendet.
			- Der Unterschied zu POST: Wenn PUT mehrmals aufgerufen wird (mit dem gleichen Inhalt und Parameter), wird nur ein Objekt erstellt und allenfalls aktualisiert. Im Gegensatz dazu hat das wiederholte Aufrufen einer POST-Anforderung den Nebeneffekt, dass dieselbe Ressource mehrfach erstellt wird.
		- ==DELETE==:
			- Wird verwendet, wenn sie ein Objekt gelöscht werden soll. Der Request-Body ist leer, der Response-Body kann einen Inhalt haben.
		- ==OPTIONS==:
			- Wird verwendet, wenn sie herausfinden möchten, welche Methoden diese URL unterstützt. Der Request- und auch der Response-Body sind leer.
		- ==HEAD==:
			- Wird verwendet, wenn sie nur die Header Informationen möchten. Der Request- und auch der Response-Body sind leer.
		- Weitere: CONNECT, TRACE, PATCH