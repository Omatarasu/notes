# Install
```
dnf install bind -y
```
### /etc/named.conf
```
options {
        listen-on port 53 { 127.0.0.1; 192.168.121.10; };
        allow-query       { 192.168.121.0/24; };
        forwarders        { 8.8.8.8; };
        recursion         yes;
        dnssec-enable     no;
        dnssec-validation no;
        ...
}

zone "angulema.fun" IN {
        type master;
        file "/etc/named/angulema.fun.db";
};

zone "121.168.192.in-addr.arpa" IN {
        type master;
        file "/etc/named/121.168.192.in-addr.arpa.db";
};
```
### /etc/named/angulema.fun.db
```
$TTL    604800
@    	IN 	SOA     node01.angulema.fun. admin.angulema.fun. (
        2      
        10800          
        3600          
        604800          
        604800          
)
@	IN	NS	node01.angulema.fun.

node01	IN	A	192.168.121.10
node02	IN	A	192.168.121.20
node03	IN	A	192.168.121.30
```
### /etc/named/121.168.192.in-addr.arpa.db
```
$TTL    604800
@       IN  SOA     node01.angulema.fun. admin.angulema.fun. (
        2017082401      
        10800          
        3600          
        604800          
        604800          
)
@       IN	NS	node01.angulema.fun.

10	IN	PTR	node01.angulema.fun.
20	IN	PTR	node02.angulema.fun.
30	IN	PTR	node03.angulema.fun.
```
