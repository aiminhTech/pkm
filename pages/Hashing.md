parent:: [[Data Transformation and Security]]

- **Converts an input into a feixed-size string called a hash value**
  background-color:: blue
- ## Key Properties
	- **Deterministic**: Same input -> Same hash
	- **Fast**: Computers hash quickly
	- **Pre-image Resistance**: Hard to get the original input from hash
	- **Avalanche Effect**: Small input change -> Very different hash
	- **Collision Resistance**: Hard to find two inputs with the same hash
	-
- ## Common Uses
	- **Data Integrity**: Detects file changes.
	- **Password Storage**: Stores passwords securely.
	- **Cryptography**: Used in digital signatures and secure protocols.
	- **Data Structures**: Hash tables for fast data lookup.
-
- ## Popular Hash Functions
	- ### MD5
		- 128-bit, outdated, insecure due to collisions.
	- ### SHA-1
		- 160-bit, vulnerable to collisions, mostly phased out.
	- ### SHA-256
		- 256-bit, secure, widely used (SSL/TLS, Bitcoin, digital signatures).
		- **Why SHA-256 is Recommended**
			- Secure against collisions.
			- Widely adopted as a standard.
			- Performance is good for most applications.
-
-