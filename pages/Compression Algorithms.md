tags:: [[Web Performance]]

- Are methods used to make files **smaller** so they take up less space and load faster over the internet.
- They work by **removing redundancy** in the data.
- Common examples for web files: **Gzip** and **Brotli**.
- **Benefits:**
	- Faster page loads
	- Less bandwidth usage
	- Better user experience
- **A compression algorithm = a way to shrink files without losing important information.**
  background-color:: blue
-
- **Gzip** = fast, widely supported.
- **Brotli** = better compression, modern, but slightly heavier to generate.
-
- ## Gzip
	- https://developer.mozilla.org/en-US/docs/Glossary/gzip_compression
	- An**older but very common**  compression algorithm
	- Supported by almost all servers and browsers
	- Make text files (HTML, CSS, JS) much smaller => faster downloads
- ## Brotli
	- https://developer.mozilla.org/en-US/docs/Glossary/Brotli_compression
	- A newer compression algorithm, developed by Google
	- Usually compresses better than Gzip (smaller file sizes)
	- Supported by all modern browsers, but can use a bit more **CPU power** when creating the files.