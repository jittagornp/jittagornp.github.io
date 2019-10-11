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
5) create empty file `kubernetes.list`   
```
$ sudo touch /etc/apt/sources.list.d/kubernetes.list
```
6) update file `kubernetes.list`    
```
$ echo \
    "deb http://apt.kubernetes.io/ kubernetes-xenial main" |\
    sudo tee -a /etc/apt/sources.list.d/kubernetes.list
```
7) install kubeadm  
```
$ sudo apt update   
$ sudo apt install -y kubeadm  
```
will install kubeadm, kubectl and kubelet  
8) check
```
$ kubeadm --help
$ kubectl --hetlp 
$ kubelet --help
```
