# Install Docker Kong With External Postgresql on Ubuntu 16.04 

# Create Network

```
$ docker network create kong-net 
```

# Kong Migrate Data To External Postgresql  
```
$ docker run --rm  \
--network=kong-net \
-e "KONG_DATABASE=postgres" \
-e "KONG_PG_HOST=<DATABASE_HOST>" \
-e "KONG_PG_USER=<DATABASE_USERNAME>" \
-e "KONG_PG_PASSWORD=<DATABASE_PASSWORD>" \
-e "KONG_PG_PORT=<DATABASE_PORT>" \
-e "KONG_PG_SCHEMA=<DATABASE_SCHEMA>" \
-e "KONG_PG_SSL=on" \
kong:latest kong migrations bootstrap
```
# Start Kong
```
$ docker run -d --name kong \
     --network=kong-net \
     -e "KONG_DATABASE=postgres" \
     -e "KONG_PG_HOST=<DATABASE_HOST>" \
     -e "KONG_PG_USER=<DATABASE_USERNAME>" \
     -e "KONG_PG_PASSWORD=<DATABASE_PASSWORD>" \
     -e "KONG_PG_PORT=<DATABASE_PORT>" \
     -e "KONG_PG_SCHEMA=<DATABASE_SCHEMA>" \
     -e "KONG_PG_PORT=<DATABASE_PORT>" \
     -e "KONG_PG_SSL=on" \
     -e "KONG_PROXY_ACCESS_LOG=/dev/stdout" \
     -e "KONG_ADMIN_ACCESS_LOG=/dev/stdout" \
     -e "KONG_PROXY_ERROR_LOG=/dev/stderr" \
     -e "KONG_ADMIN_ERROR_LOG=/dev/stderr" \
     -e "KONG_ADMIN_LISTEN=0.0.0.0:8001, 0.0.0.0:8444 ssl" \
     -p 80:8000 \
     -p 443:8443 \
     -p 39021:8001 \
     -p 39424:8444 \
     kong:latest
```

# Reference

- [https://hub.docker.com/_/kong](https://hub.docker.com/_/kong)
- [https://docs.konghq.com/1.1.x/configuration/#postgres-settings](https://docs.konghq.com/1.1.x/configuration/#postgres-settings)
