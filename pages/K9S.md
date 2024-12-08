- https://k9scli.io/
- K9s is **a terminal based UI to interact with your Kubernetes clusters**.
-
- ## Commands
	- https://k9scli.io/topics/commands/
	- ```
	  # List all available CLI options
	  k9s help
	  
	  # Get info about K9s runtime (logs, configs, etc..)
	  k9s info
	  
	  # Run K9s in a given namespace.
	  k9s -n mycoolns
	  
	  # Run K9s and launch in pod view via the pod command.
	  k9s -c pod
	  
	  # Start K9s in a non default KubeConfig context
	  k9s --context coolCtx
	  
	  # Start K9s in readonly mode - with all modification commands disabled
	  k9s --readonly
	  
	  ```
-
- ## Taskfile
	- ```taskfile.yaml
	  k9s:
	      deps:
	        - login
	      interactive: true
	      cmds:
	        - ipi-oc-k9s {{.OC_PROJ_PREFIX}}-{{.PROJ}}
	  ```