# Jenkins post steps execute shell for deploy Spring-boot Docker on Ubuntu 16.04 

# 1. Set SSH 

See on [Server Communication by SSH on Ubuntu 16.04](server_communication_by_ssh_on_ubuntu_1604.md)

# 2. MOVE SSH private key file to $JENKINS_HOME 
```
$ mv ~/.ssh/<PRIVATE_KEY_FILE> ~/jenkins/jenkins_home
```
Jenkins home from [Install Docker Jenkins on Ubuntu 16.04](install_docker_jenkins_on_ubuntu_1604.md)

# 3. Set Command

### 3.1 Run SonarQube 
```
mvn sonar:sonar -Dsonar.host.url=http://<SONARQUBE_SERVER>:9000  -Dsonar.login=<SONARQUBE_USER_TOKEN>
```
### 3.2 Create deploy folder on remote server 
```
ssh -i $JENKINS_HOME/<PRIVATE_KEY_FILE> \
-o StrictHostKeyChecking=no <REMOTE_USER>@<REMOTE_SERVER> \
'mkdir -p ~/deploy/<PROJECT_NAME>/target'
```

### 3.3 Copy .jar and Dockerfile to remote server 

Copy .jar
```
scp -i $JENKINS_HOME/<PRIVATE_KEY_FILE> \
-o StrictHostKeyChecking=no \
$JENKINS_HOME/workspace/<PROJECT_NAME>/target/*.jar \
<REMOTE_USER>@<REMOTE_SERVER>:~/deploy/<PROJECT_NAME>/target 
```

Copy Dockerfile
```
scp -i $JENKINS_HOME/<PRIVATE_KEY_FILE> \
-o StrictHostKeyChecking=no \
$JENKINS_HOME/workspace/<PROJECT_NAME>/Dockerfile \
<REMOTE_USER>@<REMOTE_SERVER>:~/deploy/<PROJECT_NAME>
```

### 3.4 Stop and Remove container

```
ssh -i $JENKINS_HOME/<PRIVATE_KEY_FILE> \
-o StrictHostKeyChecking=no \
<REMOTE_USER>@<REMOTE_SERVER> \
'docker rm $(docker stop $(docker ps -a -q --filter ancestor=<DOCKER_IMAGE_NAME> --format="{{.ID}}"))'
```
