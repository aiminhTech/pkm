- #BBC
- # Was ist Telematik
  collapsed:: true
	- Telematik (zusammengesetzt aus Telekommunikation und Informatik) ist eine Technik, welche die Bereiche Telekommunikation und Informatik verknüpft. Telematik ist also das Mittel der
	  Informationsverknüpfung von mindestens zwei Informationssystemen mit Hilfe
	  eines Telekommunikationssystems sowie einer speziellen Datenverarbeitung.
- # Was ist ein Netz?
  collapsed:: true
	- Ein Netzwerk ist ein **Zusammenschluss von zwei oder mehr Computern oder anderen elektronischen Geräten, der den Austausch von Daten und die Nutzung gemeinsamer Ressourcen ermöglicht**
	- ## Elektronische Kommunikation
		- Elektronische Kommunikation zwischen mindestens zwei Endpunkten
		- Wir benutzen diese täglich: Tik Tok, Snapchat, ect.
		- Was braucht es damit die Kommunikation zwischen zwei elektronischen Geräten funktioniert?
			- 2 Geräte
			- 1 Medium
	- ## Wie kann ein Netz aussehen?
		- ## Ausbreitung
			- ### PAN (Personal Area Network)
				- Handy und Bluetooth-Headset
			- ### LAN (Local Area Network)
				- Das Bbc-Office
			- ### CAN (Campus Area Network)
				- Die Berner Universität
			- ### MAN (Metropolitan Area Network)
				- Die Stadt Bern
			- ## WAN (Wide Area Network)
				- Ein Land, meist aber auch ein Synonym für die Welt, obwohl dies eigentlich ein GAN (Global Area Network) wäre.
		- ## Verbindungsart
		  collapsed:: true
			- ### Drahtlos
				- Dein Handy
				- WLAN Zuhause
				- WLAN in den Zügen
			- ### Drahtgebunden
				- Bbc und Edunet Gerät
		- ## Kommunkationsrichtung
		  collapsed:: true
			- ### Simplex
				- Radio (nur in eine Richtung)
				- Man hört nur zu
				- ![Bildschirmfoto 2023-07-27 um 15.26.41.png](../assets/Bildschirmfoto_2023-07-27_um_15.26.41_1690446406442_0.png)
			- ### Halb-Duplex
				- Amateurfunk (abwechselnde Richtung)
				- Man spricht und hört zu, einfach nicht gleichzeitig.
				- ![Bildschirmfoto 2023-07-27 um 15.26.56.png](../assets/Bildschirmfoto_2023-07-27_um_15.26.56_1690446418197_0.png)
			- ### Voll-duplex
				- Man spricht und hört zu, dies sogar gleichzeitig.
				- Reguläre Telefonie (gleichzeitig in beide Richtungen möglich)
				- ![Bildschirmfoto 2023-07-27 um 15.27.09.png](../assets/Bildschirmfoto_2023-07-27_um_15.27.09_1690446432969_0.png)
		- ## Kommunikationsform
		  collapsed:: true
			- ### Unicast
				- 1:1
				- Website, Exklusivität (Video auf Webseite kann gespult werden)
				- ![image.png](../assets/image_1690446575076_0.png){:height 190, :width 428}
			- ### Multicast
				- 1:Alle
				- Dienst ankündigen und Dienst suchen (z.B. Radio, TV über Sender)
				- ![image.png](../assets/image_1690446617893_0.png)
			- ### Broadcast
				- 1:n
				- Push Nachricht, MAC adressierbar («abonnieren»). (z.B. Image auf eine Auswahl an EduNet Rechner gleichzeitig verteilen)
				- ![image.png](../assets/image_1690446642810_0.png)
				-
	- ## Topologie
		- ### Vollvermaschung
		  collapsed:: true
			- ![image.png](../assets/image_1690446860926_0.png)
			- **Vorteile**
				- Jedes Gerät hat eine grosse Bandbreite zu jedem anderen Gerät im Netz.
				- Ausfall eines Gerätes oder einer Verbindung hat auf die anderen keinen Einfluss.
			- **Nachteile**
				- Braucht viel Hardware und Kabel. Ist daher sehr teuer.
		- ### Busnetz
		  collapsed:: true
			- ![image.png](../assets/image_1690446870404_0.png)
			- Veraltet und Heute nicht mehr im Einsatz
			- **Vorteile**
				- Es werden keine weiteren Geräte zur Übermittlung von Daten benötigt
				- Ausfall eines Rechners hat keine Konsequenzen
				- Geringe Kosten
				- Einfache Verkabelung und Erweiterung
			- **Nachteile**
				- Braucht viel Hardware und Kabel. Ist daher sehr teuer.
				- Daten können leicht abgehört werden
				- Eine Störung im Bus blockiert das ganze  Netz
				- Störungen sind schwer zu lokalisieren
		- ### Ringnetz
			- ![image.png](../assets/image_1690446882151_0.png)
			- **Vorteile**
				- Alle Geräte können als Verstärker arbeiten
				- Klar definierte Richtung mit Vorgänger/Nachfolger
			- **Nachteile**
				- Ausfall eines Gerätes führt zu Störungen des Netzes
				- Hoher Verkabelungsaufwand
				- Kann leicht abgehört werden
		- ### Sternnetz
			- ![image.png](../assets/image_1690446915907_0.png)
			- **Vorteile**
				- Ausfall eines Teilnehmers ohne Folgen für das Netz
				- Hohe Übertragungsrate mit Switch möglich
				- Einfach erweiterbar (bis Kapazitätsgrenze der Zentraleinheit)
				- Verständlich
				- Leichte Fehlersuche
			- **Nachteile**
				- Durch Ausfall des Zentralrechners (z.B. Switch) ist das Netz lahmgelegt
				- Zentraler Knoten kann zum Flaschenhals werden
		- ### Baum
			- ![image.png](../assets/image_1690447000717_0.png)
			- **Vorteile**
				- Einfache Konstruktion (z.B. für Gebäudeverkabelung)
				- Einfache strukturelle Erweiterbarkeit
				- übersichtlich
				- Relativ günstig
			- **Nachteile**
				- Bei einem Ausfall eines Vermittlungsgerätes: ganzer unterer Zweig abgeschnitten
				- Schwachstelle zentraler Knoten (Switch)
		- ### Hybride
			- ![image.png](../assets/image_1690447024228_0.png)
			- Topologien kommen auch in kombinierter Form vor
			- z.B.: Stern-Bus-Struktur
			-
		- ###
