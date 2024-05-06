tags:: [[Kubernetes]]

- https://kubernetes.io/docs/reference/using-api/health-checks/
- Die Kubernetes-API bietet 3 API-Endpunkte (**healthz**, **livez** und **readyz**), um den aktuellen Status des API-Servers anzuzeigen.
- Maschinen, die die Gesundheit/Lebendigkeit/Bereitschaft des 
  API-Servers überprüfen, sollten sich auf den HTTP-Statuscode verlassen.
- Ein Statuscode 200 zeigt an, dass der API-Server gesund/aktiv/bereit 
  ist, je nach aufgerufenem Endpunkt.
- Die unten aufgeführten ausführlicheren Optionen sind für menschliche Betreiber gedacht, um ihr 
  Cluster zu debuggen oder den Zustand des API-Servers zu verstehen.
- ## healthz
	- Dieser Endpunkt wird verwendet, um den allgemeinen Gesundheitszustand des API-Servers anzuzeigen.
	- Es zeigt an, ob der Server grundsätzlich aktiv ist und ordnungsgemäss funktioniert.
	- *Der Endpunkt ist jedoch veraltet und sollte nicht mehr genutzt werden.*
- ## livez
	- Dient dazu festzustellen, ob der API-Server gestartet und betriebsbereit ist.
- ## readyz
	- Gibt an, ob der API-Server bereit ist, Clientanforderungen entgegenzunehmen.
	- Wenn der **readyz**-Endpunkt "Ready" zurückgibt, ist der Server voll funktionsfähig und kann Anfragen bearbeiten.