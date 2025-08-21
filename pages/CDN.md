tags:: [[JavaScript]], [[CSS]], [[Skypack]]

- Stands for **Content Delivery Network**. It’s a network of distributed servers around the world that deliver web content (like images, JavaScript, CSS, videos, or even entire websites) to users **based on their geographic location**.
-
- ## Key Points
	- **Purpose:**
		- Make websites and apps **load faster** for users everywhere.
		- Reduce the load on a single server.
		- Improve reliability and availability (if one server goes down, another can serve the content).
	- **How it works:**
		- A CDN stores **copies of static files** (like images, JS libraries, CSS) on servers in multiple locations (called **edge servers**).
		- When a user visits your site, the CDN serves the files from the **nearest server**, minimizing latency.
	- **Benefits:**
		- Faster page load times.
		- Reduced bandwidth costs.
		- Better scalability during traffic spikes.
		- Often comes with **security features**, like DDoS protection.
	- **Examples of CDN usage:**
		- Loading popular JavaScript libraries via a CDN instead of bundling them in your project:
		  
		  ```html
		  <script src="https://cdn.jsdelivr.net/npm/aframe@1.4.2/dist/aframe.min.js"></script>
		  ```