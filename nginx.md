### /etc/nginx/conf.d/https.conf
```
upstream backend {
	server 192.168.121.20:80;
	server 192.168.121.30:80;
}

server {
    listen		443 ssl;
    server_name		www.angulema.fun;
    ssl_certificate	/etc/nginx/certs/www.angulema.fun.crt;
    ssl_certificate_key	/etc/nginx/certs/www.angulema.fun.key;
    
    location / {
        proxy_pass http://backend; 
    }
}
```
> Also need add firewall rule and disable default nginx page
