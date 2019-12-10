# How to deploy java spring boot application to Kubernetes (K8S)

### Required

- [Setup Private Docker Registry](install_docker_registry.md)  
- [Write Java Spring-boot Application](https://github.com/jittagornp/spring-boot-webflux-example/tree/master/spring-boot-webflux-dockerfile) then push image to private registry  
- [Setup K8S Cluster](install_k8s_ubuntu1804.md)  

### Information  
- application name `oauth`
- docker registry url `registry.mywebsite.com`

### 1. Create Private Docker Registry Secret on Master Node
format
```sh
$ kubectl create secret docker-registry <DOCKER_REGISTRY_ID> \
--docker-server=<DOCKER_REGISTRY_URL> \
--docker-username=<DOCKER_REGISTRY_USERNAME> \
--docker-password=<DOCKER_REGISTRY_PASSWORD> \
--docker-email=<DOCKER_REGISTRY_EMAIL>
```
run
```sh
$ kubectl create secret docker-registry my-docker-registry \
--docker-server=http://registry.mywebsite.com \
--docker-username=my_docker_account \
--docker-password=WGTSU5V22cEYW9f \
--docker-email=myemail@gmail.com
```

### 2. Create ConfigMap on Master Node

2.1 create .env file  
oauth.env  
```properties
JAVA_OPTS=-Djava.security.egd=file:/dev/./urandom -Dserver.port=8080 -Dspring.redis.url=redis://.....
```
2.2 run command to create config maps from .env file 
```sh
$ kubectl create configmap oauth-config --from-env-file=/deploy/oauth.env
```
2.3 show configmap as .yaml
```sh
$ kubectl get configmap oauth-config -o yaml
```


### 3. Deploy on Master Node

3.1 create deployment file  
deployment.yml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app.kubernetes.io/name: oauth
  name: oauth
spec:
  replicas: 2
  selector:
    matchLabels:
      app.kubernetes.io/name: oauth
  template:
    metadata:
      labels:
        app.kubernetes.io/name: oauth
    spec:
      containers:
      - name: oauth
        image: registry.mywebsite.com/oauth:latest 
        imagePullPolicy: Always  
        envFrom:
          - configMapRef:
              name: oauth-config
        ports:
        - containerPort: 8080
        volumeMounts:
        - mountPath: /logs
          name: log-volume
      imagePullSecrets:
      - name: my-docker-registry    
      volumes:
      - name: log-volume
        hostPath:
          path: /logs
          type: DirectoryOrCreate 

```
service.yml
```yaml
apiVersion: v1
kind: Service
metadata:
  name: oauth
  labels:
    app.kubernetes.io/name: oauth
spec:
  type: NodePort
  ports:
    - port: 8080
      nodePort: 30001
      name: http
  selector:
    app.kubernetes.io/name: oauth
```

3.2 run command for deploy
```sh
$ kubectl apply -f deployment.yml  
$ kubectl apply -f service.yml  
```

# Note

docker file for create java spring-boot application image
```Dockerfile
# Use official base image of Java Runtim
FROM openjdk:11-jdk

# Set volume point to /tmp
VOLUME /tmp

# Make port 8080 available to the world outside container
EXPOSE 8080

# Set application's JAR file
ARG JAR_FILE=target/*.jar

# Add the application's JAR file to the container
ADD ${JAR_FILE} app.jar

# Run the JAR file
ENTRYPOINT java $JAVA_OPTS -jar /app.jar
```
