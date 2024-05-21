tags:: [[IGE]]

- Side project to learn Deployment with [[OpenShift]], [[docker.io]], [[Podman]]
- ## API Requests
	- ` curl -X GET http://localhost:8000/api/data/${filename}`
	- `curl -X PUT -H "Content-Type: application/json" -d '{"fileName": "example.txt", "content": "This is some contentnnnn."}' http://localhost:8000/api/data`
-