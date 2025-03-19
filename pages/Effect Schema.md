tags:: [[Effect TS]], [[Zod]], [[Quicktype]]

- https://effect.website/docs/schema/introduction/
- A library for **defining and using schemas to validate and transform data** in TypeScript.
-
- ## Learning
	- Crash Course: [https://www.youtube.com/watch?v=nQA_JsCozU4](https://www.youtube.com/watch?v=nQA_JsCozU4)
	- Compare with Zod: [https://github.com/Effect-TS/effect/blob/main/schema/comparisons.md](https://github.com/Effect-TS/effect/blob/main/schema/comparisons.md)
- ## Defining a schema
  collapsed:: true
	- https://effect.website/docs/schema/getting-started/#defining-a-schema
	- One common way to define a `Schema` is by ultilizing the `Struct` constructor. This allows to create a new schema that outlines an object with specific properties.
		- ```ts
		  const Foo = S.Struct({
		    id: S.Positive,
		    name: S.NonEmptyString.pipe(S.pattern(/.*ooo$/)),
		    url: S.URL
		  })
		  
		  type Foo = typeof Foo.Type
		  ```
-
- ## Encode
	- Encoding is the process of **transforming structured TypeScript values** into another format, often for serialization *(sending data to an API, database, or UI)*
- ## Decode
  collapsed:: true
	- Decoding is the process of **validating and transforming** input data *(user input, API repsonse*) into a strongly typed Typescript value.
	- ### decodeUnknown
		- Eine Funktion, die es ermöglicht, **beliebige unbekannte Daten (`unknown`) in ein spezifisches Schema zu dekodieren und zu validieren**
		- Daten aus externen Quellen (z. B. API-Responses oder Formulareingaben) haben oft unbekannte Typen. `decodeUnknown` nimmt ein beliebiges `unknown`-Eingangsobjekt und validiert es gegen das definierte Schema.
		- **Example**
			- ```ts
			  import Schema as S from "@effect/schema";
			  
			  // Definiere ein Schema
			  const UserSchema = S.struct({
			    id: S.number,
			    name: S.string,
			  });
			  
			  // Beispiel-JSON (z.B. API Response)
			  const input: unknown = { id: 123, name: "Alice" };
			  
			  // 3decodeUnknown aufrufen
			  const result = S.decodeUnknown(UserSchema)(input);
			  
			  console.log(result);
			  // Wenn das input den Anforderungen des Schemas entspricht, wird ein Success-Wert mit den typisierten Daten zurückgegeben.
			  /*
			  Success({ id: 123, name: "Alice" })
			  */
			  
			  -----------------------------------------------------------------------------------------------------------------------------
			  const invalidInput: unknown = { id: "foo", name: "Alice" };
			  
			  const result2 = S.decodeUnknown(UserSchema)(invalidInput);
			  
			  console.log(result2);
			  // Da id hier eine String statt einer Nummer ist, schlägt die Validierung fehl.
			  /*
			  Failure(["id must be a number"])
			  
			  ```
			-
-
-
- **Decode**:
	- Diese Operation nimmt externe Daten (wie JSON von einer API oder Benutzereingaben) und wandelt sie in ein typisiertes Format um, das Ihr TypeScript-Programm sicher verwenden kann. Sie umfasst das Parsen und Validieren der Daten gegen ein Schema, um sicherzustellen, dass sie der definierten Struktur und den Typen entsprechen.
- **Encode**:
	- Diese Operation macht das Gegenteil – sie nimmt Ihre internen typisierten Daten und wandelt sie in ein externes Format um, wie z. B. JSON, um sie an eine API zu senden oder in einer Datenbank zu speichern.
- **Filter**
	- ### Definition
	- **Validierung von Daten**: Filter in Effect Schema dienen dazu, Daten gegen bestimmte Bedingungen zu prüfen. Nur Daten, die diese Bedingungen erfüllen, werden akzeptiert.
	- **Optionale Transformation**: Bei Nichterfüllung der Bedingungen können Daten abgelehnt oder in eine gültige Form transformiert werden.
	- ### Hauptfunktionen
	- **Validierung**
		- Prüft, ob Daten bestimmte Kriterien erfüllen (z. B. ob eine Zahl in einem bestimmten Bereich liegt oder ein String ein Muster wie eine E-Mail-Adresse hat).
		- Bei Nichterfüllung werden die Daten abgelehnt oder es wird ein Fehler ausgelöst.
	- **Transformation**
		- Daten können angepasst werden, wenn sie die Bedingungen erfüllen (z. B. Runden einer Zahl).
		- Bei Nichterfüllung können Standardwerte gesetzt werden (z. B. ein Mindestalter).
	- ### Einsatzgebiete
	- **Benutzereingaben**: Sicherstellung, dass Eingaben in Formularen korrekt sind (z. B. gültige E-Mail-Adressen oder Passwörter).
	- **API-Datenverarbeitung**: Extrahieren relevanter Daten oder Filtern ungültiger Daten aus API-Antworten.
	- **Datenbereinigung**: Entfernen ungültiger oder unerwünschter Daten aus Datensätzen.
	- ### Vorteile
	- **Typsicherheit**: Durch die Integration mit Schemata wird sichergestellt, dass nur typkonforme Daten verarbeitet werden.
	- **Flexibilität**: Filter können leicht angepasst oder um neue Bedingungen erweitert werden.
	- **Wartbarkeit**: Zentrale Definition von Filtern erleichtert die Pflege und Wiederverwendung im Code.
- **Transform**
  collapsed:: true
	- **Definition**: Transformation in Effect Schema bedeutet, Daten von einem Ausgangsformat (z. B. extern) in ein Zielformat (z. B. intern) umzuwandeln, um sie an spezifische Bedürfnisse anzupassen.
	- **Hauptfunktionen**:
	- Schema.transform für sichere Transformationen ohne Fehler.
	- Schema.transformOrFail für Transformationen, die fehlschlagen können, mit Fehlerbehandlung über ParseResultund Unterstützung für asynchrone Effect-Operationen.
	- **Prozess**: Nimmt Eingabedaten, wendet Transformationsregeln an und gibt die transformierten Daten oder einen Fehler aus.
	- **Einsatzgebiete**: Typkonvertierungen (z. B. String zu Number), Datenanpassungen (z. B. Zahlen runden) und Serialisierung (z. B. JSON).
	- **Beispiele**:
		- "42" wird zu 42 (NumberFromString).
		- -5 wird zu 0 (Clamping innerhalb eines Bereichs).
		- { name: "Alice" } wird zu {"name": "Alice"} (JSON).
	- **Vorteile**: Typsicherheit, Flexibilität bei verschiedenen Transformationen und Wiederverwendbarkeit durch kombinierbare Schemata.
	- **Warum es wichtig ist**: Transformationen ermöglichen Datenkompatibilität (z. B. zwischen APIs und internen Strukturen) und vereinfachen die Verarbeitung komplexer Daten.
	- ```ts
	  import * as S from "@effect/schema/Schema";
	  import { pipe } from "@effect/data/Function";
	  import { Effect } from "effect";
	  
	  // Beispielschema mit Transformationen
	  const PersonSchema = S.struct({
	    // String → Number Transformation
	    age: pipe(
	      S.string,
	      S.transform(S.number, {
	        decode: (s) => parseInt(s, 10), // String zu Number beim Dekodieren
	        encode: (n) => n.toString()     // Number zu String beim Kodieren
	      })
	    ),
	    // Zahl mit Clamping (Bereich 0-100)
	    score: pipe(
	      S.number,
	      S.transform(S.number, {
	        decode: (n) => Math.min(Math.max(n, 0), 100), // Clamping beim Dekodieren
	        encode: (n) => n                              // Unverändert beim Kodieren
	      })
	    ),
	    // String-Feld ohne Transformation
	    name: S.string
	  });
	  
	  // Beispiel 1: Dekodieren mit Transformation
	  const decodePerson = S.decodeSync(PersonSchema);
	  const input = { age: "25", score: -10, name: "Alice" };
	  const decoded = decodePerson(input);
	  console.log("Dekodiert:", decoded);
	  // Ausgabe: { age: 25, score: 0, name: "Alice" }
	  
	  // Beispiel 2: Kodieren mit Transformation
	  const encodePerson = S.encodeSync(PersonSchema);
	  const internalData = { age: 30, score: 150, name: "Bob" };
	  const encoded = encodePerson(internalData);
	  console.log("Kodiert:", encoded);
	  // Ausgabe: { age: "30", score: 150, name: "Bob" }
	  
	  // Beispiel 3: Transformation mit Fehlerbehandlung (asynchron)
	  const TransformWithFailSchema = S.struct({
	    id: pipe(
	      S.string,
	      S.transformOrFail(S.number, {
	        decode: (s, _, ast) =>
	          isNaN(parseInt(s))
	            ? S.failure([{ kind: "Invalid", message: "Keine gültige Zahl", ast }])
	            : S.success(parseInt(s)),
	        encode: (n) => S.success(n.toString())
	      })
	    )
	  });
	  
	  const decodeWithFail = S.decode(TransformWithFailSchema);
	  const result = await Effect.runPromise(decodeWithFail({ id: "abc" }).pipe(
	    Effect.catchAll((e) => Effect.succeed(`Fehler: ${e.message}`))
	  ));
	  console.log("TransformOrFail Ergebnis:", result);
	  // Ausgabe: Fehler: Invalid: Keine gültige Zahl
	  ```
		- ### Erklärung des Codes
		- **PersonSchema**:
			- **age**: Transformiert einen String (z. B. "25") in eine Zahl (25) beim Dekodieren und zurück in einen String beim Kodieren.
			- **score**: Wendet Clamping an, sodass Werte außerhalb von 0-100 angepasst werden (z. B. -10 wird 0, 150bleibt 150 beim Kodieren unverändert).
			- **name**: Einfacher String ohne Transformation.
		- **Dekodieren**:
			- decodePerson nimmt ein Objekt mit externen Daten (z. B. "25" für age) und gibt ein typisiertes internes Objekt zurück. Der score wird auf 0 geclamped.
		- **Kodieren**:
			- encodePerson nimmt interne Daten (z. B. age: 30) und gibt sie in einem externen Format zurück (z. B. age: "30"). Clamping wirkt hier nicht rückwärts.
		- **TransformOrFail**:
			- **id**: Verwendet transformOrFail, um eine String-zu-Number-Transformation mit Fehlerbehandlung zu zeigen. Bei ungültigen Eingaben (z. B. "abc") wird ein Fehler zurückgegeben.
			- Der asynchrone Effect-Fluss zeigt, wie Fehler elegant gehandhabt werden können
	-
- **parsejson**
	- Hier ist die Erklärung der Mindmap zu **parseJson** in **Effect Schema**, die ich zuvor erstellt habe. Ich werde jeden Abschnitt der Mindmap Schritt für Schritt durchgehen und beschreiben, was er bedeutet und warum er wichtig ist. Die Mindmap selbst ist eine strukturierte Übersicht darüber, wie `parseJson` in Effect Schema funktioniert, und diese Erklärung hilft, sie zu verstehen.
	  
	  ---
	- ### Mindmap: parseJson in Effect Schema
	  
	  ```
	  Effect Schema: parseJson
	  ├── Definition
	  │   ├── Was es macht: Wandelt einen JSON-String in ein typisiertes Objekt um
	  │   └── Ziel: JSON-Daten parsen und mit einem Schema validieren
	  │
	  ├── Hauptfunktionen
	  │   ├── Transformation
	  │   │   ├── Verwendet JSON.parse für Dekodierung
	  │   │   └── Verwendet JSON.stringify für Kodierung
	  │   ├── Validierung
	  │   │   └── Prüft die geparsten Daten gegen ein definiertes Schema
	  │
	  ├── Prozess
	  │   ├── Eingabe: JSON-String (z. B. '{"name": "Alice"}')
	  │   ├── Dekodierung
	  │   │   ├── JSON.parse → Rohdaten
	  │   │   └── Schema-Validierung → Typisierte Daten
	  │   ├── Kodierung
	  │   │   ├── Typisierte Daten → Rohdaten
	  │   │   └── JSON.stringify → JSON-String
	  │   ├── Ausgabe
	  │   │   ├── Erfolg: Typisiertes Objekt
	  │   │   └── Fehler: ParseError bei ungültigem JSON oder Schema-Verstoß
	  │
	  ├── Einsatzgebiete
	  │   ├── API-Antworten: JSON-Daten von Servern parsen
	  │   ├── Konfigurationsdateien: JSON-basierte Einstellungen laden
	  │   └── Datenübertragung: JSON zwischen Systemen austauschen
	  │
	  ├── Beispiel
	  │   ├── Schema: { name: string }
	  │   ├── Eingabe: '{"name": "Alice"}'
	  │   ├── Prozess: JSON.parse + Validierung
	  │   └── Ausgabe: { name: "Alice" } oder Fehler
	  │
	  ├── Vorteile
	  │   ├── Typsicherheit: Ergebnisse sind schema-konform
	  │   ├── Fehlerbehandlung: Klare Fehlermeldungen bei ungültigem JSON
	  │   └── Einfachheit: Kombiniert Parsing und Validierung in einem Schritt
	  │
	  └── Warum es wichtig ist
	    ├── Zuverlässigkeit: Sichert korrekte JSON-Verarbeitung
	    └── Effizienz: Vereinfacht den Umgang mit JSON-Daten
	  ```
	  
	  ---
	- ### Erklärung der Mindmap-Abschnitte
	  
	  1. **Definition**
		- **Was es macht**: `parseJson` nimmt einen JSON-String (z. B. `{"name": "Alice"}`) und wandelt ihn in ein typisiertes JavaScript/TypeScript-Objekt um (z. B. `{ name: "Alice" }`).
		- **Ziel**: Es parst den JSON-String und stellt sicher, dass die Daten mit einem vorgegebenen Schema übereinstimmen, z. B. dass `name` ein String ist.
		- **Warum wichtig**: Ohne diese Funktion müsstest du JSON manuell parsen und validieren, was fehleranfällig ist. `parseJson` macht das sicher und automatisiert.
		  
		  2. **Hauptfunktionen**
		- **Transformation**:
			- **JSON.parse**: Wird verwendet, um den JSON-String beim Dekodieren in ein Rohobjekt umzuwandeln.
			- **JSON.stringify**: Wird verwendet, um ein typisiertes Objekt beim Kodieren zurück in einen JSON-String zu transformieren.
		- **Validierung**: Nach dem Parsen prüft Effect Schema, ob die Daten dem Schema entsprechen (z. B. korrekte Typen, erforderliche Felder).
		- **Warum wichtig**: Diese Kombination aus Transformation und Validierung sorgt dafür, dass die Daten nicht nur geparst, sondern auch korrekt sind.
		  
		  3. **Prozess**
		- **Eingabe**: Ein JSON-String, z. B. `{"name": "Alice"}`.
		- **Dekodierung**:
			- **JSON.parse → Rohdaten**: Der String wird in ein JavaScript-Objekt umgewandelt.
			- **Schema-Validierung → Typisierte Daten**: Das Objekt wird gegen das Schema geprüft (z. B. ist `name` ein String?).
		- **Kodierung**:
			- **Typisierte Daten → Rohdaten**: Das validierte Objekt bleibt unverändert (oder wird angepasst, falls das Schema das verlangt).
			- **JSON.stringify → JSON-String**: Das Objekt wird wieder in einen JSON-String umgewandelt.
		- **Ausgabe**: Entweder ein typisiertes Objekt (Erfolg) oder ein `ParseError` (Fehler), wenn der JSON-String ungültig ist oder das Schema nicht erfüllt.
		- **Warum wichtig**: Dieser Prozess zeigt, wie `parseJson` Daten sicher zwischen Formaten hin- und her bewegt.
		  
		  4. **Einsatzgebiete**
		- **API-Antworten**: JSON von Servern (z. B. REST-APIs) wird oft als String geliefert und muss in typisierte Daten umgewandelt werden.
		- **Konfigurationsdateien**: JSON-Dateien mit Einstellungen können geladen und validiert werden.
		- **Datenübertragung**: JSON-Strings werden zwischen Systemen gesendet und empfangen.
		- **Warum wichtig**: Diese Szenarien sind alltäglich in der Softwareentwicklung, und `parseJson` erleichtert sie.
		  
		  5. **Beispiel**
		- **Schema**: `{ name: string }` – ein einfaches Schema, das erwartet, dass `name` ein String ist.
		- **Eingabe**: `{"name": "Alice"}` – ein JSON-String.
		- **Prozess**: Der String wird mit `JSON.parse` zu `{ name: "Alice" }` umgewandelt und gegen das Schema geprüft.
		- **Ausgabe**: `{ name: "Alice" }` (als typisiertes Objekt) oder ein Fehler, wenn z. B. `name` fehlt oder kein String ist.
		- **Warum wichtig**: Das Beispiel macht den Ablauf konkret und zeigt, wie einfach es ist, JSON zu handhaben.
		  
		  6. **Vorteile**
		- **Typsicherheit**: Das Ergebnis entspricht dem Schema, sodass TypeScript den Typ kennt und Fehler im Code vermeidet.
		- **Fehlerbehandlung**: Bei ungültigem JSON oder Schema-Verstoß gibt es klare Fehlermeldungen (z. B. "Expected string, got number").
		- **Einfachheit**: Parsing und Validierung werden in einem Schritt erledigt, statt in separaten Operationen.
		- **Warum wichtig**: Diese Vorteile sparen Zeit und machen den Code robuster.
		  
		  7. **Warum es wichtig ist**
		- **Zuverlässigkeit**: `parseJson` stellt sicher, dass JSON-Daten korrekt verarbeitet werden, ohne dass man sich auf manuelle Checks verlassen muss.
		- **Effizienz**: Es reduziert den Aufwand für Entwickler, indem es gängige Aufgaben automatisiert.
		- **Warum wichtig**: In einer Welt, in der JSON überall verwendet wird (APIs, Datenbanken, etc.), ist eine zuverlässige und effiziente Handhabung essenziell.
		  
		  ---
	- ### Zusammenfassung
	  Die Mindmap beschreibt `parseJson` als eine Transformation, die JSON-Strings in typisierte Objekte umwandelt und umgekehrt, mit integrierter Validierung. Sie zeigt den Prozess, Einsatzgebiete, Vorteile und ein Beispiel, um zu verdeutlichen, wie nützlich und praktisch diese Funktion in Effect Schema ist. Jeder Abschnitt baut auf dem vorherigen auf, um ein vollständiges Bild zu zeichnen.
-
-
- compose
	- ### Erklärung der Mindmap
	- **Definition**
		- **Was es macht**: compose nimmt zwei Schemata (z. B. A und B) und erstellt ein neues Schema, das Daten von der Eingabe von A zur Ausgabe von B transformiert.
		- **Ziel**: Es erlaubt, mehrere Transformations- oder Validierungsschritte in einer Kette auszuführen.
	- **Hauptfunktionen**
		- **Schema.compose**: Verbindet zwei Schemata, wobei die Ausgabe des ersten Schemas (A) die Eingabe des zweiten Schemas (B) wird.
	-
	- **Eigenschaften**:
		- Dekodierung geht von A nach B.
		- Kodierung geht von B zurück nach A.
	- **Prozess**
	- **Eingabe**: Daten, die dem ersten Schema entsprechen.
	- **Transformation**:
		- Schritt 1: Daten werden mit Schema A verarbeitet.
		- Schritt 2: Ergebnis wird mit Schema B verarbeitet.
	- **Ausgabe**: Typisierte Daten gemäß Schema B oder ein Fehler, wenn ein Schritt fehlschlägt.
	- **Einsatzgebiete**
	- **Typkonvertierung**: Mehrere Typänderungen nacheinander (z. B. String → Number → BigInt).
	- **Datenanpassung**: Kombination von Validierung und Transformation.
	- **Pipeline**: Aufbau komplexer Datenverarbeitungsketten.
	- **Beispiel**
	- **Schema A**: Wandelt String in Number um.
	- **Schema B**: Wandelt Number in BigInt um.
	- **Eingabe**: "123" → 123 → 123n.
	- **Vorteile**
	- **Modularität**: Einzelne Schemata können unabhängig definiert und wiederverwendet werden.
	- **Typsicherheit**: TypeScript erkennt die Typen durchgehend.
	- **Lesbarkeit**: Der Code bleibt übersichtlich, da die Schritte klar verkettet sind.
-
-
- instanceof
	- **instanceOf**
	- **Definition**: S.instanceOf erstellt ein Schema, das prüft, ob ein Wert eine Instanz einer bestimmten Klasse ist (z. B. Date, Error).
	- **Hauptfunktionen**: Nutzt den instanceof-Operator, um bei der Dekodierung zu validieren.
	- **Prozess**: Prüft, ob die Eingabe eine Instanz ist; gibt sie zurück oder löst einen Fehler aus.
	- **Einsatzgebiete**: Nützlich für Objekte wie Date oder benutzerdefinierte Klassen.
	- **Beispiel**: S.instanceOf(Date) akzeptiert nur Date-Instanzen.
	- **declare**
	- **Definition**: S.declare erlaubt es, Schemata für Typen zu definieren, deren Validierung oder Transformation manuell angegeben wird.
	- **Hauptfunktionen**: Flexibles Werkzeug für Typaliase, externe Typen oder komplexe Logik.
	- **Prozess**: Validierung wird durch benutzerdefinierte Funktionen gesteuert.
	- **Einsatzgebiete**: Ideal für rekursive Typen, externe Bibliotheken oder spezielle Bedingungen.
	- **Beispiel**: Ein Schema für positive Zahlen.
-
-
- redacted
	- ### Erklärung der Mindmap
	- **Definition**
		- **Was es macht**: "Redacted" bedeutet hier, sensible Daten zu maskieren oder zu entfernen (z. B. Passwörter zu *** zu ändern).
		- **Ziel**: Schutz von Privatsphäre oder Verhinderung von Datenlecks.
	- **Hauptfunktionen**
		- **Transformation**: Mit S.transform können Daten beim Kodieren geändert werden.
		- **Benutzerdefinierte Logik**: Mit S.declare kann man spezifische Regeln für das Redacten definieren.
	- **Prozess**
		- **Eingabe**: Originaldaten, z. B. ein Passwort.
		- **Redact-Schritt**: Beim Dekodieren bleiben die Daten intakt, beim Kodieren werden sie maskiert.
		- **Ausgabe**: Maskierte Daten oder Fehler bei ungültiger Eingabe.
	- **Einsatzgebiete**
		- **Logs**: Sensible Daten in Protokollen verbergen.
		- **APIs**: Daten vor dem Senden maskieren.
		- **Debugging**: Daten sicher anzeigen.
	- ```ts
	  import * as S from "@effect/schema/Schema";
	  import { pipe } from "@effect/data/Function";
	  
	  // Schema für ein Benutzerobjekt mit redactetem Passwort
	  const UserSchema = S.struct({
	    username: S.string,
	    password: pipe(
	      S.string,
	      S.transform(S.string, {
	        decode: (s) => s,           // Beim Dekodieren: Originalwert bleibt
	        encode: () => "***"        // Beim Kodieren: Maskieren mit "***"
	      })
	    )
	  });
	  
	  // Beispiel 1: Dekodieren (Originaldaten bleiben)
	  const decodeUser = S.decodeSync(UserSchema);
	  const input = { username: "alice", password: "secret123" };
	  const decoded = decodeUser(input);
	  console.log("Dekodiert:", decoded);
	  // Ausgabe: { username: "alice", password: "secret123" }
	  
	  // Beispiel 2: Kodieren (Passwort wird maskiert)
	  const encodeUser = S.encodeSync(UserSchema);
	  const user = { username: "bob", password: "mypassword" };
	  const encoded = encodeUser(user);
	  console.log("Kodiert:", encoded);
	  // Ausgabe: { username: "bob", password: "***" }
	  
	  // Beispiel 3: Kombination mit Validierung
	  const SecureUserSchema = S.struct({
	    username: S.string,
	    password: pipe(
	      S.string,
	      S.minLength(8, { message: "Passwort muss mindestens 8 Zeichen haben" }),
	      S.transform(S.string, {
	        decode: (s) => s,
	        encode: () => "***"
	      })
	    )
	  });
	  
	  const decodeSecureUser = S.decodeSync(SecureUserSchema);
	  try {
	    const secureUser = decodeSecureUser({ username: "charlie", password: "short" });
	    console.log("Secure Dekodiert:", secureUser);
	  } catch (e) {
	    console.log("Fehler:", e.message);
	  }
	  // Ausgabe: Fehler: Passwort muss mindestens 8 Zeichen haben
	  
	  const validSecureUser = { username: "dave", password: "longpassword" };
	  const encodedSecure = encodeUser(validSecureUser);
	  console.log("Secure Kodiert:", encodedSecure);
	  // Ausgabe: { username: "dave", password: "***" }
	  ```
-
-
- brand
- **Definition**
- **Was es macht**: Ein Branded Type fügt einem Basis-Typ (z. B. string) eine Markierung hinzu, um ihn eindeutig zu machen (z. B. Email).
- **Ziel**: Verhindert, dass ähnliche Typen (z. B. string und string) verwechselt werden.
- **Hauptfunktionen**
- **S.brand**: Markiert ein Schema mit einem Brand und kann mit Validierungsregeln kombiniert werden.
- **Validierung**: Stellt sicher, dass der Wert die Bedingungen des Brands erfüllt.
- **Typsicherheit**: TypeScript behandelt den gebrandeten Typ als eigenständig.
- **Prozess**
- **Eingabe**: Ein Wert des Basis-Typs.
- **Validierung**: Prüfung der Brand-Bedingung (z. B. enthält @ für Email).
- **Ausgabe**: Der Wert als gebrandeter Typ oder ein Fehler.
- **Einsatzgebiete**
- **Domänenmodellierung**: Typen wie Email, UserId, PositiveNumber.
- **Sicherheit**: Verhindert, dass ein string fälschlicherweise als Email verwendet wird.
- **API**: Typsichere Datenverarbeitung.
- **Beispiel**
- Ein string wird als Email gebrandet, wenn er ein @ enthält.
- ```ts
  import * as S from "@effect/schema/Schema";
  import { pipe } from "@effect/data/Function";
  
  // Brand für Email
  const Email = S.brand("Email")(
    pipe(
      S.string,
      S.filter((s) => s.includes("@"), { message: "Muss eine gültige E-Mail sein" })
    )
  );
  
  // Brand für PositiveNumber
  const PositiveNumber = S.brand("PositiveNumber")(
    pipe(
      S.number,
      S.greaterThan(0, { message: "Muss positiv sein" })
    )
  );
  
  // Schema mit gebrandeten Typen
  const UserSchema = S.struct({
    email: Email,
    age: PositiveNumber
  });
  
  // Beispiel 1: Dekodieren mit gültigen Daten
  const decodeUser = S.decodeSync(UserSchema);
  const validInput = { email: "user@example.com", age: 25 };
  const decoded = decodeUser(validInput);
  console.log("Dekodiert:", decoded);
  // Ausgabe: { email: "user@example.com", age: 25 }
  
  // Beispiel 2: Fehler bei ungültiger E-Mail
  try {
    decodeUser({ email: "invalid", age: 30 });
  } catch (e) {
    console.log("Fehler bei Email:", e.message);
  }
  // Ausgabe: Fehler: Muss eine gültige E-Mail sein
  
  // Beispiel 3: Fehler bei negativer Zahl
  try {
    decodeUser({ email: "test@example.com", age: -5 });
  } catch (e) {
    console.log("Fehler bei Age:", e.message);
  }
  // Ausgabe: Fehler: Muss positiv sein
  
  // Typsicherheit demonstrieren
  type User = S.Schema.To<typeof UserSchema>;
  // User ist { email: string & { [S.Brand]: "Email" }, age: number & { [S.Brand]: "PositiveNumber" } }
  
  // Funktion, die nur Email akzeptiert
  function sendEmail(email: S.Schema.To<typeof Email>) {
    console.log("Sende Email an:", email);
  }
  
  sendEmail("user@example.com"); // Funktioniert
  // sendEmail("invalid"); // TypeScript-Fehler: Nicht kompatibel mit Email-Brand
  ```