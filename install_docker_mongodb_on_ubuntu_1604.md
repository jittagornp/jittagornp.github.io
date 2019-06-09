# Install Docker Mongodb on Ubuntu 16.04 

1. Create folder for mount to data of Mongodb 
```
$ cd ~
$ mkdir mongodb
```

2. Install Mongodb
```
$ docker run -d --name mongodb --restart=always -v ~/mongodb/data/db:/data/db -p 27017:27017 mongo:latest --auth
```

3. Execute Mongo command for connect to admin database
```
$ docker exec -it mongodb mongo admin
```

4. Create user admin on admin database  
```
> db.createUser({
  user: "admin", 
  pwd: "secure", 
  roles: [ { role: "root", db: "admin" } ]
})
```

5. Show users on current database (admin)
```
> db.getUsers()
```

6. Test authen by admin
```
> db.auth("admin","secure")
```

7. Create new database (change database)
```
> use mydb 
```

8. Create new user on mydb database
```
> db.createUser({
  user: "test", 
  pwd: "123456", 
  roles: [ { role: "dbOwner", db: "mydb" } ]
})
```

9. Show users on current database (mydb)
```
> db.getUsers()
```

10. Test authen by test on current database (mydb)
```
> db.auth("test","123456")
```

11. Drop user on current database (mydb)
```
> db.dropUser("test")
```

12. Exit mongodb command
```
> exit 
```
