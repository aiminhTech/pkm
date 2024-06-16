tags:: [[node.js]], [[Programming Language]]

- [[Syntax]]
- [[Data Types]]
- [[JS EventLoop]]
- [[Scope & Closure]]
-
- ## JS im Browser
  collapsed:: true
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
	  collapsed:: true
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
	  collapsed:: true
		- Liefert Dokumente an Clients aus
			- HTML-Seiten an unseren Browser
			- Dasselbe mit CSS, JavaScript, JSON und Bilder
		- Andere Funktionen
			- Zugriffbeschränkungen (intern, extern)
			- Sicherheit (HTTPS)
			- Logs
			- Caching
	- ### Verarbeiten einer Anfrage
	  collapsed:: true
		- ![Bildschirmfoto 2023-08-02 um 20.55.20.png](../assets/Bildschirmfoto_2023-08-02_um_20.55.20_1691002521720_0.png)
			-
	- ### HTML Link
	  collapsed:: true
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
		- `await fetch(url)`
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
- ## Datentypen
  collapsed:: true
	- Einfacher als bei Java
	- Es wird nicht zwischen Integer und Double unterschieden
	- ![Bildschirmfoto 2023-08-02 um 20.40.04.png](../assets/Bildschirmfoto_2023-08-02_um_20.40.04_1691001606909_0.png){:height 141, :width 524}
	- ### String
	  collapsed:: true
		- ```jsx
		  
		  let text = "John";                 // Datentyp: String
		  let text2 = text + " " + "Doe";
		  let text3 = `Hey ${text}`;	// Template String
		  let text4 = `overlay ${menu.isOpen ? "" : "hidden"}`;
		  let char = text[0]                 
		  let size = text.length;       
		  // Datentyp: Number
		  text = text.substring(2, 2) 
		  text = text.toUpperCase();
		  text = text.replace("John", "Sam");
		  
		  
		  ```
