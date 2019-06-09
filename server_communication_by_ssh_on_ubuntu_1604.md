# Server Communication by SSH on Ubuntu 16.04

> `Server1` communicate with `Server 2`

# On Client (Server 1) 

### 1. Generate Keypairs

> ssh-keygen [-b bits-length (default 2048)] -t algorithm-type [-f output-file-name]

```
$ ssh-keygen -b 2048 -t rsa -f ~/.ssh/api-key
```

thare are 2 files created in ~/.ssh which contains 
- api-key
- api-key.pub

### 2. Change file permission 
```
$ chmod 600 ~/.ssh/api-key
$ chmod 644 ~/.ssh/api-key.pub
```

### 3. Copy public key file to Remote Server

> scp [original-file] [remote-user]@[remote-server]:

```
$ scp ~/.ssh/api-key.pub myuser@192.168.1.2:
```
enter `myuser` password 

- it will copy public key file to home directory of `myuser`  

# On Remote Server (Server 2)

### 1. Append public file to `authorized_keys`
```
$ cat ~/api-key.pub >> ~/.ssh/authorized_keys
```
### 2. Change file permission

```
$ chmod 644 ~/.ssh/authorized_keys
```

# Back to Client (Server 1)

### Test connect to Server 2 

```
$ ssh -i ~/.ssh/api-key myuser@192.168.1.2
```
