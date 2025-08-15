tags:: [[Dev-Tools]]

- ## Courses & Links
	- **Courses**
		- https://frontendmasters.com/courses/vs-code-v2/
	- **Common Short Cut:** https://stevekinney.com/courses/visual-studio-code/vscode-keyboard-shortcuts
	- **Popular Extension:**  https://stevekinney.com/courses/visual-studio-code/favorite-vs-code-extensions
-
- ## Key Bindings
	- https://stevekinney.com/courses/visual-studio-code/keybindingschat
	- We can view and customize all shortcuts via the the Command Palette using **`Preferences: Open Keyboard Shortcuts`**
	- To dig deeper, use **`Preferences: Open Keyboard Shortcuts (JSON)`**, which opens the `keybindings.json` file (battleground for fine‑grained shortcut control)
	- **Keybinding Rule Structure**
		- Each rule in `keybindings.json` consists of:
			- `key`: the keyboard combination (e.g. `ctrl+alt+j`),
			- `command`: the VS Code action (e.g. `editor.action.commentLine`),
			- Optional `when`: a context condition that must be met.
			- **Example**: only toggles comments when editing JS
				- ```json
				  {
				    "key": "ctrl+alt+j",
				    "command": "editor.action.commentLine",
				    "when": "editorTextFocus && editorLangId == 'javascript'"
				  }
				  ```
-
- ## Refactoring Techniques
	- https://stevekinney.com/courses/visual-studio-code/refactoring-in-vscode
	- **Rename Symbol**: `F2` => Rename across entire project
	- **Extract Method or Function**: Hightlight a block of code and use the `Extract Method` or `Extract Function`
	- **Extract Variable or Constant**: Select an expression and choose `Extract to variable/constant`
	- **Inline Refactoring**: If a var or func is no longer needed, right-click and choose `Inline`
-
- ## Emmet
  collapsed:: true
	- A shorthand toolkit built-in VS Cide that helps us write HTML, CSS and JSX faster using **abbrevviations**
	- It can expands abbreviations into full code snippets and is great for rapid HTML & CSS writing
	- ### Basic HTML Abbreviations
		- ```html
		  // div
		  <div></div>
		  
		  // div.box
		  <div class="box"></div>
		  
		  // div#main
		  <div id="main"></div>
		  
		  // ul>li*3
		  <ul>
		    <li></li>
		    <li></li>
		    <li></li>
		  </ul>
		  
		  // a[hre="/"]
		  <a href="" hre="/"></a>
		  
		  // p>lorem5
		  <p>Lorem ipsum dolor sit amet.</p>
		  ```
	- ### Nesting and Multiplication
		- `>` =>child element
		- `+` => sibling element
		- `*` => multiple elements
		- `{}` => inner text
		-
- ## Snippets
  collapsed:: true
	- https://stevekinney.com/courses/visual-studio-code/vscode-snippets
	- Snippets are code templates, which predefined blocks that we can quickly insert using a short trigger or prefix. They save time, reduce errors and help enforce consistent formatting accross our projects.
	- ### Structure
		- Defined in JSON, a snippet includes:
			- **`prefix`**: the trigger text
			- **`body`**: an array of code lines to insert
			- **`description`**: optional, shown in IntelliSense
			- **`scope`** (optional): which languages the snippet applies to
		- **Example**:
			- ```json
			  "Print to console": {
			    "scope": "javascript,typescript",
			    "prefix": "log",
			    "body": [
			      "console.log('$1')",
			      "$2"
			    ],
			    "description": "Log output to console"
			  } 
			  ```
			- ```json
			  "for/of Loop": {
			    "prefix": "forloop",
			    "body": [
			      "for (let i = 0; i < ${1:array}.length; i++) {",
			      "\t const ${2:element} = ${1:array}[i];",
			      "\t${0:// body}",
			      "}"
			    ],
			    "description": "Basic for loop in JavaScript"
			  }
			  
			  ```
	- ### Dynamic Features
		- **Placeholders** (`$1`, `$2`, … `$0`): define traversal order and cursor jumps
		- **Variables** (e.g., `${TM_FILENAME}`, `${CURRENT_YEAR}`, `${UUID}`): enable snippets to adapt dynamically based on context
		- **Choices** (e.g., `${1|option1,option2,option3|}`): present dropdown options at insertion time
