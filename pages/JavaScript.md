tags:: [[node.js]], [[Programming Language]]

- [[Syntax]]
- [[Data Types]]
- ## JS im Browser
	- https://developer.mozilla.org/en/
	- JS wird vom Browser ausgeführt
		- beim Laden von <script> tags in [[HTML]]
		- beim Laden von externen JS-Dateien
		- bei Browserevents (Maus, Tastatur, Touch,...)
	- ### Globaler Kontext
		- 1 Browser Tab = 1 **Window Objek**t im Browserspeicher
		- F5 erstellt das **Window Objek**t neu
		- ```
		  console.log("AHA!");
		  alert("Hallo Javascript");
		  setTimeout(/* … */);
		  setInterval(/* … */);
		  fetch(/* … */); // wird morgen relevantlocation.replace("/index.html"); // Browser springt zu index.html
		  history.back(); // Springe zur letzten Seite
		  history.forward() // Springe wieder zur aktuellen Seite
		  navigator.language; // "de-DE" Sprache des Browsers
		  
		  // "document" zeigt auf den DOM -> nächste Folie …
		  document.getElementById("button"); 
		  ```
	- ### DOM (Document Object Model)
	  collapsed:: true
		- bezeichnet die HTML Baustruktur
		- document beitet Zugriff auf das DOM
		- HTML und CSS können beliebig verändert werden
		- ![image.png](../assets/image_1674812848475_0.png)
		-
	- ### Die wichtigsten Attribute aller HTML Elemente
	  collapsed:: true
		- ```jsx
		  
		  const htmlElement = document.getElementById("myBtton"); 
		    
		  // Element verändern
		  htmlElement.innerText = "Code zwischen Start- und Endtag ersetzen";
		  htmlElement.append("<h1>Neu</h1>");
		  // Arbeiten mit CSS Styles
		  htmlElement.style = "background-color: #4CAF50; border: none; color: white;";
		  htmlElement.style.visibility = "hidden"; visible | hidden | collapse
		  // Best Practice: Arbeite mit CSS Class und setze Attribute nicht direkt!
		  htmlElement.classList.add("red");
		  htmlElement.classList.remove("red");
		  htmlElement.classList.toggle("red");
		  htmlElement.addEventListener("click", () => {});
		  
		  
		  ```
	- ### Weitere Zugriffsmethoden
	  collapsed:: true
		- **querySelector()** und **querySelectorAll()** erhalten als Argument eine CSS-Selektor-String.
		- ```jsx
		        
		  document.querySelector("input"); // das erste HtmlInputElement
		  document.querySelectorAll("#container.item"); 
		  
		  document.getElementById("id");
		  document.getElementsByName("name");
		  document.getElementsByClassName("class");
		  
		  ```
		- document repäsentiert das DOM
		- this.document liegt im Window Objekt
		- Der Code zeigt mögliche Zugriffsmethoden auf den DOM
		- querySelector() und querySelectorAll() sind neuer, besser Typisierten und am flexibelsten
		-
	- ### Events
		- EventListener und Events sind ähnlich wie in JAVA
		- Es existieren viele unterschiedliche Events
		- Unterschiedliche HTML Elemente haben unterschiedliche Events
		- ![image.png](../assets/image_1691002388954_0.png)
		- Du hast unterschiedliche Möglichkeiten eine EventListener zu registrieren.
		- Meist möchtest du dabei kein JS in deinen HTML Files.
		- ![image.png](../assets/image_1691002410220_0.png)
		-
