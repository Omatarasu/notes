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