- # Schichtenmodelle
  collapsed:: true
	- ## OSI
	  collapsed:: true
		- Open System Interconnection
		- Detaillierte Ansicht
		- ![Bildschirmfoto 2023-08-06 um 21.25.32.png](../assets/Bildschirmfoto_2023-08-06_um_21.25.32_1691349936665_0.png)
		- ### Aufgaben der Schichten
			- Layer 1: Hier werden Daten, die aus einzelnen bits bestehen, übertragen
			- Layer 2: Kümmert sich um die Übertragungsprobleme. Dafür muss sie Fehler und Probleme erkennen und beheben.
			- Layer 3: Übernimmt die Logistik. Dabei werden Adressen bereitsgestellt, die zwischen denen der Austausch stattfinden soll und Pakete vom Knotenpunkt zu Knotenpunkt geleitet.
			- Layer 4: Daten in Segemente unterteilt
			- Layer 5: Kontrolliert den Austausch von Nachrichten auf der Transportschicht. Stellt sicher, dass die Dauer des Versands eine Verbindung besteht.
			- Layer 6: Ein Übersetzer, der die Daten entschlüsselt
			- Layer 7: Stellt den Anwendungen und Usern die Funktionalitäten / Services zu Verfügung
		- ### Was wo generiert?
			- Layer 1: Bit
			- Layer 2: Frame
			- Layer 3: Packet
			- Layer: 4 Segment
	- ## TCP/IP
	  collapsed:: true
		- Gröbere Ansicht, aber meistens ausreichend für reine Netzwerk Probleme
		- ![Bildschirmfoto 2023-08-06 um 21.26.07.png](../assets/Bildschirmfoto_2023-08-06_um_21.26.07_1691349971382_0.png)
		- ### Aufgaben der Schichten
			- Layer 1: Kümmert sich um die Übertragung von Daten auf die verschiedene Medien
			- Layer 2: Das nächste Zwischenziel ermittelt und die Pakete dorthin weitergeleitet. Kern dieser Schicht bildet das IP
			- Layer 3: Die Ende-zu-Ende Verbindung herstellen. Generiert kleine Pakete, die in Schichten 2 übermittelt werden. Wichtigsten Protokolle TCP und UDP
			- Layer 4: Protokolle, die mit Programmen zusammenarbeiten und das Netze für den Austausch von Daten nutzen. Bsp: HTTP, SMTP, DNS, usw
			-
	- ## Netzwerkprotokoll
		- Ein Netzwerkprotolle legt fest, wie zwei Rechner kommuniezieren und Daten austauschen.
		- Das Protokoll enthält bestimme Regeln und Definition, welches Format die Übertragung haben muss und wie die Rechner miteinander kommunizieren werden.
