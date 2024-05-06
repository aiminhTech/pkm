tags:: [[LRN-220: Supercheck Website 3.0]], [[LRN-213: Supercheck Website]]

-
- ## Description
	- **Abort**:
		- Möglichkeit RPC-Calls abzubrechen
			- Expliziter Abbruch des Clients mit der ID des laufenden RPC-Requests
			- Abbruch aller Requests eines Clients, falls die Verbindung länger als eine gewisse Dauer unterbrochen wird.
	- **Subscribe**:
		- Möglichkeit aktualisierte Resultate von bereits abgeschlossen RPC-Calls 
		  zu erhalten, falls das Backend denselben RPC-Call für andere Clients 
		  ausführt.
			- Subscription aktivieren
			- Subscription kündigen
				- Automatisches Kündigen aller Subscriptions eines Clients, falls die Verbindung länger als eine gewisse Dauer unterbrochen wird.
			- Client: Aktualisierungen empfangen und anzeigen
			- Backend: Subscriptions verwalten und Aktualisierungen versenden
-
-