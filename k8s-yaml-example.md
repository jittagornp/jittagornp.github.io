# K8S YAML example 

- application name `oauth`
- docker registry url `registry.pamarin.com`

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
        image: registry.pamarin.com/oauth:latest 
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
      - name: pamarin-registry    
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
