tags:: [[Chrome Developer Tools]], [[Core Web Vitals]]

-
- **Course**
	- https://frontendmasters.com/courses/web-perf-v2/
-
-
- ## Importance of WP
  collapsed:: true
	- **User Expectations** -> People expect websites to load quickly. Slow sites make users leave
	- **SEO** -> Faster websites rank higher in search engines
	- **Advertising** -> Ads work better on fast websites because users stay longer and interact more
	- ### Benefits of WP
		- Better user experience
		- Higher SEO ranking
		- More effective advertising
		- Increased conversions (faster sites lead to more sales or sign-ups)
		- Lower bounce rates (fewer people leave before the site loads)
-
- ## Measuring
  collapsed:: true
	- #[[Waterfall Charts]], #[[Flame Charts]], #[[Core Web Vitals]]
	- ### Legacy Metrics
		- Older ways of measuring web perfomance. They were used in the past to see how fast a web page loads.
		- They are called **legacy metrics** because they only measure **when the page technicallly finishes loading**, no how fast it feels to users
		- **DOM Content Loaded**: when the HTML is fully downloaded and JS has run
		- **Load Event**: when all resources, including images are fully loaded and displayed
	-
- ## Capturing
  collapsed:: true
	- ### Performance API
		- https://developer.mozilla.org/en-US/docs/Web/API/Performance
		- `performance.now()`:
			- Return a high-precision timestamp in ms
			- Useful for measuring how long somthing takes
		- `performance.getEntries()`
			- Return a list of **performance entries** (like navigation, resource loading, paint timings, etc.).
			- Each entry shows details such as start time and duration.
	- ### Performance Observer
		- If we only use `performance.getEntries()`, we **might miss some events** (like layout shifts or paints) because they happen before we ask for them. This is called the **==observer effect==**, we only see data after we start observing, not what already happened.
		- Solution -> `PerformanceObserver`
		- `PerformanceObserver` lets us **listen for performance events as they happen**.
		- The browser collects the data and reports it when the main thread is idle, so it doesn’t slow the page down.
		- ```js
		  const observer = new PerformanceObserver((list) => {
		    for (const entry of list.getEntries()) {
		      console.log('Layout shift score:', entry.value);
		    }
		  });
		  
		  observer.observe({ type: 'layout-shift', buffered: true });
		  
		  ```
- ## Testing & Tools
	- ### Testing Methods
		- **Lab data / Synthetic testing**
			- Run tests in a controlled environment using tools like **Lighthouse** or **WebPageTest**.
			- Pros: consistent results, easy to compare changes.
			- Cons: may not reflect real user experience.
		- **Field data / Real user monitoring (RUM)**
			- Collect data from **actual users visiting your site**.
			- Pros: shows real-world performance across devices, networks, and locations.
			- Cons: less controlled, more variable results.
	- ### Tools:
		- DevTool, Google Lighthouse
		- https://requestmetrics.com/resources/tools/crux/
		- https://pagespeed.web.dev/
		- https://webpagetest.org/
	- ### Real User Monitoring (RUM)
		- **RUM** collects performance data from **actual users** visiting your website, giving insights into real-world experiences.
		- Helps identify **slow pages, device/network issues, and bottlenecks** that lab tests might miss.
		- **Rum Tools**
			- **Enterprise-level:** Akamai mPulse, New Relic, Datadog
			- **Project-based / lightweight:** [[Request Metrics Tool]], Web Vitals JS
		- **Benefits:**
			- Measures performance across **real devices, browsers, and networks**
			- Helps prioritize improvements that **matter most to users**
