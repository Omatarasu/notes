```
apt install isc-dhcp-server -y
```
> install dhcp server
### /etc/default/isc-dhcp-server 
```
INTERFACESv4="enp1s0"
```
> dhcp interface
### /etc/dhcp/dhcpd.conf
```
option domain-name "angulema.fun";
option domain-name-servers 192.168.77.10;

default-lease-time 600;
max-lease-time 7200;

subnet 192.168.77.0 netmask 255.255.255.0 {
    range 192.168.77.30 192.168.77.50;
    option routers 192.168.77.1;
}
```
> easy config for dhcp 
```
systemctl enable --now isc-dhcp-server.service
systemctl restart isc-shcp-server.service
```
> restart service
### /etc/dhcp/dhcpd.conf
```
...
host dhcp01 {
    hardware ethernet 52:54:00:8e:2f:e7;
    fixed-address 192.168.77.5;
}
```
> fixed mac address
```

```
