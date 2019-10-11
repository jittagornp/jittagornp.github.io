# Install Kubernetes on Ubuntu 18.04

> TODO

# Environments
- Linux Ubuntu 18.04
- Nodes
```
master node : 10.130.38.189
worker node1 : 10.130.38.192
worker node2 : 10.130.38.200
```

### All Nodes

1) [Install Docker CE](install_docker_on_ubuntu_1804.md)
2) turnoff swap
```
$ sudo swapoff -a
$ sudo vi /etc/fstab  
```
comment this line
```
#/swap.img  none    swap    sw  0    0 
```
3) 
```
$ sudo apt-get update
```
