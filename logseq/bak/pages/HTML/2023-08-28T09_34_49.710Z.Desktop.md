- #Webdesign #BBC
- # Semantik & HTML Einführung
  collapsed:: true
	- **Semantik** (von altgr. σημαίνειν *sēmaínein*, ‚bezeichnen‘, ‚zum Zeichen gehörig‘),
	  auch **Bedeutungslehre**, nennt man die Theorie oder Wissenschaft von der Bedeutung der **Zeichen**.
	- ## Zeichen?
		- Festgelegte, mit einer bestimmten Bedeutung verknüpfte und eine ganz bestimmte Information
		  vermittelnde (grafische) Einheit.
	- ## Semantik im Zusammenhang zum Web
		- Struktur von Webseiten: Beschreibungssprache (HTML).
		- Jedes Zeichen (Tags) dieser Beschreibungssprache hat eine **Bedeutung.**
		- Je besser die Bedeutungen zugewiesen sind, desto besser können Maschinen die
		  Struktur verstehen
	- ## Semantik in einer Webseite
		- ![Bildschirmfoto 2023-07-27 um 12.11.43.png](../assets/Bildschirmfoto_2023-07-27_um_12.11.43_1690434705097_0.png)
		- Mit HTML machen wir nichts anderes als die auf einer Webseite enthaltene Information zu
		  strukturieren und den einzelnen Informationen so viel Bedeutung zu geben wie möglich.
	- ## Was ist HTML?
		- HyperText Markup Language
		- HTML ist ein Beschreibungssprache
		- Sprache zur **Strukturierung** aller Elemente einer Webseite
		- Sammlung vordefinierter Tags
		- Ermöglicht das Einbinden von Scriptsprachen
		- Plattformunabhängig
		- Zur Darstellung der Inhalte einer HTML-Datei ist eine „Rendering Engine“
		  notwendig. Dieser ist wesentlicher Bestandteil eines Web-Browsers
		- **Beispiel HTML**
			- ![Bildschirmfoto 2023-07-27 um 12.13.08.png](../assets/Bildschirmfoto_2023-07-27_um_12.13.08_1690434790865_0.png){:height 360, :width 718}
			- ![Bildschirmfoto 2023-07-27 um 12.14.10.png](../assets/Bildschirmfoto_2023-07-27_um_12.14.10_1690434853259_0.png)
- # Tags
  collapsed:: true
	- ## Heading (<h1> – <h6>)
		- ![Bildschirmfoto 2023-07-27 um 12.16.55.png](../assets/Bildschirmfoto_2023-07-27_um_12.16.55_1690435017639_0.png)
	- ## Paragraph (<p>)
		- ![Bildschirmfoto 2023-07-27 um 12.16.42.png](../assets/Bildschirmfoto_2023-07-27_um_12.16.42_1690435004673_0.png)
			-
	- ## Break (<br>)
		- ![Bildschirmfoto 2023-07-27 um 12.16.27.png](../assets/Bildschirmfoto_2023-07-27_um_12.16.27_1690434988665_0.png)
	- ## Unordered List / List Item (<ul> / <li>)
		- ![Bildschirmfoto 2023-07-27 um 12.17.47.png](../assets/Bildschirmfoto_2023-07-27_um_12.17.47_1690435069252_0.png)
	- ## Ordered List / List Item (<ol>/ <li>)
		- ![Bildschirmfoto 2023-07-27 um 12.18.26.png](../assets/Bildschirmfoto_2023-07-27_um_12.18.26_1690435108264_0.png)
	- ## Bilder (<img>)
		- Auf Bilder wird in einer späteren Präsi genauer eingegangen.
		- Kurz src und alt erklären
		- Placeholder.com bietet eine einfache Schnittstelle für generierte Platzhalter – hier ein 300x400 px grosses png (obviously) Verwendet eure Zeit für HTML, und nicht für die Bildersuche!
	- ## Links (<a>)
		- ![Bildschirmfoto 2023-07-27 um 13.52.04.png](../assets/Bildschirmfoto_2023-07-27_um_13.52.04_1690440725578_0.png)
		- ![Bildschirmfoto 2023-07-27 um 13.52.13.png](../assets/Bildschirmfoto_2023-07-27_um_13.52.13_1690440735437_0.png)
		- ![Bildschirmfoto 2023-07-27 um 13.52.25.png](../assets/Bildschirmfoto_2023-07-27_um_13.52.25_1690440751589_0.png)
		- ![Bildschirmfoto 2023-07-27 um 13.52.44.png](../assets/Bildschirmfoto_2023-07-27_um_13.52.44_1690440766196_0.png)
			- Belehrt den User nicht! Denkt an die Screen Reader und Suchmaschienen« àlink
			  zur Quelle» ist schon aussagekräftiger als «<a> klicken Sie hier </a> für die Quelle»
			- Wir können auch ein Bild oder eine Liste zum link machen. Von Vorteil simpel halten. (Bild oder Text)
			- Was soll passieren, wenn auf einen Button im Link geklickt wird?
			-
			-
- # LATER Schemantische Tags
	- ## Navigation (<nav>)
		-
	- ## Table (<table>)
		- ```css
		  
		  <tabel>
		  	<tr>
		      	<th>Firstname</th>
		          <th>Lastname</th>
		          <th>Points</th>
		      </tr>
		      <tr>
		      	<td>Firstname</tdv>
		          <td>Lastname</td>
		          <td>Points</td>
		      </tr>
		      <tr>
		      	<td>Firstname</td>
		          <td>Lastname</td>
		          <td>Points</td>
		      </tr>
		  </table>
		  ```
	-