- ## Syntax
  collapsed:: true
	- **Eingebettet im HTML**:` <script>… </script>`
	- Ähnliche Syntax wie Java
	- Schwach typisiert (Keine Angaben von Datentypen im Code)
	- Semikolons sind optional
	- ![image.png](../assets/image_1691001483673_0.png){:height 567, :width 445}
		- ### Variablen
			- “**let**“ deklariert eine Variable
			- “**const**“ deklariert eine Konstante
			- “**var**“ deklariert globale Variablen und sollte nicht mehr verwendet werden
			- Variable ohne Zuweisung sind ‘**’undefined**’’
			- Falls möglich verwende “**const**“, sonst “**let**“
			- ![Bildschirmfoto 2023-08-02 um 20.39.15.png](../assets/Bildschirmfoto_2023-08-02_um_20.39.15_1691001558034_0.png)
		- ### Steuerlogik
			- ```jsx
			  
			  if (bedingung) {
			    anweisungen;
			  } else if (bedingung) {
			    anweisungen;
			  } else {
			    anweisungen;
			  }
			  
			  ```
			- ```jsx
			  switch (variable) {
			    case wert1:
			      anweisungen;
			      break;
			    case wert2:
			      anweisungen;
			      break;
			    default:
			      anweisungen;
			  }
			  ```
			- ```jsx
			  while (bedingung) {
			    anweisungen;
			    break;
			    continue;
			  }
			  do {
			    anweisungen;
			  } while (bedingung);
			  
			  ```
			- ```jsx
			  for (let schritt = 0; schritt < 5; schritt++) {
			    anweisungen;
			  }
			  ```
			- ```jsx
			  try {
			    anweisungen;
			  } catch (exception) {
			    anweisungen;
			  } finally {
			    anweisungen;
			  }
			  throw new Error("...");
			  
			  
			  ```
		- ### Vergleichsoperatoren
		  collapsed:: true
			- Vergleiche immer mit `===`
			- `==` vergleicht nur den Wert
			- `===` vergleicht den Wert und den Typ
			- ```jsx
			  let x = 10;
			  let y = "10"
			  if (x == y) { /* x ist hier gleich wie y */ }
			  if (x === y) { /* x ist hier nicht gleich wie y */ }
			  if (x != y) { }
			  if (x !== y) { }
			  
			  ```
			-
		- ### Array
		  collapsed:: true
			- ```jsx
			  
			  const cars = ["Saab", "Volvo", "BMW"];
			  cars[0] = "Audi";
			  let myCar = cars[2];
			  
			  let size = cars.length;
			  
			  cars.push("Audi"); 	// Fügt ein Element hinzu
			  let car = cars.pop(); 	// Löscht das letzte Element
			  for (let x of cars) {
			    text += x;
			  }
			  
			  cars.forEach(car => {
			    text += `<p>${car}</p>`;
			  });
			  
			  
			  ```
		- ### Klassen
		  collapsed:: true
			- JS kennt Klassen ähnlich wie Java.
			- Verwende wenn möglich **keine Klassen**, sondern **JS Objekte!**
			- ```jsx
			  
			  class Car {
			    constructor(brand) {
			      this.carname = brand;
			    }
			    present() {
			      return 'I have a ' + this.carname;
			    }
			  }
			  class Model extends Car {
			    constructor(brand, mod) {
			      super(brand);
			      this.model = mod;
			    }
			    show() {
			      return this.present() + ', it is a ' + this.model;
			    }
			  }
			  
			  mycar = new Model("Ford", "Mustang");
			  mycar.present();
			  
			  
			  ```
		- ### JS Objekt
		  collapsed:: true
			- Entspricht dem Objekt bei Java
			- Assoziatives Array (Key-Value Pairs)
			- Kapselt Daten, manchmal auch Verhalten
			- JS Objekte sind viel flexibler
			- ```jsx
			        
			    const ronald = {
			        vorname: "Ronald",
			        nachname: "Reagan",
			        männlich: true,
			        AnzahlKinder: 3,
			        Geburtsdatum: "1911-02-06",
			        Partei:
			        {
			          Name: "Republican Party",
			          Hauptsitz: "Washington, D.C.",
			          Gründungsdatum: "1854-03-20",
			          Gründungsort: "Ripon"
			        },
			        Amt: "US-Präsident"
			      };
			  
			  
			  ```
			- JS Objekte sind **dynamisch** typisiert. Attribute und Methoden können jederzeit hinzugefügt werden.
				- ```jsx
				  //beispiel1
				  const user = {
				  
				    name: "Mario",
				    login: "admin",
				     
				    getName() {
				        return this.name
				    }
				  }
				  let userName = user.name;
				  let userName = user["name"];
				  let userName = user.getName();
				  
				  
				  //beispiel2
				  user.password = "1234";
				  let userPassword = user.password;
				  user.setName = function(newName) {
				    this.name = newName;
				  }
				  user.setName("Luigi");
				  
				  
				  ```
				- Der Code zeigt, wie man bei Js Object Literals nach der Erstellung Attribute und
				  Funktionen dynamisch hinzufügen kann.
				- Das „this“-Keyword innerhalb eines Js Object Literals zeigt, wie bei Java auf die
				  Instanz.
				-
