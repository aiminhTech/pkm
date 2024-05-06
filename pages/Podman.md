## run container
	- `podman run -it --rm docker.io/denoland/deno:ubuntu-1.36.4`
	- podman run --name chatpad --rm -it -p 8080:80 ghcr.io/deiucanta/chatpad:latest
	- ``` 
	  podman build -t hello-openshift-time:latest .
	  podman run -it --rm --publish 9000:8000 hello-openshift-time:latest
	  podman image ls
	  ```
	- podman build -t "time-svc" -f Dockerfile-time .  //build container
	  podman tag localhost/time-svc:latest default-route-openshift-image-registry.apps.ipip-ocp.ipip.ch/test-qai-hello-openshift/time-svc:latest
- ## Steps to create image
	- **Write** a [[Dockerfile]]
	- **Build image locally** `podman build -t my-image:tag /path/to/Dockerfile/directory`
	- **Run the container** ``
	- **Push the Image** `podman push`
- ## Build with `build.sh`
	- exp
		- ```
		  #!/bin/bash
		  
		  podman build -t "hello-openshift-time" -f Dockerfile-time ..
		  podman build -t "hello-openshift-date" -f Dockerfile-date ..
		  podman build -t "hello-openshift-data" -f Dockerfile-data ..
		  
		  podman tag localhost/hello-openshift-date:latest default-route-openshift-image-registry.apps.ipip-ocp.ipip.ch/test-qai-hello-openshift/hello-openshift-date
		  podman tag localhost/hello-openshift-time:latest default-route-openshift-image-registry.apps.ipip-ocp.ipip.ch/test-qai-hello-openshift/hello-openshift-time
		  podman tag localhost/hello-openshift-data:latest default-route-openshift-image-registry.apps.ipip-ocp.ipip.ch/test-qai-hello-openshift/hello-openshift-data
		  
		  podman push default-route-openshift-image-registry.apps.ipip-ocp.ipip.ch/test-qai-hello-openshift/hello-openshift-time
		  podman push default-route-openshift-image-registry.apps.ipip-ocp.ipip.ch/test-qai-hello-openshift/hello-openshift-date
		  podman push default-route-openshift-image-registry.apps.ipip-ocp.ipip.ch/test-qai-hello-openshift/hello-openshift-data
		  ```
	- `chmod a+x oci-image/build.sh` => Add execute permission to the `oci-image/build.sh` file for all users.
		- `chmod`: change file permissions in Unix-like operating systems.
		- `a+x`: This part specifies the permission change.
		- `a` stands for "all users," which means it will change permissions for the owner, the group, and others.
			- `+x` means "add execute permission." It grants the permission to execute the file.