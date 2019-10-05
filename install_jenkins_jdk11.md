# Install Jenkins JDK 11    

1. make directory 
```shell
$ cd ~   
$ mkdir jenkins_home
```

2. set priority
```shell
$ chmod 777 jenkins_home
```

3. run docker 
```shell  
$ docker run -d \
  -p 80:8080 \
  -p 50000:50000 \
  -v ~/jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  jenkins/jenkins:jdk11  
  ```
