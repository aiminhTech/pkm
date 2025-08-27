tags:: [[Chrome Developer Tools]], [[Core Web Vitals]]

-
- **Course**
	- https://frontendmasters.com/courses/web-perf-v2/
-
-
- ## Importance of WP
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
	- #[[Waterfall Charts]], #[[Flame Charts]], #[[Core Web Vitals]]]]
	- ### Legacy Metrics
		- Older ways of measuring web perfomance. They were used in the past to see how fast a web page loads.
		- They are called **legacy metrics** because they only measure **when the page technicallly finishes loading**, no how fast it feels to users
		- **DOM Content Loaded**: when the HTML is fully downloaded and JS has run
		- **Load Event**: when all resources, including images are fully loaded and displayed
	-
- ## Capturing
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
-
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
	- **Tools**:
		- DevTool, Google Lighthouse
		- https://requestmetrics.com/resources/tools/crux/
		- https://pagespeed.web.dev/