- ## Settings Goals
  collapsed:: true
	- ### How fast should the site be?
		- Speed is partly technical and partly psychological
		  background-color:: blue
		- The **perception of speed** is not the same for everyone. Different users anf tasks affect how fast or slow a site feels
		- For important tasks (like checking out in a store), users notice delays more
		- For less important tasks, they may be more patient
		- **The Psychology of Waiting**
			- People want to **start**
			- Bored (nothing to do), Anxious (worry if the site is broken), Unexplained (dont know why they are waiting) and Uncertain (not knowing how long it will take) waits feel slower
			- People will wait for **value**
		- => The solution is to **make sites technically fast AND make them *feel* fast** by managing user expectations (show progress, give feeback, make waits interactive, etc.)
		  background-color:: pink
	- ### Determine Goals
		- site should be fast enough to **keep users happy, beat competitors, and rank well in search.**
		- The speed a website depends on 3 factors:
			- **User experience** → Users expect fast loading; slow sites make them leave.
			- **Competitors** → To stand out, your site usually needs to be about **20% faster** than others for users to notice.
			- **SEO page rank** → Google rewards faster sites with better search rankings.
	- ### Understanding users
		- https://statcounter.com/
		- Understanding website's user base is key to testing and optimizing for a better experience. Users visit from many devices, screen sizes, OS and network speeds
		- Some may use high-end laptops, others low-end phones. Some have fast Wi-fi, others rely on slow mobile data. Different screen sizes change how site looks and works.
		- => **By knowing the audience, we can test on the right conditions and make sure the site feels fast and usable for all types of users, not just the best-case scenario**
		  background-color:: pink
-
- ## Improving Performance
  collapsed:: true
	- Use real data, not just lab data
	- Fix the worst metric first (small fixes that bring quick improvments)
	- Reduce the number of steps between what you’re measuring (for example, fewer scripts or requests between a click and the page update).
	- ![image.png](../assets/image_1756456827924_0.png)
- ## Improving TTFB
  collapsed:: true
	- TTFB is important because if affects other metrics like
		- **FCP**: nothing can be painted until the first bytes arrives
		- **LCP:**: a slower server delays when the main content shows up
	- For UX, a long TTFB feels like the sites is **frozen** before anything happens
	-
	- ### Compresss HTTP Responses #[[Compression Algorithms]]
	  background-color:: yellow
		- **Compression = smaller files → faster pages.**
		  background-color:: blue
		- **Considerations:**
			- Brotli gives better results, but not all servers/devices support it.
			- Compression adds some CPU cost on the server side.
			- Best practice: enable compression in **local dev environment** to test performance before deploying.
	- ### Efficient Protocols #[[Web Communication Protocols]]
	  background-color:: yellow
		- HTTP 2 and 3 **stream multiple resources efficiently** to improve speed and reliability compared to HTTP 1.1.
	- ### Host Capcity
	  background-color:: yellow
		- Make sure the **server matches the workload**. Too small = slow, too big = wasted resourxes
		- Optimize the system to **reduce delays**, like faster server processing and better network handling
	- ### Host Proximity #CDN
	  background-color:: yellow
		- CDNs store copies of your content **closer to users** around the world
		- This reduces the time it takes for data to travel and speeds up page loads. Especially helpful for large files lime imgs, videos or scripts
- ## Improving FCP
  id:: 68b1671d-71e4-4d17-a229-414b10f6fc4b
  collapsed:: true
	- It's closly related to TTFB and LCP (FCP happens first, LCP is the largest content)
	-
	- ### Remove Sequences Chains
	  background-color:: yellow
		- Sequential loading of resources like CSS and fonts can block rendering, delaying FCP.
		- **Fewer sequential dependencies = faster content display for users.**
		- => Collapse these deps by **prepackaging** CSS and JS with a bundler #Webpack, #Rollup, #Vite
		  background-color:: blue
		- This reduces waiting for multiple files to load one after another, resulting in **a faster FCP**
	- ### Preloading Resources
	  background-color:: yellow
		- Preloading tells the browser to **start downloading importants files early**, before they are needed for rendering
		- **Link Preload**
			- Can preload style, script img, font and fetch (font & fetch mabe need CORS)
			- Use `preload` to start fetching the font files right away
			- ```html
			  <link rel="preconnect" href="https://fonts.googleapis.com">
			  <link rel="preload" as="style" href="https://fonts.googleapis.com/css?family=Roboto">
			  ```
	- ### Lazy Loading 
	  background-color:: yellow
		- Loading resources only when they are needed, instead of all at once. Commonly used for imgs, videos or offscreen content
		- **Using `defer`**
			- Adding the `defer` attribute to `<script>` tags tells the browser to load the script in the background and execute it after HTML parsing
			- ```html
			  <script src="script.js" defer></script>
			  ```
		-
	-
