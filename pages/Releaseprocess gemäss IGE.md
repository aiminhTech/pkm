tags:: [[IGE]], [[OpenShift]], [[Jenkins]], [[Nexus Repository]], [[Hashicorp Vault]], [[Ansible]]

-
- ## Template Repository für OCI Images und Openshift
	- **Guidelines:** [OCI Image Guidelines](https://wiki.ipip.ch/display/SWE/OCI+Image+Guidelines)
	- **Bitbucket:** https://git.ipip.ch/projects/OPS/repos/openshift/browse
- ## Deployment für Applikationen via #Ansible
	- **Guidelines:** [Openshift Guidelines](https://wiki.ipip.ch/display/SWE/Openshift+Guidelines)
	- **Project path wks:** `/ige/jp/ops/ansible-apps`
		- test cmd: `ipi-ansible-playbook -i inventories/entwicklung/ -p process_archive_viewer`
		  id:: 67593df3-8891-4867-9277-4944b57c2b60
	- **Bitbucket:** https://git.ipip.ch/projects/OPS/repos/ansible-apps/browse
- ## Realeasprocess
	- ### Repository publizieren
		- Das Git- Repo offiziell machen, mit 2 Branches `develop` und `master`.
			- `develop`-Branch wird für die Entwicklung und das Testen neuer Features genutzt.
			- `master`-Brand wird wird für stabile und freigegebene Versionen des Projekts verwendet. Dieser Branch enthält geprüften und fehlerfreien Code, der bereit für den Einsatz in Produktionsumgebungen ist. Änderungen in diesem Branch erfolgen in der Regel durch Merge-Requests aus dem `develop`-Branch, sobald diese vollständig getestet und validiert wurden.
	- ### OCI-Image generieren
		- Build-Image mithilfe von `build.sh` gemäss dem Template des IGE erstellen.
	- ### Jenkins Jobs
	- ### Integration in Ansible-Apps
		- Die Integration in Ansible-Apps erstellen (playbook, inventories und andere notwendigen Komponente)
-
- ## Release Versionierung
	- {{embed [[Semantische Versionierung]]}}