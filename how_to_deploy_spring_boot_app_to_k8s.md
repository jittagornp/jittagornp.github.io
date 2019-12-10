# How to deploy spring boot application to Kubernetes (K8S)
- application name `oauth`
- docker registry url `registry.mywebsite.com`

### 1. Create deployment file 

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

2. Create Docker Registry Secret
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
