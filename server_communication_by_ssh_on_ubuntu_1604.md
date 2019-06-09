# Server Communication by SSH on Ubuntu 16.04

> Server1 <-> Server 2

# On Client (Server 1) 

1. Generate Keypairs

> ssh-keygen [-b bits-length (default 2048)] -t algorithm-type [-f output-file-name]

```
$ ssh-keygen -b 2048 -t rsa -f ~/.ssh/api-key
```

2. Change file permission 
```
$ chmod 600 ~/.ssh/api-key
$ chmod 644 ~/.ssh/api-key.pub
```

3. Copy public key file to Remote Server

> scp [original-file] [remote-user]@[remote-server]:

```
$ scp ~/.ssh/api-key.pub myuser@192.168.1.2:
```
