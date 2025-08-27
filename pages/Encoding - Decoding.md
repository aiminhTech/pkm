parent:: [[Data Transformation and Security]]

- **Encoding**: Converting data into **a specific format** so that it can be **stored, processes or transmitted** by computers
	- **=> Changing data into a usable/transmittable format**
	  background-color:: blue
- **Decoding**: Taking the encoded data and **converting it back into its original form** so it can be unterstood by software or humans
	- => **Changing it back so humans/apps can understand**
	  background-color:: blue
-
- ## Charater Encoding
	- These are ways to represent letters, numbers and symbols in binary (0 and 1) so computer can store and process text
	- ### ASCII (American Standard Code for Infomation Interchange)
		- https://developer.mozilla.org/de/docs/Glossary/ASCII#:~:text=ASCII%20(American%20Standard%20Code%20for,in%20digitale%20Form%20verwendet%20werden
		- Uses **7 bits** (128 possible characters).
		- Covers **English letters, digits, punctuation** (A–Z, a–z, 0–9, etc).
		- Example:
		- Letter `A` → **65** in decimal → `01000001` in binary.
	- ### UTF-8 (Unicode Transformation Format, 8-bit) - modern
		- Uses **1 to 4 bytes** (8–32 bits) depending on the character.
		- Compatible with ASCII (the first 128 characters are the same).
		- Example:
			- English `A` = same as ASCII.
			- Emoji 😀 needs 4 bytes.
	- => ASCII = limited to English, UTF-8 = global (covers almost all writing systems + emojis)
	  background-color:: blue
	-
- ## Base Encoding
	- These are data encoding schemes.
	- They are used to **convert binary data into text format** so it can safely travel through systems that only handle text (like JSON, URLs)
	- ### Base32
		- https://de.wikipedia.org/wiki/Base32
		- Use **32 Characters**:  A–Z + 2–7.
		- Output is longer but easier to read (case-insensitive).
		- Often used in QR codes, OTP (Google Authenticator codes).
	- ### Base64
		- https://de.wikipedia.org/wiki/Base64
		- Uses **64 characters**: A–Z, a–z, 0–9, +, /.
		- Common for encoding images, files, or binary data in text-based formats (like sending an image in an email).