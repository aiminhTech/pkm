tags:: BBC

- ## Typografie
	- Whitespace ist eines der mächtigsten Werkzeuge im Design. Whitespace ist
	  id:: 64c1f8b1-758b-47de-9c0c-1fb23d01decf
	  nicht verschwendete Fläche, sondern ein wichtiges Designelement.
	- Durch Whitespace bekommt der Benutzer ein angenehmeres Gefühl, er wird nicht gleich erdrückt und findet sich schneller auf der Webseite zurecht.
	- Typografie, die Gestaltung mit Text, ist ein weiteres wichtiges Element eines
	  Webseitendesigns. Nur mit Text können übersichtliche, ansprechende Designs
	  gestaltet werden.
	- ## Gestaltung mit Text
		- ## Schriftarten
			- ### Serifenschrift
				- Vorteile:
					- Führtdas Auge in der Zeile
					- Fliesstext besser lesbar
				- Nachteile:
					- Wirkt altmodisch
					- GrosseTitel wirken verzerrt
					- Kleingedrucktes schlechter lesbar
			- ### Serifenlose Schrift
				- Vorteile:
					- Wirkt modern
					- Grosse Titel einfach lesbar
					- Kleingedrucktes besser lesbar
					- Kleine Schrift verschwimmt auf Bildschirmen weniger
				- Nachteile:
					- Fliesstext führt das Auge nicht
			- ### Font Pairing - Die Wahl der Schriftarten
				- Max. 3 Schriftarten
				- Freie Schriften
					- [fonts.google.com](https://fonts.google.com/)
				- Inspiration[](https://fonts.google.com/)
					- [fontpair.co](http://fontpair.co/)
					- [femmebot.github.io/](https://femmebot.github.io/google-type/)[google](https://femmebot.github.io/google-type/)[-type](https://femmebot.github.io/google-type/)
					- [canva.com/](https://www.canva.com/learn/the-ultimate-guide-to-font-pairing/)[learn](https://www.canva.com/learn/the-ultimate-guide-to-font-pairing/)[/](https://www.canva.com/learn/the-ultimate-guide-to-font-pairing/)[the](https://www.canva.com/learn/the-ultimate-guide-to-font-pairing/)[-ultimate-](https://www.canva.com/learn/the-ultimate-guide-to-font-pairing/)[guide](https://www.canva.com/learn/the-ultimate-guide-to-font-pairing/)[-](https://www.canva.com/learn/the-ultimate-guide-to-font-pairing/)[to](https://www.canva.com/learn/the-ultimate-guide-to-font-pairing/)[-font-pairing](https://www.canva.com/learn/the-ultimate-guide-to-font-pairing/)
			- ### Kontrast
				- Accessibility
					- [snook.ca/](https://snook.ca/technical/colour_contrast/colour.html)[technical](https://snook.ca/technical/colour_contrast/colour.html)[/](https://snook.ca/technical/colour_contrast/colour.html)[colour_contrast](https://snook.ca/technical/colour_contrast/colour.html)[/colour.html](https://snook.ca/technical/colour_contrast/colour.html)
					- [color.adobe.com/de/](https://color.adobe.com/de/create/color-contrast-analyzer)[create](https://color.adobe.com/de/create/color-contrast-analyzer)[/color-](https://color.adobe.com/de/create/color-contrast-analyzer)[contrast](https://color.adobe.com/de/create/color-contrast-analyzer)[-](https://color.adobe.com/de/create/color-contrast-analyzer)[analyzer](https://color.adobe.com/de/create/color-contrast-analyzer)
				- Farbschemata
					- [color.adobe.com](https://color.adobe.com/)
	- ## Farben
		- Trivialnamen und RGB-Code
		- **Farben haben Namen:**
			- red, yellow, orange, deeppink, lightgreen, firebrick, rebeccapurple, etc.
		- **RRGGBB:**
			- **ff1493**, **90ee90**, **b22222**
			  id:: 6641bbdf-04c2-48dc-b64a-cec337b0e9e8
		- **RGB**:
			- **f00**, **ff0**, **639**
- ## Responsive Webdesign
  collapsed:: true
	- responsive = ansprechbar, empfänglich, zugänglich, **reagierend**, ***antwortend***, responsiv
	- ## Wieso?
		- Mittlerweile werden Webseiten mehr von mobilen Geräten aufgerufen als von Desktop-Computern. Deshalb ist wichtig, dass Webseiten auf mobilen Geräten benutzerfreundlich sind.
	- ## Viewport
		- Für Benutzer sichtbare Fläche einer Webseite.
		- Im <head>-Tag
		- ```html
		  <meta name="viewport"
		  content="width=device-width, 
		  initial-scale=1.0">
		  ```
			- Eine erste Massnahme für die Implementierung von Responsive Webdesign ist, im <head>-Tag des HTML ein <meta>-Tag mit name=**"**viewport**"** hinzuzufügen.
			- width=device-width sagt, dass sich der Inhalt der Breite des Viewports anpassen soll.
			- Initial-scale=1.0 heisst 100% zoom.
	- ## Wie soll ich vorgehen, um ein Responsive Webdesign zu realisieren?
		- ### Mobile first
			- Bei der Philosophie «Mobile First» denkt man schon ganz am Anfang aus der Sicht eines
			  mobilen Benutzers und gestaltet Mockups und Design für mobile Geräte.
			- Alle Bildressourcen werden mobiltauglich zur Verfügung gestellt, damit der Mobilbenutzer nie heranzoomen muss.
			- Aus einer bestehenden Desktop-Seite eine mobile Version zu machen ist viel
			  schwieriger als von Anfang an eine mobile Version zu machen.
			- Bei «Mobile First» besteht der Nachteil, dass die Webseite nicht wirklich für
			  Desktopgeräte gemacht wird.
		- ### Media Queries
			- Je nachdem wie gross der Viewport ist, werden andere CSS-Eigenschaften aktiv.
			- Beispiel
				- ```css
				  body {
				    background-color: lightblue;
				  }
				  
				  @media screen and (min-width: 480px) {
				    body {
				      background-color: lightgreen;
				    }
				  }
				  
				  ```
			- #### Verschiedene Medien
				- Print ist, wenn man eine Webseite ausdruckt. Z.B. kann hier der Hintergrund weiss gemacht werden.
				- Speech ist für Screenreaders, welche eine Webseite vorlesen.
				- ```css
				  @media all …
				  
				  @media screen …
				    
				  @media print …
				    
				  @media speech …
				  
				  ```
		-
- ## W3C
  collapsed:: true
	- # Definition
		- **World Wide Web Consortium**
		- ist eine internamtional Gemeinschaft
		- Die Aufgabe des W3C besteht darin, das Web zu seinem vollen Potential zu führen, indem es entsprechende Protokolle und Richtlinien entwickelt.
	- # Wie halte ich W3C-Richtlinien ein?
		- HTML5: [http://validator.w3.org/](http://validator.w3.org/)
		- CSS 3: [https://jigsaw.w3.org/css-validator/#validate_by_input](https://jigsaw.w3.org/css-validator/)
	- # Wozu halte ich W3C-Richtlinien ein?
		- Cross-Browser KompatinilitätVerhindert unerwartetes
		- Verhalten einer Webseite
		- Accessibility
		-
- [[CSS]]
- [[HTML]]
- [[JavaScript]]