- # Netzwerk Komponente
  collapsed:: true
	- ## NIC (Network Interface Card)
		- Layer 1
			- Mit der NIC kann ein Computer an ein Netzwerk angeschlossen werden.
			- Funktion: Signale auf der physischen Schicht senden. Nimmt Daten entgegen und sendet dies.
	- ## Switch
		- Layer 2
			- Verbinder mehrere verschiedene Rechner miteinander (im gleichen Netz)
			- Merkt sich, welche MAC-Adresse an welchem Port angeschlossen ist.
			- Kann von jedem Gerät empfangen werden, da jedes Gerät eine MAC hat
		- Layer 3
			- Funktion:
				- kombiniert die Aufgaben eines Routers in einem Gerät
				- kann nicht von jedem Gerät empfangen werden, da nicht jedes Gerät eine IP hat
	- ## Router
		- Layer 3
		- Funktion:
			- verbindet verschiedene Netze miteinander
			- Ermittlung der verfügbaren Route
	- ## Bridge
		- Layer 2
		- Ein Produkt zur Verbindung eines LAN mit einem anderen LAN
		- Kann verschiedene Medien miteinander verbinden
		- ![image.png](../assets/image_1691350035362_0.png)
	- ## Amplifer
		- Layer 1
		- Verstärkt effektive nur das vorhandene elektronische Signal (nur Layer 1)
		- Wenn Fehler hat, werden diese weitergeschicht
		- Ist nicht Übertragungsmedium spezifisch
	- ## Repeater
		- Layer 1
		- erhält die Funksignale des Routes
		- korrigiert teilweise leichte Verzerunungen des Signale und sendet diese weiter
		- Je nach Art des Repeater kann es sein, dass dieser auf einem höhoren Level arbeitet
	- ## Firewall
		- Hardware: Layer 1-4
		- Software: Layer 5-7
		- ![image.png](../assets/image_1691350048924_0.png)
	-
