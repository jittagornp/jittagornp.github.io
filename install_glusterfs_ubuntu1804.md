# Install GlusterFS on Ubuntu 18.04 

# Envioments

- Linux Ubuntu 18.04    
- Node  
```
1. client node :   
2. glusterfs-node1 : 10.130.15.87
3. glusterfs-node2 : 10.130.117.8    
```

# On glusterfs-node1 & glusterfs-node2 

1) edit `/etc/hosts`
```
$ vi /etc/hosts
```
add configs
```
10.130.15.87 glusterfs-node1
10.130.117.8 glusterfs-node2
```
2) install software-properties-common  
```
$ sudo apt install software-properties-common -y
```
3)  download glusterfs public-key  
```
$ wget -O- https://download.gluster.org/pub/gluster/glusterfs/6/rsa.pub | apt-key add -  
```
4) add repository
```
$ sudo add-apt-repository ppa:gluster/glusterfs-6  
```
5) install glusterfs 
```
$ sudo apt install glusterfs-server -y
```
6) start glusterfs service
```
$ sudo systemctl start glusterd
```
7) enabled run everytime at system boot 
```
$ sudo systemctl enable glusterd
```
8) show glusterfs status
```
$ systemctl status glusterd
```
9) show glusterfs version
```
$ glusterfsd --version
```
10) create directory for share in cluster 
```
$ mkdir -p /storage
```
# Only glusterfs-node1
  
1) add server to glusterfs storage pool
```
$ gluster peer probe glusterfs-node2  
```
2) check status
```
$ gluster peer status
```
3) show list 
```
$ gluster pool list  
```
4) create volume (select 4.1 or 4.2)   
  
4.1) replica 
```
$ gluster volume create volume-01 replica 2 transport tcp \
glusterfs-node1:/storage \
glusterfs-node2:/storage \
force
```
4.2) distribute  
```
$ gluster volume create volume-01 transport tcp \
glusterfs-node1:/storage \
glusterfs-node2:/storage \
force
```
> `volume-01` is name of volume   

5) start volume 
```
$ gluster volume start volume-01  
```
6) show volume info  
```
$ gluster volume info volume-01   
```
