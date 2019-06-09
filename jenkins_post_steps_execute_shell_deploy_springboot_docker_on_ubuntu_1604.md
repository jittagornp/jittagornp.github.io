# Jenkins post steps execute shell for deploy Spring-boot Docker on Ubuntu 16.04 

### 1. Set SSH 

See on [Server Communication by SSH on Ubuntu 16.04](server_communication_by_ssh_on_ubuntu_1604.md)

### 2. Set Command

Run sonarqube 
```
$ mvn sonar:sonar -Dsonar.host.url=http://10.130.138.66:9000  -Dsonar.login=<SONARQUBE_USER_TOKEN>
```
