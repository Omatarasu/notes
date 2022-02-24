```
dnf install dhcp-server -y
```
> install centOS
```
setenforce 0
```
### /etc/selinux/config
```
SELINUX=permissive
```
> disable selinux
```
systemctl disable --now firewalld 
```
> disable firewall
### /etc/dhcp/dhcpd.conf (master)
```
failover peer "my-failover" {
	primary;                          # main server
	address 192.168.100.10;           # server address
	port 519;                         # listen port 

	peer address 192.168.100.20;      # slave server address
	peer port 520;                    # slave server port

	max-response-delay 30;            # dead-interval
	max-unacked-updates 10;           # some meed parameter
	load balance max seconds 3;       # some need parameter 
        split 128;                        # balance 50/50
        mclt 1800;                        # some parameter
}


option domain-name "angulema.fun";            # domain search 
option domain-name-servers 192.168.100.1;     # dns servers

default-lease-time 604800;                    # 7 days lease
max-lease-time 2419200;                       # 4 weeks max lease

include "/etc/dhcp/dhcpd.d/subnet01.conf";    # file with subnet configs
```
### /etc/dhcp/dhcpd.conf (slave)
```
failover peer "my-failover" {
	secondary;                        # slave server
	address 192.168.100.20;           # server address
	port 520;                         # listen port 

	peer address 192.168.100.10;      # master server address
	peer port 519;                    # master server port

	max-response-delay 30;            # dead-interval
	max-unacked-updates 10;           # some meed parameter
	load balance max seconds 3;       # some need parameter 
}
option domain-name "angulema.fun";            # domain search 
option domain-name-servers 192.168.100.1;     # dns servers

default-lease-time 604800;                    # 7 days lease
max-lease-time 2419200;                       # 4 weeks max lease

include "/etc/dhcp/dhcpd.d/subnet01.conf";    # file with subnet configs
```
### /etc/dhcp/dhcpd.d/subnet01.conf (any server) 
```
subnet 192.168.100.0 netmask 255.255.255.0 {
	option routers 192.168.100.1;                     # default gateway
	pool {
		failover peer "my-failover";                  # use fileover
		range 192.168.100.120 192.168.100.200;        # address range
	}
}
```
