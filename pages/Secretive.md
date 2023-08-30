tags:: macos

- https://github.com/maxgoedjen/secretive
- Store SSH Keys in Secure Encalve
- ## Safer Storage
	- The most common setup for SSH keys is just keeping them on
	  disk, guarded by proper permissions. This is fine in most cases, but 
	  it's not super hard for malicious users or malware to copy your private 
	  key. If you store your keys in the Secure Enclave, it's impossible to 
	  export them, by design.
- ## Access Control
	- If your Mac has a Secure Enclave, it also has support for strong access controls like Touch ID, or authentication with Apple Watch. You can configure your keys so that they require Touch ID (or 
	  Watch) authentication before they're accessed.
-
-