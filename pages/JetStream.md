tags:: [[NATS]]

- https://docs.nats.io/nats-concepts/jetstream
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
	- A *work-queue* retention policy satisfies a very common use case of queuing up messages that are intended to be processed **once and only
	  once**.