- ## Improving LCP
  collapsed:: true
	- ### Optimize Loading
	  background-color:: yellow
	  collapsed:: true
		- #### Lazy Loading Imgs
		  background-color:: yellow
			- **Lazy loading** delays loading of **non-critical resources**, like images that aren’t immediately visible on the screen
			- Use the `loading="lazy"` attribute on images that are **not part of LCP**
			- ```html
			  <img src="non-critical-image.jpg" loading="lazy" alt="Example">
			  ```
			- This tells the browser to **load the image only when it’s about to appear**, reducing initial load time.
		- #### Eager Loading
		  background-color:: yellow
			- This makes sure the LCP element loads as soon as posible
			- **How to prioritize important images:**
				- **`fetchPriority="high"`** → tells the browser to download this image **before others**
				- ```html
				  <img src="hero.jpg" fetchPriority="high" alt="Hero image">
				  ```
				- **Preload the image** → instructs the browser to **start fetching the image early**, even before it’s used in HTML.
				- ```html
				  <link rel="preload" as="image" href="hero.jpg">
				  ```
			- Both methods help reduce **resource delay** and **render delay**, improving LCP.
	- ###  Optimize Images #[[Image Format]]
	  background-color:: yellow
	  collapsed:: true
		- #### Formats #[[Image Format]]
			- Sending smaller imgs makes pages load faster
			- HTTP compression (Gzip/Brotli) does not help much for imgs because fomats like JPEG and PNG are already compressed
			- **Choose modern, efficient img formats: WebP, AVIF = fewer bytes = faster laoad**
			  background-color:: blue
		- #### Responsive
			- Adapt to different screen sizes and resolutions, so users dont download unnessessarily large fles
			- Helps reduce load time and improve performance
			- **`srcset` attribute**
				- Provides multiple image sources for different screen widths or resolutions
				- ```html
				  <img src="small.jpg"
				       srcset="medium.jpg 768w, large.jpg 1200w"
				       sizes="(max-width: 768px) 100vw, 1200px"
				       alt="Example image">
				  
				  ```
			- **`<picture>` element**
				- Lets you provide **different formats or images** for different conditions (e.g., WebP vs JPEG)
				- ```html
				  <picture>
				    <source srcset="image.avif" type="image/avif">
				    <source srcset="image.webp" type="image/webp">
				    <img src="image.jpg" alt="Example image">
				  </picture>
				  
				  ```
	- ### Caching
	  background-color:: yellow
		- Stores copies of resources so returning users don't have to download them again -> improving speeed
		- **Types of Caching**
			- **Server Caching** = The server keeps a copy of generated content to respond faster
			- **Browser Caching** = The user's browser stores files like imgs, CSS and JS locally
		- **How to control caching:**
			- **Cache-Control headers**: define how long and under what conditions resources can be cached.
			- **Expires headers**: set a specific expiration date for cached resources.
- ## Improving CLS & INP
	- ### Tatics to improve CLS
		- **Specify image dimensions** → set `width` and `height` for images so the browser reserves space.
		- **Provide layout size hints** → reserve space for ads, embeds, or dynamic content.
		- **Avoid late-rendered content pushing elements** → load critical content first or use placeholders.
	- ### Tatics to improve INP
		- **`setTimeout`** → breaks long tasks into smaller chunks, giving the browser a chance to handle user input.
		- **`requestAnimationFrame`** → schedules updates **just before the next paint**, ensuring smoother animations and timely responses.
-