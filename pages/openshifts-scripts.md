tags:: [[IGE]]

- https://git.ipip.ch/projects/OPS/repos/operations-scripts/browse
- Eine Sammlung von Scipts, die für das IGE Operations Team sinnvoll sind. Dabei sind unterschiedliche Scriptsprachen vertreten (python, bash) und auch unterschiedliche Reifergrade der Tools.
-
- ## `ocifind`
	- Extracts the given OCI image to a temporary location and invokes the find(1) command.
	- ```bash
	  SYNOPSIS:
	      ocifind <image-name> [find arguments...]
	  
	  EXAMPLES:
	      PULL=missing ocifind docker.io/library/alpine:latest -type f | fzf
	      PULL=never ocifind localhost/process-viewer-backend:latest -type f | fzf
	  
	  ENVIRONMENT VARIABLES:
	      PULL=[*always|missing|never|newer] : podman pull policy
	      FIND=find                          : custom find command
	      TMPDIR=${TMPDIR-"/tmp"}            : base directory for mktemp (used internally)
	  ```
	-
-