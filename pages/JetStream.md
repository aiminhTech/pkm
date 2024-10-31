tags:: [[NATS]]

- https://docs.nats.io/nats-concepts/jetstream
- https://nats-io.github.io/nats.deno/ #Deno
- **Message Persistence**
- Allows for **persistent messaging** , **storing** and **replaying previously published messages**.
- This feature enhances NATS messaging by adding message durability and high availability to the system.
- ## Object Store
  collapsed:: true
	- ```ts
	  // Function to create an os
	  // ttl: nanos
	  function objectStore(bucket: string): Promise<ObjectStore | null> {
	    return nc
	      ? nc.jetstream().views.os(bucket, { storage: StorageType.File, ttl: nanos(30_000) })
	      : Promise.resolve(null);
	  }
	  
	  
	  // Function to store data 
	  export async function storeHealthcheck(
	    url: string,
	    json: string,
	  ): Promise<void> {
	    const os = await objectStore("supercheck");
	    if (os) {
	      await os.putBlob({ name: url }, new TextEncoder().encode(json));
	    }
	  }
	  
	  //Function to load data
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
- ## KV Store
  id:: 6641e504-c40c-42f2-a48f-0d2d2ea1c7bf
  collapsed:: true
	- ```ts
	  const kvStoreTTLNanos = Number(Deno.env.get("SUPERCHECK_NATS_KV_TTL_SECS") || "86400") * 1000
	  
	  // Function to create a kvs
	  //ttl : ms
	  function kvStore(bucket: string): Promise<KV | null> {
	    return nc
	      ? nc.jetstream().views.kv(bucket, { storage: StorageType.File, ttl: kvStoreTTLNanos })
	      : Promise.resolve(null);
	  }
	  
	  // Function to store data 
	  export async function storeKV(
	    key: string,
	    value: string,
	  ): Promise<void> {
	    const os = await kvStore("supercheck_kv");
	    if (os) {
	      await os.put(key, value);
	    }
	  }
	  
	  //Function to load data
	  export async function loadKV(
	    key: string,
	  ): Promise<Record<string, string> | null> {
	    const kv = await kvStore("supercheck_kv");
	  
	    if (kv) {
	      const val = await kv.get(key)
	  
	      return val ? { key, val: val.string() } : null
	    }
	    return null;
	  }
	  
	  ```
- ## Work-queue Stream
	- https://natsbyexample.com/examples/jetstream/workqueue-stream/deno
	- A *work-queue* retention policy satisfies a very common use case of queuing up messages that are intended to be processed **once and only
	  once**.
	-
- ## Stream
	- **`consumer.fetch()`**:
		- **Batch Processing**: This method is typically used to retrieve a fixed number of messages in a single batch from a stream.
		- **Blocking Call**: It waits (blocks) until the specified number of messages are fetched, or a timeout occurs.
		- **Control**: Provides more control over when and how 
		  many messages are retrieved at one time, which can be useful for batch 
		  processing scenarios.
		- **Use Case**: Suitable when you want to process messages in chunks and manage backpressure manually.
	- **`consumer.consume()`**:
		- **Continuous Processing**: This method starts a continuous stream of messages and often runs in a loop.
		- **Event-Driven**: You usually set up a callback function to handle every incoming message as it arrives.
		- **Efficiency**: More suited to applications that need to process messages as soon as they are available.
		- **Use Case**: Ideal for real-time processing or when consuming messages in a long-running process.