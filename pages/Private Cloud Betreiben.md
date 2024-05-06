## Cloud nutzen
	- ### compose
	- ### deploy
- ## Infrastructure as Code
	- https://en.wikipedia.org/wiki/Infrastructure_as_code
	- {{video https://www.youtube.com/watch?v=zWw2wuiKd5o}}
	- Infrastructure as Code (IaC) bedeutet im Grunde, die Konfiguration und Bereitstellung von IT-Infrastruktur (Server, Netzwerke, Datenbanken, etc.) mithilfe von Code zu automatisieren, anstatt dies manuell zu tun. Statt jeden Schritt der Infrastruktur-Einrichtung von Hand durchzuführen, wird der gesamte Prozess in Code geschrieben und automatisch ausgeführt.
	- ### Methodiken
		- #### Deklarativ
		  collapsed:: true
			- ```Terraform-File
			  resource "azurerm_windows_virtual_machine" {
			   name = "vm01"
			   resource_group_name = “resgroup”
			   admin_username = "azureadmin” 
			   
			  network_interface_ids = [
			   azurerm_network_interface.0.id,
			   ]
			  
			  source_image_reference {
			   publisher = "MicrosoftWindowsServer"
			   offer = "WindowsServer"
			   sku = "2022-Datacenter"
			   version = "latest"
			   } 
			  } 
			  ```
		- #### Imperativ
		  collapsed:: true
			- ```Azure CLI
			  az vm create \ 
			   --resource-group resgroup \ 
			   --name vm01 \ 
			   --image Win2022AzureEditionCore \ 
			   --public-ip-sku Standard \ 
			   --admin-username azureadmin 
			  ```
	- ### Konfigurationsmanagement-Tools
		- versuchen ein möglichst grosses Spektrum an Cloudlösungsanbieter über eine einheitliche Schnittstelle (APIs) anzusprechen.
		- Infrastrukturanpassungen lassen sich damit sehr einfach auch über verschiedene Anbieter hinweg nutzen.
		- Die Konfigurationen werden bei den meisten Tools über standardisierte Template-Formate wie z.B. JSON oder YAML festgelegt.
		- In der Praxis werden oft mehrere Tools gemeinsam verwendet.
		- Beispiele von Konfigurationsmanagement-Tools:
			- Ansible
			- Terraform
			- Chef
			- Puppet
			- SaltStack