- ## Kommunikation mit dem Webserver
  collapsed:: true
	- ### Der Begriff Webserver
		- Liefert Dokumente an Clients aus
			- HTML-Seiten an unseren Browser
			- Dasselbe mit CSS, JavaScript, JSON und Bilder
		- Andere Funktionen
			- Zugriffbeschränkungen (intern, extern)
			- Sicherheit (HTTPS)
			- Logs
			- Caching
	- ### Verarbeiten einer Anfrage
		- ![Bildschirmfoto 2023-08-02 um 20.55.20.png](../assets/Bildschirmfoto_2023-08-02_um_20.55.20_1691002521720_0.png)
			-
	- ### HTML Link
		- Browser lädt eine Seite vom Webserver
		- Per HTTP-GET
		- Ganze Seite wir neu geladen (neuer DOM wird erstellt)
		- ![image.png](../assets/image_1691002565385_0.png)
		- ![Bildschirmfoto 2023-08-02 um 20.56.11.png](../assets/Bildschirmfoto_2023-08-02_um_20.56.11_1691002575329_0.png)
			-
	- ### HTML Formulare
	  collapsed:: true
		- Browser lädt eine Seite vom Webserver
		- Benutzereingaben werden als Key/Value Pairs mitgesendet
		- Ganze Seite wir neu geladen
		- *method* = GET oder POST (GET ist Default)
		- *action* = URL des Request Empfängers
		- ![image.png](../assets/image_1691002621159_0.png)
		-
	- ### Fetch API
	  collapsed:: true
		- await fetch(url) ;
		- Laden von Serverresourcen mittels JS (JSON, HTML, Bilder, …)  Typischste Anwendung: CRUD Operationen bei einer Rest-API
		- Nur Teile einer Seite können neu geladen werden. Bessere UX!
		- ![image.png](../assets/image_1691002673984_0.png)
		- ### Read
			- ![image.png](../assets/image_1691002714609_0.png)
			- ![image.png](../assets/image_1691002721420_0.png)
		- ### Create
			- ![image.png](../assets/image_1691002752239_0.png)
		- ### Update und Delete
			- ![image.png](../assets/image_1691002764293_0.png)
			- ![image.png](../assets/image_1691002769317_0.png)
		-
	- ### Asynchrone Methoden
	  collapsed:: true
		- **await** darf nur in asynchronen Funktionen verwendet werden
		- Asynchrone Funktionen sind mit dem Keyword **async** markiert.
		- ![image.png](../assets/image_1691002807350_0.png)
		-
- ## Promise, await und async
  collapsed:: true
	- ### Was ist ein Callback-Funktion?
	  collapsed:: true
		- Eine **Callback-Funktion** ist eine Funktion, welche als Argument übergeben wird.
		- Beispiel:
			- *setTimeout() *startet eine **Callback-Funktion** nach 10 Millisekunden
			- ![image.png](../assets/image_1691002988948_0.png)
	- ### Threads bei JS
	  collapsed:: true
		- JS läuft standardmässig auf dem UI Thread
		- UI Thread blockiert === Browser eingefroren
		- Langanhaltende Tasks **müssen** asynchron ausgeführt werden
		- «asynchron» im Sinne von parallel, auf einem weiteren Thread
		- ![image.png](../assets/image_1691003554782_0.png)
			- Der Code zeigt, wie mit einer Endlosschleife der Browser eingefroren wird.
			-
	- ### Asynchron Funktionen
	  collapsed:: true
		- Eine **asynchrone Funktionen** wird auf einem eigenen Threads ausgeführt.
			- 1. Start asynchrone Funktion 1
			- 2. Start asynchrone Funktion 2
			- 3. Asynchrone Funktion 1 wird ausgeführt
			- 4. Asynchrone Funktion 2 wird ausgeführt
			- 5. Asynchrone Funktion 1 ist fertig
			- 6. Asynchrone Funktion 2 ist fertig
			- 7.…
		- ![image.png](../assets/image_1691003659372_0.png)
			- Eine Funktion bei JS wird durch das Keyword «async» zu einer asynchronen Funktion.
			- Der Code zeigt zwei Schreibweise einer asynchronen Funktion.
	- ### Promise
		- Asynchrone Funktionen geben ein **Promise****<T>** zurück. Dies ist ein Platzhalter für ein Versprechen, dass vielleicht erfüllt wird, vielleicht aber auch nicht.
		- Erläuterung zu Promise: https://www.w3schools.com/js/js_promise.asp
		- Erläuterung zu fetch(): https://developer.mozilla.org/en-US/docs/Web/API/fetch
		- ![image.png](../assets/image_1691003731974_0.png)
		- *promise.then**(**thenCallback**) : **Promise**<T>*
		- *promise.catch**(**catchCallback**) : **Promise**<T>*
		- *thenCallback* wird mit dem Resultat aufgerufen, falls der Code ohne Exception durchgelaufen ist.
		- *catchCallback* im Falle einer Exception.
		- ![image.png](../assets/image_1691003821605_0.png)
			- Ein Promise Objekt kennt zwei Methoden, then() und catch().  Beide Methoden geben jeweils wieder ein Promise Objekt zurück, dadurch können die Aufrufe aneinandergereiht werden.
			- Then() nimmt als Argument eine Callback-Funktion entgegen, welche im Erfolgsfall mit
			  dem Resultat der asynchronen Funktion aufgerufen wird.
			- Catch() nimmt als Argument eine Callback-Funktion entgegen, welche im Exceptionfall mit der Excption der asynchronen Funktion aufgerufen wird.