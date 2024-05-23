tags:: K8S

- https://www.redhat.com/de/technologies/cloud-computing/openshift
- ## ipi
	- ` ipi-oc-login-internal`
		- https://console.apps.ipip-ocp.ipip.ch/dashboards
	- `ipi-oc-login-dmz` #DMZ
		- https://console.apps.ipi-ocp.ipi.ch/dashboards
- ## Overview
	- [[OCI]] image
		- contains the packaged application
	- [[RedHat Container Tools]]
	- [[Kubernetes]]
- ## SWE Admin Manifest auf Openshift Projekt
	- ```yml
	  kind: RoleBinding
	  apiVersion: rbac.authorization.k8s.io/v1
	  metadata:
	    name: admin_swe
	  subjects:
	    - kind: Group
	      apiGroup: rbac.authorization.k8s.io
	      name: Auth_OS_SWE
	  roleRef:
	    apiGroup: rbac.authorization.k8s.io
	    kind: ClusterRole
	    name: admin
	  
	  ```