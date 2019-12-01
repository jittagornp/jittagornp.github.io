# Install Docker Registry

### Required
- domain name for map to this instance 

### 1. Install Docker 
### 2. Install Registry

2.1  define username & password

```shell
$ mkdir /auth && touch /auth/htpasswd
$ docker run \
         --entrypoint htpasswd \
         registry:2.6.2 -Bbn {USERNAME} {PASSWORD} > /auth/htpasswd
 $ cat /auth/htpasswd
```

2.2 run registry
```shell
$ docker run -d \
         --restart=always \
         --name privateregistry \
         -v /auth:/auth \
         -e "REGISTRY_AUTH=htpasswd" \
         -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm" \
         -e REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd \
         -v /mnt/registry:/var/lib/registry \
         -p 80:5000 \
         registry:2.6.2
```
2.3 test login
```shell
$ docker login {DOMAIN_NAME} -u {USERNAME}

> password: 
```

2.4 test logout
```shell 
$ docker logout {DOMAIN_NAME}
```
