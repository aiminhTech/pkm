- https://logseq.com/
- ## Locations
- **macos** : `~ /icloud/logseq/grahps/pkm`
	- automatically sync with iphone
- **acer**: `~ /pkm`
- **ige wks**: `C:/ige/pkm`
  id:: 664c6765-4e0b-408b-8918-5cf42e209865
	- $env:https_proxy="http://www-proxy.ipip.ch:8080"
- ## Videos
  collapsed:: true
	- {{youtube https://www.youtube.com/watch?v=cy5A-_S1bnU}}
	- {{youtube  https://www.youtube.com/watch?v=qtN7qqdeTwU}}
	- {{youtube  https://www.youtube.com/watch?v=fhwn3m7pZzw}}
	- {{youtube https://www.youtube.com/watch?v=Fnxq3iITAJk}}
	-
- ## WKS
  collapsed:: true
	- ### Download Windows ZIP
		- ``` powershell
		  $res = Invoke-RestMethod `-Uri
		  'https://api.github.com/repos/logseq/logseq/releases/latest' `
		  -Headers @{"Accept" = "application/vnd.github+json" }
		  
		  $zipUrl = $res.assets |
		  
		  Where-Object {$_.name.EndsWith(".zip") -and $_.name.Contains("-win-x64")} |
		  Select-Object -ExpandPropertybrowser_download_url
		  Invoke-RestMethod -UserAgent 'curl/8.4.0' -Uri $zipUrl -OutFile
		  logseq.zip
		  
		            
		  # TODO rename existing C:\ige\logseq to C:\ige\logseqOLD and
		  unzip logseq.zip to C:\ige\logseq\
		  
		              
		  ```
	- ### Start  
	  ``` powershell
	  $env:NODE_TLS_REJECT_UNAUTHORIZED=0
	              
	  C:\ige\logseq\Logseq.exe
	  ```
- ## Plugins
  collapsed:: true
	- `~/.logseq/plugins`
	- ``` 
	  logseq-block-to-page
	  logseq-bullet-threading
	  logseq-journals-calendar  	
	  ```
-