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
  pwd: "<ADMIN_PASSWORD>", 
  roles: [ { role: "root", db: "admin" } ]
})
```

5. Show users on current database (admin)
```
> db.getUsers()
```

6. Test authen by admin
```
> db.auth("admin","<ADMIN_PASSWORD>")
```

7. Create new database (change database)
```
> use <NEW_DATABASE> 
```

8. Create new user on <NEW_DATABASE> database
```
> db.createUser({
  user: "<NEW_USERNAME>", 
  pwd: "<NEW_PASSWORD>", 
  roles: [ { role: "dbOwner", db: "<NEW_DATABASE>" } ]
})
```

9. Show users on current database (<NEW_DATABASE>)
```
> db.getUsers()
```

10. Test authen by <NEW_USERNAME> on current database (<NEW_DATABASE>)
```
> db.auth("<NEW_USERNAME>","<NEW_PASSWORD>")
```

11. Drop user on current database (<NEW_DATABASE>)
```
> db.dropUser("<NEW_USERNAME>")
```

12. Exit mongodb command
```
> exit 
```
