-
- https://issues.ipip.ch/browse/LRN-249
-
- ## Links
	- https://wiki.ipip.ch/pages/viewpage.action?pageId=199862658#ST.96Mappingf%C3%BCrPatent&ESZ-Einf%C3%BChrung
	- **Mikes Webseite:**  https://st96analyzer.apps.ipip-ocp.ipip.ch/
		- source code: `/ige/jp/esv-projects/esv/patdoc/patdoc-xml-st96/st96analyzer`
-
-
- ## Code
	- ```javascript
	  const dbclickHandler = (event) => {
	    const cellDiv = event.target.closest("div[data-shred-row]"); // Sucht das übergeordnete Div-Element der angeklickten Zelle anhand des Attributs 'data-shred-row'.
	    const expanded = "grid-column: span 3 / span 3; min-height: 2rem"; // Definiert den CSS-Stil für die erweiterte Ansicht.
	    const cells = cellDiv.parentElement.querySelectorAll(`div[data-shred-row="${cellDiv.dataset.shredRow}"]`); // Findet alle Zellen in derselben Zeile basierend auf dem Attribut 'data-shred-row'.
	    cells.forEach(cell => cell.style.cssText === "" ? cell.style = expanded : cell.style = ""); // Erweitert oder minimiert die Zellen je nach aktuellem Stil.
	  };
	  ```
		- Die Funktion erkennt per `event.target.closest` das nächste Elternelement mit dem Attribut `data-shred-row`, um sicherzustellen, dass das richtige Element ausgewählt wird.
		- Der CSS-Stil `expanded` definiert, dass die Zelle über drei Spalten reicht und eine Mindesthöhe von 2rem hat.
		- Dann sucht die Funktion alle Zellen, die dieselbe Zeile (`data-shred-row`) teilen, und setzt den Stil entweder auf den erweiterten Zustand oder entfernt ihn.
-