- ## Tasks - `tasks.json`
  collapsed:: true
	- https://stevekinney.com/courses/visual-studio-code/vscode-tasks
	- It's the configuration file (`.vscode/tasks.json`) where we define automation tasks from building and testing to Docker cmds, sothat we don't need to keep typing the same things over and over
	- **Example**: https://stevekinney.com/courses/visual-studio-code/vscode-task-examples
	- **Tips and Tricks**: https://stevekinney.com/courses/visual-studio-code/vscode-tasks-tips-and-tricks
	- ### Why use tasks?
		- **Consistency**: ensure team-wide cmd across machine
		- **Speed**: execute tasks with `Ctrl+Shift+B` or via `Command Palatte`
		- **Automation**: chain tasks like build -> test -> deploy in 1 cmd
		- **Integration**: plays well with debugging and problem matchers for error handling
	- ### Basic Structure
	  collapsed:: true
		- ```json
		  {
		    "version": "2.0.0",
		    "tasks": [
		      {
		        "label": "Build the project",
		        "type": "shell",
		        "command": "npm run build",
		        "problemMatcher": "$tsc",
		        "group": {
		          "kind": "build",
		          "isDefault": true
		        }
		      }
		    ]
		  }
		  
		  ```
		- **Key properties**:
			- `version`: must be `"2.0.0"`
			- `label`: friendly task name
			- `type`: either `shell` or `process`
			- `command`: what gets executed (e.g., `npm run build`)
			- `problemMatcher`: helps parse errors (e.g., `$tsc`, `$eslint-stylish`)
			- `group`: categorizes tasks (e.g., `"build"`, `"test"`), and can define a default
		- **Task Types**
			- **Shell**: Runs your command in the OS shell (e.g., `echo Hello from the shell!`).
			- **Process**: Executes commands more directly, requiring explicit `command` and `args` (e.g., `node` with `["app.js"]`)
	- ### Compound Tasks
		- Allow to run multiple tasks in sequence. Useful for orchestrating complex workflows (either running them one after the other or simultaneously)
		- **Example Structure**
			- ```json
			  {
			    "version": "2.0.0",
			    "tasks": [
			      {
			        "label": "Task A",
			        "type": "shell",
			        "command": "echo Task A"
			      },
			      {
			        "label": "Task B",
			        "type": "shell",
			        "command": "echo Task B"
			      },
			      {
			        "label": "Run A and B",
			        "dependsOn": ["Task A", "Task B"],
			        "dependsOrder": "sequence",
			        "problemMatcher": []
			      }
			    ]
			  }
			  
			  ```
			- Here, the **"Run A and B"** task triggers both **Task A** and **Task B**, executing them in declared order via `dependsOrder: "sequence"`
		- ### Dependency Modes:  `dependsOrder`
			- **`sequence`** (default): Runs tasks one at a time—in list order. If one fails, subsequent tasks won’t run.
			- **`parallel`**: Launches all dependent tasks at once—great for independent tasks like asset compilation.
			- **`any`**: Starts all tasks in parallel but completes as soon as *any* one finishes. Useful for race-type scenarios.
		- ### Creating Complex Pipelines
			- Using nested dependencies, you can build advanced task flows. For example:
				- **Clean** (remove old builds)
				- **Build Frontend** and **Build Backend** (both depend on Clean)
				- **Run Tests** (depends on both build tasks, in sequence)
				- **Full Pipeline** task to tie everything together
		- ### Summary
			- `dependsOn`: Defines which tasks a compound task triggers
			- `dependsOrder`: Controls execution mode: `sequence`, `parallel`, or `any`
			- Compound Flows: Enables layered workflows—clean → build → test → etc.
- ## Debugging
  collapsed:: true
	- https://stevekinney.com/courses/visual-studio-code/vscode-debugging-basics
	- ### Basic Debugging
		- **Setting Breakspoints**: Place breakpoints on lines where we want execution to pause during runtime
		- **Live Inspection Tools**: When execution stops, wecan inspect variables, examine the call stack, and evaluate expressions to debug effectively
		- **Stepping Through Code**
	- **Launch Configuration via `launch.json`**
		- https://stevekinney.com/courses/visual-studio-code/launch-config
		- VS Code provides debugging templates to get started quickly.
		- ```json
		  // This file tells VS Code how to launch and debug our app
		  {
		    "version": "0.2.0",
		    "configurations": [
		      {
		        "type": "node",
		        "request": "launch",
		        "name": "Launch Program",
		        "skipFiles": ["<node_internals>/**"],
		        "args": ["${workspaceFolder}/index.js"]
		      }
		    ]
		  }
		  
		  ```
- ## Dev Containers
	- https://stevekinney.com/courses/visual-studio-code/vscode-dev-containers
	- It lets we define and work within a fully isolated, consistent development environment using Docker right from VSCode. Editor, terminal, debugger and extensions will all run inside this container, as if it were our local machine.
	- The config lives in a `devcontainer.json` file inside our project
	- ### How to Set Up and Customize
		- https://stevekinney.com/courses/visual-studio-code/setting-up-dev-containers
		  logseq.order-list-type:: number
		- **Add Configuration:** Use CMD Palette `Dev Containers: Add Dev Container Configuration Files…` to choose from prebuilt templates sourced from official `vscode-dev-containers` GitHub repo
		  logseq.order-list-type:: number
		- **Customize with `devcontainer.json`:** After setup, you’ll get a generated `devcontainer.json` that you can tweak, specifying the base image, additional VS Code features, port forwarding, post-create commands, and user privileges
		  logseq.order-list-type:: number
-
-