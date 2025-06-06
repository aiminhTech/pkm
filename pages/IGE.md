project:: [[IGE Procedure App]], [[LRN-235: Process Archive Viewer]], [[LRN-276: Data Delivery Explorer]]

- ## Projects
	- ### Vorlehre
		- [[Memory Game]]
	- ### 2. Lehrjahr
		- [[hello-openshift]]
		- [[LRN-197: TMB]]
		- [[LRN-202: AI Chat]]
		- [[LRN-213: Supercheck Website]]
	- ### 3. Lehrjahr
		- [[LRN-235: Process Archive Viewer]]
		- [[LRN-276: Data Delivery Explorer]]
		- **Procedure-App**
			- [[EGOV-3553: Frontend Umsetzung Erneuerung Zugriff Kontokorrentauszüge]]
			- [[EGOV-3553: Frontend Umsetzung Erneuerung Zugriff Kontokorrentauszüge]]
- ## Login Info
  collapsed:: true
	- ### S3 
	  id:: 66bded88-8a50-4ec3-a9bc-79f48af21d10
	  collapsed:: true
		- #S3
		- https://s3-admin.ipip.ch/ui/s3-console/
			- **Tenant Name:** A_LAN_Elektronische_Geschaeftsprozesse
			- ```
			  s3_access_key_id=  "74I2SNGE16W4I4YN35LP"
			  s3_secret_access_key = "zvzZASPzS2ld+2x5KN2Qn/OnSZViYWOW/ECxeAuj"
			  s3_endpoint = https://s3.ipip.ch:10443	
			  ```
		- https://s3-admin.ipip.ch/?accountId=94734607459828255227
			- user: root
			- pass: Welcome2IGE
	- ### Elastic
	  id:: 66cc7663-c057-4a83-affc-eeaefc514740
		- #[[Elastic Search]]
		- ### API
			- [https://a-elasticsearch.ipip.ch](https://a-elasticsearch.ipip.ch)
			- ```
			  user: elastic
			  password: HnIrsM_q7MfEQlB1uPJ8
			  ```
		- ### Elastic Kibana UI
			- Dort kann man die Indexes und Struktur sehen
			- [https://a-elastic.ipip.ch](https://a-elastic.ipip.ch)
			- [https://a-elastic.ipip.ch/app/dev_tools#/console](https://a-elastic.ipip.ch/app/dev_tools#/console) (für Elastic dev Konsole)
			- ```
			  user: elastic
			  password: HnIrsM_q7MfEQlB1uPJ8
			  ```
		- ### Python code, der in Elastic schreibt
			- (nicht finale Version,wird noch geändert, aber die Index Struktur ist ziemlich fest):
			- [https://git.ipip.ch/projects/OPS/repos/rundeck_batch/browse/BPP_camunda_prozess_archivieren/run.py?at=refs%2Fheads%2FAM-677_prozess_historie_elastic#745,885,930,956,986](https://git.ipip.ch/projects/OPS/repos/rundeck_batch/browse/BPP_camunda_prozess_archivieren/run.py?at=refs%2Fheads%2FAM-677_prozess_historie_elastic#745,885,930,956,986)
	- ### Camunda Cockpit
	  collapsed:: true
		- https://i-esv.ipie.ch/cockpit/app/cockpit/ir-marke-geschaeftsprozesse/#/login
		- ```
		  user: gast
		  password: gast
		  ```
	- ### Vault
	  id:: 66cc8d92-a4fb-4ef2-909f-d95d38766b74
		- https://vault.ipip.ch/ui/vault/
		- ```
		  windows user
		  username: quach
		  ```
	-
- ## Ressourcen
	- **Database**: https://database.ipi.ch/database-client/search
	- **JIRA**: https://issues.ipip.ch/secure/Dashboard.jspa
	- **Nexus**:
	  id:: 673d9735-2f8d-4a08-a424-6ea83787b6bc
	  collapsed:: true
		- https://containers.ipip.ch/#browse/welcome
		- https://repository.ipip.ch/repository/npm-jsr-registry/
-
- ## Others
	- [[LELA Präsi]]
-