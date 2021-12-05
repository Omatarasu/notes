## FILTER
```
nft add table inet filter
```
> create table (inet = both ipv4 and ipv6)
```
nft 'add chain inet filter input {type filter hook input priority 0; policy accept;}'
nft 'add chain inet filter ouptut {type filter hook output priority 0; policy accept;}'
nft 'add chain inet filter forward {type filter hook forward priority 0; policy accept;}'
```
> inet - family, filter - table, input - chain name, policy - default (accept or drop)
```
nft add rule inet filter input tcp dport 22 counter accept
```
> acccept ssh
```
nft add rule inet filter input tcp dport 3260 counter accept
```
> accept iscsi target
```
nft add rule inet filter input ip protocol gre counter accept
```
> accept gre
```
nft add rule inet filter input iifname "lo" counter accept
```
> accept loopback
```
nft add rule inet filter input udp dport 1194 counter accept
```
> allow openvpn
```
nft add 'rule inet filter input udp dport {137,138,139,445} counter accept'
nft add 'rule inet filter input tcp dport {137,138,139,445} counter accept'
```
> allow samba
```
nft add rule inet filter input icmp type echo-request counter accept
```
> accept icmp-requests
```
nft add rule inet filter input ct state established,related counter accept
```
>  accept established and related connections 
## NAT
```
nft add table nat
```
> create nat table
```
nft 'add chain nat postrouting { type nat hook postrouting priority 100 ; }'
```
> SNAT chain create (change destination address)
```
nft 'add chain nat prerouting { type nat hook prerouting priority -100; }'
```
> DNAT chain create (change source address)
```
nft add rule ip nat postrouting ip saddr 192.168.1.0/24 oifname "enp1s0" counter masquerade 
```
> MASQUEARDE chain create (all packages from 192.168.1.0/24 snat to addr on enp1s0)
```
nft add rule nat postrouting ip saddr 192.168.1.0/24 oif enp1s0 snat to 1.2.3.4
```
> SNAT LAN 192.168.1.0/24 to global ip 1.2.3.4
```
nft 'add rule nat prerouting iif etp1s0 tcp dport { 80, 443 } dnat to 192.168.1.120'
```
> DNAT to http server 192.168.1.120
