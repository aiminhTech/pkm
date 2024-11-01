tags:: [[IGE]], [[OpenShift]], [[Jenkins]], [[Nexus]], [[Hashicorp Vault]]

- Projektablage (private git repo vs offizielles Projekt)
- Anpassung des
    openshift/build.sh templates
- Zwei OCI Images / Zwei
    OpenShift Deployments
- Jenkins Jobs: on commit deployment für Abnahme / manuelles
    deployment für Produktion
- Konfiguration der S3 und
    Elastic Credentials für Abnahme und Produktion
- ## Guildelines
	- [OCI Image Guidelines](https://wiki.ipip.ch/display/SWE/OCI+Image+Guidelines)
	- [Openshift Guildelines](https://wiki.ipip.ch/display/SWE/Openshift+Guidelines)
- ## Openshift Entwicklungsprozess
- ## Template Repository für OCI Images und Openshift
	- **Bitbucket:** https://git.ipip.ch/projects/OPS/repos/openshift/browse
- ## Deployment für Applikationen via Ansible #Ansible
	- This is the Git repo where we place Ansible playbooks to configure our applications
	- **Project path wks:** `/ige/jp/ops/ansible-apps`
	- **Bitbucket:** https://git.ipip.ch/projects/OPS/repos/ansible-apps/browse
	-
- Weiteres Vorgehen besprechen