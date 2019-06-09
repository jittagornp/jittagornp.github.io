# Install Docker on Ubuntu 16.04 (LTS) 

> Docker version 18.09.6, build 481bc77  

1. Delete Old Version  
```
$ sudo apt-get remove docker docker-engine docker.io containerd runc
```

2. Update package  
```
$ sudo apt-get update
```

3. Install package `apt` to use a repository over HTTPS:
```
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```

4. Add GPG Key 
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

5. Verify Fingerprint
```
$ sudo apt-key fingerprint 0EBFCD88
```

6. Add apt docker  
```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

7. Update Package Index
```
$ sudo apt-get update  
```

8. Install Docker
```
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

9. Check version
```
$ sudo docker --version
```

10. Hello World  
```
$ sudo docker run hello-world
```
