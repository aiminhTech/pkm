- https://www.npmjs.com/
- https://www.baeldung.com/ops/npm-install-vs-npm-ci
-
- ## `npm install`
	- Installs the dependencies required to run the project.
	- We define the project’s direct dependencies in the *package.json* file:
		- ```package.json
		  {
		    "name": "some-project",
		    "version": "1.0.0",
		    "dependencies": {
		      "lodash": "^4.17.21"
		    },
		    "devDependencies": {
		      "eslint": "^8.1.0"
		    }
		  }
		  ```
	- In this example, we use a *package.json* with **caret (^) version** ranges to specify the versions of the [*lodash*](https://www.npmjs.com/package/lodash) and [*eslint*](https://www.npmjs.com/package/eslint) packages while allowing *npm* to accept new minor versions of these dependencies automatically.
	- **ignore peer dependencies**
		- `--legacy-peer-deps`
- ## `npm ci`
	- When no lock file exists, *npm install* installs dependencies according to *package.json* and [[Semantische Versionierung]] In addition, the command automatically generates a *package-lock.json* file, which locks a snapshot of installed versions.