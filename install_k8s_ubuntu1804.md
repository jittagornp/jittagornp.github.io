# Install Kubernetes (On-Premise) on Ubuntu 18.04

> TODO

# Environments
- Linux Ubuntu 18.04
- Nodes
```
master node : 10.130.38.189
worker node1 : 10.130.38.192
worker node2 : 10.130.38.200
```

# All Nodes

1) [Install Docker CE](install_docker_on_ubuntu_1804.md)
2) turnoff swap
```
$ sudo swapoff -a
$ sudo vi /etc/fstab  
```
then comment this line
```
#/swap.img  none    swap    sw  0    0 
```
3) update and install apt-transport-https  
```
$ sudo apt-get update
$ sudo apt install -y apt-transport-https
```
4) add ap-key 
```
$ curl -s \
    https://packages.cloud.google.com/apt/doc/apt-key.gpg |\
    sudo apt-key add -
```