- # Adressierung
	- ## MAC (Media Access Controll)
	  collapsed:: true
		- Jedes Gerät, welches in einem Netzwerk kommuniziert, hat eine MAC
		- ### Aufbau
		  collapsed:: true
			- ![Bildschirmfoto 2023-08-06 um 21.28.55.png](../assets/Bildschirmfoto_2023-08-06_um_21.28.55_1691350140493_0.png)
			-
	- ## IPv4
	  collapsed:: true
		- logisch verteilbar
		- ### Aufbau
		  collapsed:: true
			- ![Bildschirmfoto 2023-08-06 um 21.38.50.png](../assets/Bildschirmfoto_2023-08-06_um_21.38.50_1691350733144_0.png)
			- Netzteil: bestimmt das IP-Netz in den sich der Host befindet
			- Hostteil: der Bereich, welchen wir benutzen können um Hosts (Geräten) eine logische Adresse zu zuweisen
			- Wenn Hostteil:
				- 0 => Netzadresse
				- 255 => Broadcast-Adresse
		- ### Private Adressen
		  collapsed:: true
			- können nicht für öffentliche Netze verwendet werden
				- im Internet nicht geroutet werden
				- ![Bildschirmfoto 2023-08-06 um 21.40.53.png](../assets/Bildschirmfoto_2023-08-06_um_21.40.53_1691350857122_0.png)
		- ### IPv4-Subnetting
		  collapsed:: true
			- Die Aufteilung eines Netzes in mehrere kleinere Netzwerke
			- Berechnung
				- IP-Adresse in Binär schreiben
				  logseq.order-list-type:: number
				- Subnetmaske in Binär schreiben
				  logseq.order-list-type:: number
				- Logisch UND anwenden, um Netz-ID zu bestimmen 
				  logseq.order-list-type:: number
				- Hostteil alle Bits auf 1 setzen, um Broadcast zu bestimmen
				  logseq.order-list-type:: number
				- Bsp.
					- IP-Adresse: 120.48.7.105
					- Subnetzmaske: 255.255.255.248
					- ![Bildschirmfoto 2023-08-06 um 21.42.10.png](../assets/Bildschirmfoto_2023-08-06_um_21.42.10_1691350933644_0.png)
					  :LOGBOOK:
					  CLOCK: [2023-08-06 Sun 21:06:59]
					  :END:
	- ## IPv6
	  collapsed:: true
		- ## Wozu?
			- dem Internet drohen die Adressen auszugehen
			- mehr mögliche Adressen als bisher zur Verfügung zu stellen
		- ### Aufbau
		  collapsed:: true
			- ![Bildschirmfoto 2023-08-06 um 21.43.00.png](../assets/Bildschirmfoto_2023-08-06_um_21.43.00_1691350985647_0.png)
			- aufgeteilt in 8 Blöcken an je 16Bits
			- validen Werte: 0000 - FFFF (65536 mögliche Werte)
		- ### Netzteil
		  collapsed:: true
			- für das Routing
			- Im Netzteil können die letzten 16 Bits für ein Subnetz ID verwendet werden
			- ![Bildschirmfoto 2023-08-06 um 21.42.38.png](../assets/Bildschirmfoto_2023-08-06_um_21.42.38_1691350962412_0.png)
			- Die Netzmaske muss zu /48 anpassen, wenn man dies tut
			- Hostteil wird automatisch generiert
		- ### Adressentypen
			- #### Unicast
				- ![Bildschirmfoto 2023-08-06 um 21.31.11.png](../assets/Bildschirmfoto_2023-08-06_um_21.31.11_1691350274208_0.png)
				- für ein Interface
				- 2000::/3 => 2000:: bis 3FFF::
			- #### Anycast
			  collapsed:: true
				- ![Bildschirmfoto 2023-08-06 um 21.31.31.png](../assets/Bildschirmfoto_2023-08-06_um_21.31.31_1691350295011_0.png)
				- eine Gruppe von Interfaces, nur das erstes  wird über diese Adresse erreicht
				- 2000::/3 => 2000:: bis 3FFF::
			- #### Multicast
			  collapsed:: true
				- ![Bildschirmfoto 2023-08-06 um 21.30.51.png](../assets/Bildschirmfoto_2023-08-06_um_21.30.51_1691350255373_0.png)
				- für eine Gruppe von Interfaces, alle werden über diese Adresse erreicht
		- ### Adressebereich
		  collapsed:: true
			- #### Global Unicast Address
				- Internet, geroutet auf dem Internet
				- Vergleichbar mit öffentlichen IPv4
				- 2000::/3 => 2000:: bis 3FFF::
			- #### Unique Local
				- Im LAN geroutet
				- vergleichbar mit privaten IPv4
				- FC00::/7 => FC00:: bis FDFF::
			- #### Link Local
				- Netzwerk Link, weder intern nach extern geroutet
				- nicht routebar
				- vergleichbar mit IPv4 APIPA
				-
		-
- # Analyse
	- ## Vermittlungsschicht
	  collapsed:: true
		- `ipconfig`
			- `/all` : alle Konfigurationsinfo
			- `/release` : gibt IP für den abgegebenen Adapter frei
			- `/renew` : ernerut P für den abgegebenen Adapter frei
		- `ping` : Verbindungstest, Auflösung des Hostnamens
		- `route print`
			- anzeige der statischen Routen auf dem Rechner
			- erstellen und löschen einzelner Einträge
		- `tracert`, `pathping`: verfolgen der IP-Pakete über mehrere Router honweg Analysieren der Route
	- ## Transportschicht
	  collapsed:: true
		- `netstat -an`: zeigt offene Netzverbindungen
		- `telnet` : einzelne Sockets testen
		- `nmap` : sockets systematisch scannen
	- ## Anwendungsschicht
	  collapsed:: true
		- `nslookup` : Namensserver Anfragen (z.B Hostname => IP)
		- `ftp, netuse` : einzelne Dienste
-
	-
	-
-
-