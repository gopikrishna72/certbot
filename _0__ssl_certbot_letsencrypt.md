
Directories on host machine:
* `/data/certbot/letsencrypt`
* `/data/certbot/www`



* Nginx server in docker container
```
    -v /data/certbot/letsencrypt:/etc/letsencrypt
    -v /data/certbot/www:/var/www/certbot
```

config file for your site 
```
location '/.well-known/acme-challenge' {
        default_type "text/plain";
        root        /var/www/certbot;
    }
```



* `ssl_update.sh` script
* generates a self-signed certificate
* renew certificates with Let's Encrypt

* update certificates

`ssl_mysite.sh`

```
#!/bin/bash

export CERT_DIR_PATH="/data/certbot/letsencrypt";
export WEBROOT_PATH="/data/certbot/www";
export LE_RENEW_HOOK="docker restart web-nginx-front";
export DOMAINS="mysite.com";
export EMAIL="myemail@gmail.com";
export EXP_LIMIT="30";
export CHECK_FREQ="30";
export CHICKENEGG="1";
export STAGING="0";

bash /data/ssl_update.sh
                  
```




References:
* https://github.com/vdhpieter/docker-letsencrypt-webroot

