tags:: [[VueUse]]

- https://vueuse.org/core/useWebSocket/#usewebsocket
- ## Installation
	- ```package.json
	  bun add @vueuse/core
	  ```
-
- ## Usage (Example)
	- ```typescript
	  const { send, data, close, ws, status } = useWebSocket(src, {
	      autoReconnect: true,
	  
	      onConnected(ws) {
	        started.value = true
	        console.log("connected")
	      },
	      onDisconnected(ws, event) {
	        console.log("disconnected", event)
	      },
	      onError(ws, event) {
	        console.log("error", event)
	      },
	  
	      async onMessage(ws, event) {
	        RPC_LOGGING && console.log(event);
	  
	        const res = decodeResponse(new Uint8Array(await (event.data as Blob).arrayBuffer()))
	        const id = getID(res)
	  
	        if (id) {
	          const error = getError(res)
	  
	          if (error) {
	            promises.reject(id, res)
	          } else {
	            promises.resolve(id, res)
	          }
	        } else {
	          console.warn("receive message without promise id", res);
	        }
	      },
	    })
	  ```