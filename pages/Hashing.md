- Hashing is a process used in computing *to convert an input (or message) into a fixed size string of characters*, which typically a sequence of numbers and letters. This output is known as a **hash value**. **hash code** or **digest**.
- Hash functions are designed to be fast and **to produce a unique output for each unique input**, even though the size of the output is fixed and 
  generally much smaller than the input.
-
- ## Key Properties
	- **Deterministic**: The same input will always produce the same hash value.
	- **Fast Computation**: Hashing should be computationally efficient, meaning it can quickly produce a hash value.
	- **Pre-image Resistance**: It should be infeasible to reverse-calculate the original input from its hash value.
	- **Small Changes in Input**: A small change in the input should produce a significantly different hash value. This is known as the "avalanche effect."
	- **Collision Resistance**: It should be infeasible to find two different inputs that produce the same hash value.
- ## Common Uses of Hashing:
	- **Data Integrity**: Hashing ensures the integrity of data files. Even slight alterations to a file will result in a completely different hash valu
	- **Password Storage**: Systems often store passwords in their hashed forms to prevent unauthorized access. Even if the hashed 
	  passwords are stolen, they can't be easily reversed to the original passwords
	- **Cryptography**: Hashing plays a crucial role in various cryptographic algorithms and digital signatures
	- **Data Structures**: Hash tables use hash functions to quickly locate data in a database
-
- ## Popular hash functions
	- ### MD5 (Message-Digest Algorithm 5)
		- **Length**: Produces a 128-bit hash value.
		- **Usage**: Was widely used in the past for checksums and password hashing.
		- **Security**: Considered insecure by modern standards due to vulnerabilities allowing for hash collisions (two different 
		  inputs producing the same hash). This makes it unsuitable for security-sensitive applications.
	- ### SHA-1 (Secure Hash Algorithm 1)
		- **Length**: Produces a 160-bit hash value.
		- **Usage**: Used in various security applications and protocols, including TLS and SSL, until vulnerabilities were discovered.
		- **Security**: Known to be vulnerable to collision attacks since 2005, and major organizations typically mandate phasing it
		  out in favor of more secure alternatives.
	- ### SHA-256 (Secure Hash Algorithm 256)
		- **Length**: Produces a 256-bit hash value.
		- **Usage**: Widely used in various security protocols, including SSL/TLS, Bitcoin, and digital signatures.
		- **Security**: Currently considered very secure and collision-resistant, making it a popular choice for contemporary cryptographic needs.
		-
- ## Why SHA-256 is Recommended
	- **Security**: SHA-256 is part of the SHA-2 family, which offers significant improvements over both MD5 and SHA-1. It is 
	  resistant to known collision attacks, making it suitable for applications requiring high security.
	- **Adoption**: SHA-256 is adopted by numerous security systems, including SSL/TLS, and is considered the standard for secure hashing.
	- **Performance**: While more complex than MD5 and SHA-1, the performance of SHA-256 is acceptable for most applications, and the
	  increased security is usually a worthwhile trade-off.
-