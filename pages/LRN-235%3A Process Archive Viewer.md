tags:: [[IGE]], [[S3]]

- https://issues.ipip.ch/browse/LRN-235
- https://wiki.ipip.ch/pages/viewpage.action?pageId=178930536
-
- ## Ansible Deploy Dev
	- `ipi-ansible-playbook -i inventories/entwicklung/ -p process_archive_viewer`
- ## Project Links
	- **JIRA**: https://issues.ipip.ch/browse/LRN-235
	- **Bitbucket**: https://git.ipip.ch/users/quach/repos/process-viewer/browse
	- **Openshift**:
		- **entwicklung**: https://dev-process-archive-viewer.apps.ipip-ocp.ipip.ch/
		- **abnahme**: https://a-process-archive-viewer.apps.ipip-ocp.ipip.ch/
		- **produktion**: https://process-archive-viewer.apps.ipip-ocp.ipip.ch/
- ## Sourcecode
  collapsed:: true
	- https://archive.ipip.ch/
	- **Inklusiv container und alles**: https://git.ipip.ch/projects/OPS/repos/process-archive-viewer/browse
	- **Python code für den frontent + backend**: https://git.ipip.ch/projects/OPS/repos/process-archive-viewer/browse/app/main.py
	- **Python code Elastic**: https://git.ipip.ch/projects/OPS/repos/rundeck_batch/browse/BPP_camunda_prozess_archivieren/run.py?at=refs%2Fheads%2FAM-677_prozess_historie_elastic#745,885,930,956,986
- ## Tools
	- ### Frontend #Angular, #[[Angular Material]]
	- ### Backend:
		- #### [[S3]]
		  collapsed:: true
			- {{embed ((66bded88-8a50-4ec3-a9bc-79f48af21d10))}}
		- #### [[Elastic Search]]
			- {{embed ((66cc7663-c057-4a83-affc-eeaefc514740))}}1
			  id:: 673d95bf-62d7-4db1-ba9c-7b4a1b3fd929
	- ### Testing
		- https://issues.ipip.ch/browse/LRN-247
	- ### Deployment
		- #### Vault Secret Paths
			- production:
			- abnahme: https://vault.ipip.ch/ui/vault/secrets/abnahme/kv/platforms%2Fs3%2FA_LAN_Elektronische_Geschaeftsprozesse/details?version=4
			- entwicklung: https://vault.ipip.ch/ui/vault/secrets/entwicklung/kv/applications%2Fprocess-archive-viewer/details?version=1
- ## Libraries
  collapsed:: true
	- **@elastic/elasticsearch**: https://www.elastic.co/guide/en/elasticsearch/client/javascript-api/current/index.html
	- **timelines-chart**: https://www.npmjs.com/package/timelines-chart
	- **ngx-simple-charts**:
		- https://angular2guy.wordpress.com/2023/07/01/a-scrolling-date-timeline-chart-with-angular-material-components/
		- https://github.com/Angular2Guy/ngx-simple-charts
	- **apexcharts**: https://apexcharts.com/angular-chart-demos/timeline-charts/
-
- ## Subtasks
	- [[LRN-237: Frontend Verbesserung Dropdowns]]
	- [[LRN-238: Frontend Verbesserung Widgets]]
	- [[LRN-239: Frontend Verbesserung Tabelle]]
	- [[LRN-240: Frontend Verbesserung Views]]
	- [[LRN-241: Frontend Implementierung Duration]]
	- [[LRN-244: Frontend Verbesserung Landingpage]]
	- [[LRN-245: Backend Integration Testing]]
	- [[LRN-246: : Frontend Implementierung Paging in Business-Transaction-View]]
	- [[LRN-247: Release Process Archive Viewer mit Ansible]]
	- [[LRN-255: Manuelles Testen und Fehlerbehebung vor Release]]