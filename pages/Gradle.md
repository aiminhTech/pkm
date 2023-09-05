tags:: [[Java]]

- https://gradle.org/
- Gradle is a build automation tool known for its flexibility to build software
- A build automation tool is used to automate the creation of applications. The building process includes compiling, linking, and packaging the code. The process becomes more consistent with the help of
   build automation tools.
- [Gradle Tutorial For Beginners](https://www.simplilearn.com/tutorials/gradle-tutorial)
- ## Installation Ubuntu
	- ```
	  sudo apt update
	  cd /tmp
	  wget https://services.gradle.org/distributions/gradle-8.3-bin.zip
	  unzip gradle-8.3-bin.zip
	  mv gradle-8.3 /opt/gradle
	  sudo ln -s /opt/gradle/bin/gradle /usr/bin/gradle
	  gradle --version
	  ```