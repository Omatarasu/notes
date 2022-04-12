### comman show open ports
```
ss -ltnp # tcp
ss -lunp # udp
```
> t - tcp, n - numbers of ports, p - process
### command show mounts
```
df
```
### command show UUID of disks 
```
blkid
```
### test rsyslog configuration
```
rsyslogd -f /etc/rsyslog.conf -N 1
```
