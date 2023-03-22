- JS wird vom Browser ausgeführt
	- beim Laden von [[<script>]] tags in [[HTML]]
	- beim Laden von externen JS-Dateien
	- bei Browserevents (Maus, Tastatur, Touch,...)
- ## Globaler Kontext
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
- ## DOM (Document Object Model)
	- bezeichnet die HTML Baustruktur
	- document beitet Zugriff auf das DOM
	- HTML und CSS können beliebig verändert werden
	- ![image.png](../assets/image_1674812848475_0.png)
	-
-