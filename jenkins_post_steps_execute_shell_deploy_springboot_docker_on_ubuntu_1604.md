# Jenkins post steps execute shell for deploy Spring-boot Docker on Ubuntu 16.04 

# 1. Set SSH 

See on [Server Communication by SSH on Ubuntu 16.04](server_communication_by_ssh_on_ubuntu_1604.md)

# 2. MOVE SSH private key file to $JENKINS_HOME 
```
$ mv ~/.ssh/ ~/jenkins/jenkins_home
```
Jenkins home from [Install Docker Jenkins on Ubuntu 16.04](install_docker_jenkins_on_ubuntu_1604.md)

# 3. Set Command

### 3.1 Run SonarQube 
```
$ mvn sonar:sonar -Dsonar.host.url=http://<SONARQUBE_SERVER>:9000  -Dsonar.login=<SONARQUBE_USER_TOKEN>
```
### 3.2 Create deploy folder
```
$ ssh -i $JENKINS_HOME/api-key \
-o StrictHostKeyChecking=no <REMOTE_USER>@<REMOTE_SERVER> \
'mkdir -p ~/deploy/project/target'
```

### 3.3 Copy .jar and Dockerfile to remote server 


