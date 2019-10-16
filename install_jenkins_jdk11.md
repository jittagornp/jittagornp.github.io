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
  --name jenkins \ 
  --restart=always \ 
  -p 80:8080 \
  -p 50000:50000 \
  -v ~/jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v $(which docker):/usr/bin/docker \  
  jenkins/jenkins:jdk11
  ```
  
  # Run Pipeline
  
 error
```
....
....docker.sock: connect: permission denied
...
```
quick fix : but not secure, run command
```shell
$ sudo chmod 777 /var/run/docker.sock
```
