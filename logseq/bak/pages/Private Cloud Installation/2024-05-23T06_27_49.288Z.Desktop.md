tags:: [[M346 - Cloud Lösung konzipieren und realisieren]]

- ## Aufbau einer Private Cloud Allgemeine
	- Das Ziel der Private Cloud ist virtuelle Maschinen in einer Cloud zur Verfügung zu stellen.
- ## Ablaufplan zur Installation der Cloud
	- ![Bildschirmfoto 2023-12-03 um 18.12.50.png](../assets/Bildschirmfoto_2023-12-03_um_18.12.50_1701623573553_0.png)
- ## Remote Verbindung einrichten (Fernzugriff per SSH)
	- Braucht es dazu einen **private** und einen **public** Key
	- Server und Client tauschen die Schlüssel aus.
	- ### Authentisierung
		- #### mit öffentlichem Schlüssel
		  collapsed:: true
			- Auf dem Gerät, das zugreifen will => ein private und public Key erstellen
			- Dann wird der ==public Key== auf das Gerät übertragen, auf das wir zukünftig zugreifen wollen.
			- ![Bildschirmfoto 2023-12-03 um 18.33.56.png](../assets/Bildschirmfoto_2023-12-03_um_18.33.56_1701624838642_0.png){:height 426, :width 718}
		- #### mittels Passworts
		  collapsed:: true
			- Der Client baut eine Verbindung zum Server auf und sendet den ==public Key== an den Client.
			- Der Client vergleicht den vom Server gesendeten public Key mit Einträgen in der Datei know_hosts.
			- Ist dem Client der public Key nicht bekannt, fragt er den Benutzer, ob der Fingerabdruck des Servers ok ist.
			- ![Bildschirmfoto 2023-12-03 um 18.36.40.png](../assets/Bildschirmfoto_2023-12-03_um_18.36.40_1701625001606_0.png)
	- ==Diese Methode bietet eine verschlüsselte Verbindung, die Authentifizierung ist aber nach wie vor per Passwort und erhöht die Sicherheit nicht.==
	- ### Public und Private Key erstellen
		- Private und Public Key erstellt man mit cmd `ssh-keygen`
		- Es wird ein entsprechendes Schlüsselpaar auf den lokalen Maschinen erzeugen.
		- Dadurch entstehen zwei Dateien.
			- **Ein privater Schlüssel** => (**id_rsa**) welcher auf dem lokalen System (Client) verbleibt
			- **Ein öffentlicher Schlüssel** => (**id_rsa.pub**) welcher später auf den Server übertragen wird.
			- `ssh-keygen -o -t rsa -C "vmadmin@iet-gibb.ch" -b 4096`
				- Parameter:
				  ==-t== bestimmt Verschlüsselungstyp. Es können sowohl RSA als auch Ed25519 verwendet werden. Die Vorteile des Verschlüsselungsalgorithmus Ed25519 sind - sicherer, schneller zu verifizieren und kompakter von der Dateigrösse.
				- ==-o== es wird Openssh verwendet.
				- ==-C== gibt den Kommentar an, der am Schluss des Schlüssels erscheint.
				- Die Schlüssel finden Sie nach dem Erstellen im Ordner: