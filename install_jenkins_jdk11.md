# Install Jenkins JDK 11    

1. run docker 
```shell  
$ docker run -d \
  -p 80:8080 \
  -p 50000:50000 \
  -v ~/jenkins_home:/var/jenkins_home \
  jenkins/jenkins:jdk11
  ```
2. set priority
```shell
$ cd ~   
$ chmod 777 jenkins_home/
```
