tags:: [[LRN-221 Supercheck Verbesserung RPC]]

- ## Backend
	- ### `messaging.ts`
	  collapsed:: true
		- Der Zweck des gegebenen Codes ist die Verbindung zu einem NATS-Server 
		  herzustellen
		- ```ts
		  import { delay } from "std/async/delay.ts";
		  import { ConnectionOptions, NatsConnection, connect } from "nats";
		  
		  // Konfiguration  für die Verbindung definiert
		  let nc: NatsConnection | undefined = undefined;
		  const config: ConnectionOptions = {
		    name: "supercheck-backend",
		    servers: `${Deno.env.get("NATS_SERVICE_HOST") || "127.0.0.1"}:4222`,
		    waitOnFirstConnect: true,
		    reconnect: true,
		    maxReconnectAttempts: -1,
		  };
		  
		  // Eine Verbindung herstellt und darauf wartet, dass die Verbindung 
		  aufgebaut wird
		  (async () => {
		    try {
		      console.log("connecting to NATS");
		      nc = await connect(config);
		      console.log("connected to NATS", nc.info);
		    } catch (e) {
		      console.error("error", e.message);
		    }
		  })();
		  
		  
		  // Stellt sicher, dass die Verbindung bereit ist, bevor sie zurückgegeben wird.
		  // Wenn `nc` undefined ist, wird die Funktion solange warten, bis eine 
		  // gültige Verbindung zu einem NATS-Server hergestellt wurde, bevor sie diese 
		  // Verbindung zurückgibt.
		  export const ncOrWait = async (): Promise<NatsConnection> => {
		    while (nc === undefined) {
		      console.log("nats connection not ready, sleeping");
		      await delay(1000)
		    }
		    return nc
		  }
		  
		  ```
	- ### `rpc_messaging`
	  collapsed:: true
		- Der Zweck ist es, eine abstrakte Struktur bereitzustellen, um RPC-Request über Messaging-Systeme #NATS zu senden und zu empfangen
		- ```ts
		  
		  class RPCMessagingPublisher implements RPCRequestHandler {
		    // Nimmt eine RPCRequest entgegen, kodiert diese und ruft dann `executeEncoded` 
		    // auf, um die Anfrage zu versenden.
		    execute<T extends RPCValue = RPCValue>(req: RPCRequest): 
		    Promise<RPCResponse<T, string>> {
		      return this.executeEncoded(encodeRequest(req))
		    }
		    
		    
		  
		    // Nimmt eine bereits kodierte Anfrage entgegen, sendet sie über ein 
		    // Messaging-System (hier als "nc" referenziert) mit einem Zeitlimit von 
		    // 90 Sekunden und decodiert die Antwort.
		    async executeEncoded<T extends RPCValue = RPCValue>(req: Uint8Array): 
		    Promise<RPCResponse<T, string>> {
		      try {
		        const nc = await ncOrWait()
		        const result = await nc.request("foo", req, { timeout: 90_000 })
		        const decoded = decodeResponse<T>(result.data)
		        return decoded
		      } catch (e) {
		        console.log(e);
		  
		        return [{ error: true, id: getID(decodeRequest(req))! }, e.message]
		      }
		    }
		  }
		  
		  
		  
		  //  Erstellt eine Instanz der `RPCMessagingPublisher`-Klasse
		  export const publisher = new RPCMessagingPublisher()
		  
		  
		  
		  // Nimmt eine spezifische Parameter entgegen und erstellt eine Anfrage, 
		  // sendet sie über den `publisher` und parse dann die Antwort basierend auf 
		  // der Spezifikation (.
		  export const execute = async <P extends RPCValue, R extends RPCValue 
		  = RPCValue>(spec: RPCSpec<P, R>, params: P): Promise<R> => {
		    const id = ulid()
		    const req: RPCRequest = [{ id }, spec.name, params]
		    console.log(req);
		  
		    const res: RPCResponse<R, string> = await publisher.execute(req)
		    return spec.returnParser(res[1])
		  }
		  ```
		-
	- ### `rpc.ts`
	  collapsed:: true
		- In diesem TypeScript-Code werden Enums (Enumerationen) verwendet, um symbolische Namen für bestimmte, klar definierte Werte zu erstellen. Das hilft dabei, den Code übersichtlicher und lesbarer zu gestalten. Insbesondere dienen die Enums hier folgenden Zwecken:
		  
		  1. **`RPCMessageElementIdx` Enum:**
		     ```typescript
		     export enum RPCMessageElementIdx {
		       TYPE = 0,
		       META = 1,
		     }
		     ```
			- **Beschreibung:** Definiert Indizes zur Kennzeichnung der Position von Elementen innerhalb einer RPC-Nachricht (Remote Procedure Call). `TYPE` (0) steht für den Nachrichtentyp und `META` (1) für die Metadaten.
			  
			  2. **`RPCRequestElementIdx` Enum:**
			  ```typescript
			  export enum RPCRequestElementIdx {
			  TYPE = RPCMessageElementIdx.TYPE,
			  META = RPCMessageElementIdx.META,
			  METHOD_NAME = 2,
			  FIRST_PARAM = 3
			  }
			  ```
			- **Beschreibung:** Erweiterung des `RPCMessageElementIdx` Enums, um zusätzliche Indizes für spezifische Elemente von RPC-Anfragen hinzuzufügen. `METHOD_NAME` (2) steht für den Methodennamen und `FIRST_PARAM` (3) für den ersten Parameter der Anfrage.
			  
			  3. **`RPCResponseElementIdx` Enum:**
			  ```typescript
			  export enum RPCResponseElementIdx {
			  TYPE = RPCMessageElementIdx.TYPE,
			  META = RPCMessageElementIdx.META,
			  DATA_OR_ERROR = 2
			  }
			  ```
			- **Beschreibung:** Erweiterung des `RPCMessageElementIdx` Enums für spezifische Elemente von RPC-Antworten. `DATA_OR_ERROR` (2) steht für die Daten oder Fehlerinformationen in der Antwort.
			  
			  **Zusammenfassend:** Diese Enums helfen dabei, fixierte Positionen in strukturierten Arrays für RPC-Nachrichten (sowohl Anfragen als auch Antworten) zu referenzieren. Dadurch wird es einfacher und sicherer, auf die einzelnen Elemente innerhalb dieser Arrays zuzugreifen.
			  
			  **Confidence Level:** High
			  
			  **Quellen:**
		- Offizielle TypeScript-Dokumentation: [TypeScript Enums](https://www.typescriptlang.org/docs/handbook/enums.html)
		- Die Funktionen `request` und `response` dienen dazu, spezifische Typen von RPC-Nachrichten zu erzeugen: Anfragen und Antworten. Sie vereinfachen den Prozess der Erstellung dieser Nachrichten, indem sie Standardstrukturen festlegen.
		- ### `request` Funktion
		  ```typescript
		  export function request(meta: RPCRequestMeta, methodName: RPCRequestMethod, ...params: RPCValue[]): RPCRequest {
		  return [RPCMessageType.REQUEST, meta, methodName, ...params]
		  }
		  ```
		- **Beschreibung:** Diese Funktion erstellt eine RPC-Anfrage.
		- **Parameter:**
			- `meta`: Metadaten der Anfrage vom Typ `RPCRequestMeta`.
			- `methodName`: Der Name der Methode, die aufgerufen werden soll, vom Typ `RPCRequestMethod`.
			- `...params`: Beliebig viele zusätzliche Parameter der Anfrage vom Typ `RPCValue[]`.
		- **Rückgabewert:** Liefert ein Array vom Typ `RPCRequest`, welches die Anfrage repräsentiert.
		- ### `response` Funktion
		  ```typescript
		  export function response<T extends RPCValue = RPCValue>(data: T, meta: RPCResponseMeta = {}): RPCResponse<T, never> {
		  return [RPCMessageType.RESPONSE, meta, data]
		  }
		  ```
		- **Beschreibung:** Diese Funktion erstellt eine RPC-Antwort.
		- **Parameter:**
			- `data`: Die Antwortdaten vom generischen Typ `T`, welcher standardmäßig `RPCValue` ist.
			- `meta`: Optionale Metadaten der Antwort vom Typ `RPCResponseMeta`.
		- **Rückgabewert:** Liefert ein Array vom Typ `RPCResponse<T, never>`, welches die Antwort repräsentiert.
		- ### Zweck und Nutzen
		  1. **Strukturierte Erstellung:**
		   Beide Funktionen stellen sicher, dass die erstellten Nachrichten den erwarteten Strukturen entsprechen. So wird das Risiko von Formatierungsfehlern reduziert.
		  
		  2. **Klarheit und Lesbarkeit:**
		   Durch die Verwendung dieser Funktionen wird der Code klarer und weniger fehleranfällig, da Entwickler auf einfache Weise korrekte RPC-Nachrichten erstellen können, ohne sich um die genaue Anordnung der Elemente kümmern zu müssen.
		  
		  3. **Typensicherheit:**
		   Mit TypeScript-Typen und Generics wird sichergestellt, dass die Nachrichten die richtigen Datentypen enthalten. Das vereinfacht die Fehlersuche und verbessert die Kompatibilität zwischen verschiedenen Teilen der Anwendung.
		  
		  **Confidence Level:** High
		  
		  **Quellen:**
		- Offizielle TypeScript-Dokumentation: [TypeScript Functions](https://www.typescriptlang.org/docs/handbook/functions.html)
		- [Using Generics in TypeScript Functions](https://www.typescriptlang.org/docs/handbook/2/generics.html)
	- ### `store.ts`
		- ```ts §
		  export async function storeRPCRequest(
		    req: Uint8Array | RPCRequest,
		  ): Promise<string> {
		    const os = await objectStore("supercheck_rpc", rpcStoreTTLNanos); // Initialisiert den Objekt-Store
		    
		    const decoded = ArrayBuffer.isView(req) ? decodeRequest(req) : req; // Dekodiert die Anfrage, wenn sie ein Uint8Array ist
		    
		    // Generiert einen Hash basierend auf dem Methodennamen und dem ersten Parameter
		    const hash = await hashMethodNameAndParams(decoded[RPCRequestElementIdx.METHOD_NAME], decoded[RPCRequestElementIdx.FIRST_PARAM]); 
		    
		    // Speichert den ersten Parameter der Anfrage blob mit dem Namen `req_${hash}`
		    await os.putBlob({ name: `req_${hash}` }, encode(decoded[RPCRequestElementIdx.FIRST_PARAM])); 
		    return hash; // Gibt den Hash zurück
		  }
		  
		  ```
		- ```
	- ##
	-