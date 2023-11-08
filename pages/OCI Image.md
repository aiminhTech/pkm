tags:: OCI, [[Container Image]]

- [Understanding container images - OCI image specification · Ravikanth Chaganti](https://ravichaganti.com/blog/2022-10-28-understanding-container-images-oci-image-specification/)
- ## Image Specification
  :LOGBOOK:
  CLOCK: [2023-09-05 Tue 13:44:23]
  :END:
	- Contains an image index, image manifest, a set of file system layers, and a configuration.
	- ![image.png](../assets/image_1693914342614_0.png)
- ## Image index
	- an index of manifests that point to images for different platforms / architectures.
	- ```
	  {
	    "schemaVersion": 2,
	    "manifests": [
	      {
	        "mediaType": "application/vnd.oci.image.manifest.v1+json",
	        "digest": "sha256:30a76a4a2be556c8ff8cff68a3e6a68656a2e2272329b3d4eac5a90072929f7c",
	        "size": 657
	      }
	    ]
	  }
	  ```
	- For each manifest representing a container image, the `mediaType` will be set to `application/vnd.oci.image.manifest.v1+json`.
	- Note: OCI image specification can also be used to package non-container 
	  image artifact types. We will learn about it another day.
- ### Image manifest
	- Contains references to the image configuration JSON and a set of file system layers used to create the image
	- ```
	  {
	    "schemaVersion": 2,
	    "config": {
	      "mediaType": "application/vnd.oci.image.config.v1+json",
	      "digest": "sha256:8b895fab1ad99d2ce5a24b59e3029741fa14d80a98e42cbe352ebea2f64b4446",
	      "size": 1268
	    },
	    "layers": [
	      {
	        "mediaType": "application/vnd.oci.image.layer.v1.tar+gzip",
	        "digest": "sha256:3e6080001d7b2e588ba7bd7c83b4fe5cdc389c5619525db7f24656198f7d44ab",
	        "size": 2916043
	      },
	      {
	        "mediaType": "application/vnd.oci.image.layer.v1.tar+gzip",
	        "digest": "sha256:da30198d6af810de0ead95a824b42b1748f62816bcb0486d9b60090c70e02759",
	        "size": 114
	      },
	      {
	        "mediaType": "application/vnd.oci.image.layer.v1.tar+gzip",
	        "digest": "sha256:5b5387c8849f2140efd643840a2af9829f0616cba8516bc3b01e67529a80406b",
	        "size": 145
	      }
	    ]
	  }
	  ```
	- The contents of an image manifest are specific to a platform and OS version