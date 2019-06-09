  
# Install Java on Ubuntu 16.04

1. Install the OpenJDK 8 from a PPA repository 
```
$ sudo add-apt-repository ppa:openjdk-r/ppa
```

2. Update the system package cache and install 
```
$ sudo apt-get update
$ sudo apt-get install openjdk-8-jdk
```

3. If you have more than one Java version installed on your system use the following command to switch versions
```
$ sudo update-alternatives --config java 
```

4. Make sure your system is using the correct JDK 
```
$ java -version
```

# Reference

https://docs.datastax.com/en/cassandra/3.0/cassandra/install/installOpenJdkDeb.html 
