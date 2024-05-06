tags:: [[NPM]]

- https://bun.sh/
- `bun install`
- ## `bunfig.toml`
	- ```toml
	  telemetry = false
	  
	  [install]
	  #frozenLockfile = true
	  registry = "https://repository.ipip.ch/repository/npm-public/"
	  
	  [install.cache]
	  dir = ".bun/install/cache"
	  disable = true
	  ```