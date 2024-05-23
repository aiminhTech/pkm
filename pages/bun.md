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
- ## `bun update`
	- update all deps to the latest versions that's compatible with the version range specified in `package.json`
	- does not update directly in `package.json` but `bun.lockb`
	- check out `bun.lockb` when use `bun update`
-
-