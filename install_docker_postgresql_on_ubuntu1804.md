# Install Docker Postgresql on Ubuntu 18.04 
```shell
$ docker run -d -p 5432:5432 \
--restart=always \
-v /root/postgresql/data:/var/lib/postgresql/data \
-e POSTGRES_USER="<DATABASE_USERNAME>" \
-e POSTGRES_PASSWORD="<DATABASE_PASSWORD>" \
-e POSTGRES_DB="<DEFAULT_DATABASE>" \
--name postgres \
postgres 
```
