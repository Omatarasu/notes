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
nft add rule inet filter input iifname "lo" counter accept
```
> accept loopback
```
nft add rule inet filter input icmp type echo-request counter acccept
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
nft add rule ip nat postrouting oifname "enp1s0" counter masquerade 
```
> MASQUEARDE chain create (all ipv4 package from enp1s0 snat)
