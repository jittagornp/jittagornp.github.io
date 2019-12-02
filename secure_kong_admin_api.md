# Secure Kong Admin API

### 1. add `key-auth` plugin

Http post : `http://<KONG_HOST>:<ADMIN_PORT>/plugins`  
Headers 
```
ContentType : application/json
```
Body   
```json
{
	"name" : "key-auth",
	"config" : {
		"key_names" : ["apikey"]
	}
}
```
