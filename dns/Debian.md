# Install
```
apt install bind9 -y
```
### /etc/bind/named.conf.default-zones
```
zone "angulema.fun" IN {
        type master;
        file "/etc/bind/angulema.fun.db";
};

zone "121.168.192.in-addr.arpa" IN {
        type master;
        file "/etc/bind/121.168.192.in-addr.arpa.db";
};
```
### /etc/bind/named.conf.options
```
options {
	  directory "/var/cache/bind";
	  listen-on port 53 { 127.0.0.1; 192.168.121.20; };
          allow-query       { 192.168.121.0/24; };
          forwarders        { 8.8.8.8; };
          recursion         yes;
          dnssec-validation no;
	  listen-on-v6 { none; };
};

```
### /etc/bind/angulema.fun.db
```
$TTL    604800
@    	IN 	SOA     node02.angulema.fun. admin.angulema.fun. (
        2      
        10800          
        3600          
        604800          
        604800          
)
	IN	NS	node02.angulema.fun.

node01	IN	A	192.168.121.10
node02	IN	A	192.168.121.20
node03	IN	A	192.168.121.30
```
### /etc/bind/121.168.192.in-addr.arpa.db
```
$TTL    604800
@       IN  SOA     node01.angulema.fun. admin.angulema.fun. (
        2017082401      
        10800          
        3600          
        604800          
        604800          
)
        IN	NS	node01.angulema.fun.

10	IN	PTR	node01.angulema.fun.
20	IN	PTR	node02.angulema.fun.
30	IN	PTR	node03.angulema.fun.

```
