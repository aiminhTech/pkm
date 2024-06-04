- https://nats.io/
- ## NATS?
	- https://docs.nats.io/nats-concepts/what-is-nats
	- NATS is an infrastructure that allows such data exchange, segmented in the form of messages. We call this a "**message oriented middleware**".
	-
- ## NATS Connection
	- ### Import deno.json
		- ```deno.json
		  "nats": "https://deno.land/x/nats@v1.18.0/src/mod.ts"
		  ```
	- ### Establish Connection
		- ```ts
		  import { ConnectionOptions, NatsConnection, ObjectStore, StorageType, connect, nanos } from "nats";
		  	
		  export let nc: NatsConnection | undefined = undefined;
		  const config: ConnectionOptions = {
		    name: "supercheck-backend",
		    servers: `${Deno.env.get("NATS_SERVICE_HOST") || "127.0.0.1"}:4222`,
		    waitOnFirstConnect: true,
		    reconnect: true,
		    maxReconnectAttempts: -1,
		  };
		  
		  
		  (async () => {
		    try {
		      console.log("connecting to NATS");
		      nc = await connect(config);
		      console.log("connected to NATS", nc.info);
		    } catch (e) {
		      console.error("error", e.message);
		    }
		  })();
		  ```
	- ## Create a store, save and load from store data example
		- ```ts
		  function objectStore(bucket: string): Promise<ObjectStore | null> {
		    return nc
		      ? nc.jetstream().views.os(bucket, { storage: StorageType.File, ttl: nanos(30_000) })
		      : Promise.resolve(null);
		  }
		  
		  export async function storeHealthcheck(
		    url: string,
		    json: string,
		  ): Promise<void> {
		    const os = await objectStore("supercheck");
		    if (os) {
		      await os.putBlob({ name: url }, new TextEncoder().encode(json));
		    }
		  }
		  
		  export async function loadHealthcheck(
		    url: string,
		  ): Promise<string | null> {
		    const os = await objectStore("supercheck");
		  
		    if (os) {
		      const blob = await os.getBlob(url)
		  
		      return blob ? new TextDecoder().decode(blob) : null
		    }
		    return null;
		  }
		   
		  ```