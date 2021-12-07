```
dnf install dhcp-relay
cp /lib/systemd/system/dhcrelay.service /etc/systemd/system/
```
### /etc/systemd/system/dhcrelay.service
```
ExecStart=/usr/sbin/dhcrelay -d --no-pid 192.168.1.1
```
### restart service
```
systemctl reload-daemon
systemctl restart dhcrelay.service
```
# Sources 
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/dhcp-relay-agent
