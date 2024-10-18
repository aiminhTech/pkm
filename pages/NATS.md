tags:: [[JetStream]], [[Publish-Subscribe]], [[Request-Reply]]

- https://nats.io/
- https://natsbyexample.com/
- ## NATS?
	- https://docs.nats.io/nats-concepts/what-is-nats
	- NATS is an infrastructure that allows such data exchange, segmented in the form of messages. We call this a "**message oriented middleware**".
- ## NATS Connection Deno
	- https://github.com/nats-io/nats.deno
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
- ## Features
	- [[Publish-Subscribe]]
	- [[Request-Reply]]
	- [[JetStream]] - Message Persistence
		- KV Store
		- Object Store
		- Storage Type:
			- File / Memory
		- Retention:
			- Limit / Interest / Queue
		- [[Consumer]]
		- Work-queue Stream