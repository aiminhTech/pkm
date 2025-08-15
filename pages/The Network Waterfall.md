tags:: [[Chrome]], [[Chrome Developer Tools]]

- Is a tool used by web developers to visualize and analyze how a web page's resources are loaded over the network. It’s part of the **browser’s developer tools**, typically found under the **Network tab**.
- The Network Waterfall breaks down **each request** made by a web page, showing:
  | Info | Description |
  | ---- | ---- | ---- |
  | **URL** | The resource being requested (e.g. HTML, CSS, JS, images, fonts). |
  | **Status** | HTTP status code (e.g. 200, 404, 301). |
  | **Type** | Type of file or request (e.g. document, script, stylesheet, image). |
  | **Initiator** | What triggered the request (e.g. parser, script). |
  | **Size** | Size of the downloaded resource. |
  | **Time** | How long it took to load the resource. |
  | **Waterfall** | A visual timeline showing when and how long each resource took to load. |
- The **visual timeline** looks like a **cascade of bars**, each representing a different resource’s loading time — hence the name “waterfall.” It helps visualize:
	- **When** resources start loading.
	- **Which ones block others**.
	- **Parallel vs. sequential** loading.
	- **Delays**, such as DNS lookup, connection time, SSL handshake, time to first byte (TTFB), content download, etc.