tags:: [[taskfile.dev]], [[Dockerfile]], [[LRN-226 Technology Repetition: MaterialUI, Dexie.js, Angular]]

- https://issues.ipip.ch/browse/LRN-229
-
- ## Dockerfile
	- ```dockerfile
	  // builder stage
	  FROM docker.io/library/node:latest as builder
	  
	  ENV NPM_CONFIG_REGISTRY=https://repository.ipip.ch/repository/npm-public/
	  ENV NODE_TLS_REJECT_UNAUTHORIZED=0
	  
	  WORKDIR /build
	  
	  COPY package*.json ./
	  
	  RUN npm install
	  RUN npm install -g @angular/cli
	  
	  COPY . .
	  RUN ng build --configuration production
	  
	  FROM docker.io/sigoden/dufs:latest as dufs
	  
	  WORKDIR /app
	  
	  // kopiert das von ng gebaute Projekt aus dem 
	  // Builder-Image in das Arbeitsverzeichnis /app.
	  COPY --from=builder /build/dist/material-ng-dexie/browser /app
	  
	  ARG GIT_REVISION
	  ENV DENO_DEPLOYMENT_ID=${GIT_REVISION}
	  
	  ARG BUILD_TIME
	  ENV BUILD_TIME=${BUILD_TIME}
	  
	  EXPOSE 5000
	  ENTRYPOINT ["/bin/dufs"]
	  CMD ["--render-try-index", "/app"]
	  ```