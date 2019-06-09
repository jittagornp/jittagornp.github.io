# Install Docker Jenkins on Ubuntu 16.04 

1. Create jenkins folder
```
$ cd ~
$ mkdir jenkins
$ chmod 777 jenkins
```

2. install docker 
```
$ docker run -d -p 80:8080 -p 50000:50000 -v ~/jenkins/jenkins_home:/var/jenkins_home -u root jenkins/jenkins:lts
```
