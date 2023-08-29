- #Datenbank-Entwurf #Datenbank
- # Tabellenstruktur erstellen
  id:: 6485e8b4-c321-4f88-b299-7027cee6a8ae
  collapsed:: true
	- Entitätstyp als Tabellenname
	- Attribute definieren und eintragen
	- Beispieldatensatz einfüllen
	- ==Entität = Informationsobjekt==
- # Definition von Identifikationsschlüsseln
  id:: 6485e966-93eb-4298-af89-cbe83c73bad4
  collapsed:: true
	- ## Primärschlüssel (Primary-Key)
		- ((6485e3f8-8d96-46a5-ab6a-47c217738616))
		  id:: 6485e993-eb1c-4daf-92a2-260261f91b41
		- **Jeder** Entitätstyp muss einen Primärschlüssel besitzen
		- Primärschlüssel ist eindeutig
		- Darf keine überflüssigen Attribute enthalten (streicht man ein Attribut, darf der
		  Schlüssel nicht mehr eindeutig sein)
		- ==Auch bei der Eingabe von neuen Datensätzen dürfen die Schlüssel die Eindeutigkeit nicht verlieren==
		- ==Ein PK darf keine Nullwerte enthalten==
		- ## Natürliche Schlüssel
			- Kann ein Schlüssel **aus den bestehenden Attributen** gebildet werden, ist dies ein natürlicher Schlüssel. (ISBN, Ländername,...)
		- ## Künstliche Schlüssel
			- Kann **kein** Schlüssel aus den bestehenden Attributen gebildet werden (manchmal will man auch einfach nicht), kann ein künstlicher Schlüssel generiert werden.
			- Dies ist in der Regel eine ID-Nummer…
			- In der Regel werden heutzutage nur noch künstliche oft auto_increment PKs verwendet, da es später für die Softwareentwicklung viel einfacher ist, damit umzugehen.
	- ## Fremdschlüssel (Foreign-Key)
		- ((6485e3f8-2aa0-4165-ae82-0b96018c05fa))
		- Attributeines Entitätstypen, welches in einer anderen Entitätsmenge Primärschlüssel ist („Verweis, Zeiger“)
		- Beispiel:
		  background-color:: green
			- Herr Mayer kann bei den SCL Tigers nur die Funktion als Präsident haben, falls der PK aus den FK ==person_id== und ==verein_id== gebildet wird. Falls er nun aberzusätzlich noch das Amt des Sportchefs übernehmen will (und dies zulässig seinsoll), müsste man zusätzlich auch noch den FK ==funktion_id== in den PK aufnehmen.
			- ![Bildschirmfoto 2023-06-11 um 17.42.53.png](../assets/Bildschirmfoto_2023-06-11_um_17.42.53_1686498176041_0.png)
			- Falls nur die FK ==person_id== und ==verein_id== gemeinsam den PK in der Tabelle ==person_verein_funktion== bilden, kann eine Person im gleichen
			  Verein nur **eine** Funktion innehaben, da sonst die Eindeutigkeit des PK verletzt würde.
			- Nimmt man den FK ==funktion_id== jedoch auch noch in den PK auf, kann eine Person in einem Verein **mehrere** Funktionen haben.