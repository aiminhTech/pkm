- https://integration-api.apps.ipip-ocp.ipip.ch/menu.shtml
- https://i-database.ipi.ch/database/api/healthcheck
-
- Eine interaktiven Webseite für die Überprüfung des Status von verschiedenen API-Healthcheck-Endpoints.
- ## Tools
	- **Backend**: [[Hono]], [[Deno]]
	- **Frontend**: [[Vue.js]], [[Element Plus]]
- ## Possible solutions for blocked request
	- **Domain Sharding**: This involves splitting resources across multiple subdomains. By doing so, browsers treat these subdomains as different hosts and allow six connections per domain, effectively increasing the total limit.
	- **Asynchronous Loading**: Load non-critical resources asynchronously, after the initial page load. JavaScript allows for asynchronous loading of scripts and other resources, which can help in reducing the immediate load and distribute it over a longer period, improving initial page load times.
	- **Utilize Browser Caching**: By properly leveraging browser caching, you can reduce the number of resources that need to be loaded from the server on subsequent visits. This involves setting appropriate cache-control headers on your resources.
	- **Deploy Content Delivery Network (CDN)**: Using a CDN can distribute your content across multiple geographically dispersed servers. This not only helps in reducing latency by serving content from a location closer to the user but can also help sidestep the concurrent connection limit by serving different resources from different domain names managed by the CDN.
	- **Upgrade to HTTP/2 or HTTP/3**: Both HTTP/2 and HTTP/3 offer improvements over HTTP/1.1, including the ability to multiplex requests over a single connection, essentially eliminating the need for multiple connections and the associated limit. Upgrading your server to support HTTP/2 or HTTP/3, and ensuring clients support it, can significantly improve performance. HTTP/2 is widely supported in modern browsers and offers backward compatibility with HTTP/1.1.