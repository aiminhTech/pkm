- #Datenbank-Entwurf #Datenbank
- # Abstecken des Problemrahmens
  id:: 6485df42-460f-4ded-a452-be874227b3ca
  collapsed:: true
	- Problem definieren
	- Problem analysieren und abgrenzen
	- Substantive anstreichen **(Entitätstypen suchen)**
- # Bildung von Entitätstypen und Attributen
  id:: 6485df47-5a3a-458f-8682-795b5a4941a1
  collapsed:: true
	- Entitätstypen definieren
	- Mögliche Attribute zuordnen
	- Entitätstypen zeichnen
	- ## Darstellung
		- ### Diagramm
			- ![Bildschirmfoto 2023-06-11 um 17.16.16.png](../assets/Bildschirmfoto_2023-06-11_um_17.16.16_1686496579587_0.png)
			- ![Bildschirmfoto 2023-06-11 um 17.18.00.png](../assets/Bildschirmfoto_2023-06-11_um_17.18.00_1686496682799_0.png)
		- ### Tabellenform
			- ![Bildschirmfoto 2023-06-11 um 17.17.08.png](../assets/Bildschirmfoto_2023-06-11_um_17.17.08_1686496630957_0.png)
			- ![Bildschirmfoto 2023-06-11 um 17.19.08.png](../assets/Bildschirmfoto_2023-06-11_um_17.19.08_1686496750691_0.png)
- # Festlegen von Beziehungen
  id:: 6485e028-a4f5-4786-972d-5b00dd56d7b7
  collapsed:: true
	- Entitätstypen verbinden
	- Art der Kardinalität festlegen
	- ## Kardinalitäten
		- ![Bildschirmfoto 2023-06-11 um 17.20.18.png](../assets/Bildschirmfoto_2023-06-11_um_17.20.18_1686496820056_0.png){:height 302, :width 598}
		- ==m==
		  collapsed:: true
			- must, multiple
			- 1 oder mehrere Elemente
		- ==c==
		  collapsed:: true
			- choice, can
			- 0 oder 1 Element
		- ==mc==
		  collapsed:: true
			- must-can
			- 0, 1 oder mehrere Elemente
			-
- # Beziehungen überprüfen
  id:: b9d44628-10a0-4bf2-a673-2cdae5f3e384
  collapsed:: true
	- ==m:m== kann nicht in Tabellen gespeichertwerden!
	- auflösen von komplexen Beziehungen ==[m:m]== und ==[m:mc]==
	- überprüfen der Beziehungen => keine ==[1:1], [1:c]== oder ==[c:c]== (begrenzt
	  sinnvoll)
	- Attribute allenfalls neu zuordnen
	- Bsp.
		- ![Bildschirmfoto 2023-06-11 um 17.28.09.png](../assets/Bildschirmfoto_2023-06-11_um_17.28.09_1686497292305_0.png){:height 150, :width 300}
		- ![Bildschirmfoto 2023-06-11 um 17.28.46.png](../assets/Bildschirmfoto_2023-06-11_um_17.28.46_1686497328051_0.png){:height 150, :width 300}
			-