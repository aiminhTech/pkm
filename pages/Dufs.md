- https://github.com/sigoden/dufs
  title:: Dufs
- Dufs is a distinctive utility file server that supports static serving, uploading, searching, accessing control, webdav...
-
- ## Installation
	- ### docker
	- ``docker run -v `pwd`:/data -p 5000:5000 --rm sigoden/dufs /data -A``
- ## Usage
	- Serve current working directory in read-only mode
		- ```
		  dufs
		  ```
	- Allow all operations like upload/delete/search/create/edit...
		- ```
		  dufs -A
		  ```
-