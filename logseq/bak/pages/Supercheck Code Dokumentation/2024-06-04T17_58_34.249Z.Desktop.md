tags:: [[LRN-221 Supercheck Verbesserung RPC]]

- ## Backend
	- ### `messaging.ts`
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
		- Der Zweck ist es, eine abstrakte Struktur bereitzustellen, um RPC-Request über Messaging-Systeme #NATS zu senden und zu empfangen
		- ```ts
		  
		  class RPCMessagingPublisher implements RPCRequestHandler {
		    // Nimmt eine RPCRequest entgegen, kodiert diese und ruft dann `executeEncoded` 
		    // auf, um die Anfrage zu versenden.
		    execute<T extends RPCValue = RPCValue>(req: RPCRequest): 
		    Promise<RPCResponse<T, string>> {
		      return this.executeEncoded(encodeRequest(req))
		    }
		  
		    // nimmt eine bereits kodierte Anfrage entgegen, sendet sie über ein 
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