- ## Increment Operators
  collapsed:: true
	- In JavaScript, the `++count` and `count++` expressions both increment the value of the variable `count` by 1, but they do so in slightly different ways due to the position of the increment operator (`++`).
	- ### Prefix Increment `++count`
		- The variable `count` is incremented by 1 before its value is used in the expression.
		- First, the variable `count` is increased by 1.
		- Then, the new value of `count` is returned and used in the expression.
		- ```javascript
		  let count = 5;
		  let result = ++count; // count is incremented to 6, then result is assigned the value 6
		  console.log(result); // 6
		  console.log(count);  // 6
		  ```
	- ### Postfix Increment `count++`
		- The variable `count` is incremented by 1 after its value is used in the expression.
		- First, the current value of `count` is returned and used in the expression.
		- Then, the variable `count` is increased by 1.
		- ```javascript
		  let count = 5;
		  let result = count++; // result is assigned the value 5, then count is incremented to 6
		  console.log(result); // 5
		  console.log(count);  // 6
		  ```
	- ### Use Case:
		- **Using Prefix Increment in a Loop**:
			- Here, `++i` increments `i` before the condition check in each iteration.
			- ```javascript
			  for (let i = 0; i < 5; ++i) {
			    console.log(i); // Prints 0, 1, 2, 3, 4
			  }
			  ```
		- **Using Postfix Increment in a Loop**:
			- Here, `i++` increments `i` after the condition check in each iteration.
			- ```javascript
			  for (let i = 0; i < 5; i++) {
			    console.log(i); // Prints 0, 1, 2, 3, 4
			  }
			  ```H
				-
	- ### Choosing Between `++count` and `count++`:
		- Use **`++count`** if you need the incremented value immediately in the expression.
		- Use **`count++`** if you need the original value before it is incremented in the expression.
- ## Strict mode `use strict`
  collapsed:: true
	- Is a directive that helps you write more secure and error-free code by enabling strict mode.
	- When you use strict mode, it changes the way JavaScript operates in the following ways
		- **Prevents the use of undeclared variables**: You must declare all variables with `var`, `let`, or `const`. This helps avoid accidental global variables.
		- **Disallows duplicate parameter names**: You can't have function parameters with the same name, which helps prevent confusion and potential errors in your code.
		- **Throws errors for unsafe actions**: Certain actions that JavaScript normally allows, but can lead to bugs or security issues, will throw errors in strict mode. For example, assigning a value to a non-writable property or using a variable/object before declaring it.
		- **Changes in `this` behavior**: In functions, `this` will be `undefined` if the function is called without an object context, instead of defaulting to the global object (like `window` in browsers).
- ## Promise, await und async
  collapsed:: true
	- ### Was ist ein Callback-Funktion?
	  collapsed:: true
		- Eine **Callback-Funktion** ist eine Funktion, welche als Argument übergeben wird.
		- Beispiel:
			- *setTimeout() *startet eine **Callback-Funktion** nach 10 Millisekunden
			- ![image.png](../assets/image_1691002988948_0.png)
	- ### Threads bei JS
		- JS läuft standardmässig auf dem UI Thread
		- UI Thread blockiert === Browser eingefroren
		- Langanhaltende Tasks **müssen** asynchron ausgeführt werden
		- ==asynchron== im Sinne von parallel, auf einem weiteren Thread
		- Der Code zeigt, wie mit einer Endlosschleife der Browser eingefroren wird.
			- ![image.png](../assets/image_1691003554782_0.png){:height 351, :width 295}
	- ### Asynchron Funktionen
		- Eine **asynchrone Funktionen** wird auf einem eigenen Threads ausgeführt.
			- 1. Start asynchrone Funktion 1
			- 2. Start asynchrone Funktion 2
			- 3. Asynchrone Funktion 1 wird ausgeführt
			- 4. Asynchrone Funktion 2 wird ausgeführt
			- 5. Asynchrone Funktion 1 ist fertig
			- 6. Asynchrone Funktion 2 ist fertig
			- 7.…
		- ![image.png](../assets/image_1691003659372_0.png){:height 351, :width 407}
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
- ## `this` Keyword
	- The value of the `this` keyword is the global object
	- ### The value of the ==this== keyword in:
		- **Regular Functions**:  is *the object on which the function is invoked*
		- **Arrow Functions:** is *determined by the lexical environment in which the arrow function was defined*
		- **Classes:** in constructor functions or classes is *the value of the newly created instance*
		- **Event handler:** using a regular function is *the element that received the event*