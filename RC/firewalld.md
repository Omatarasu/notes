### firewalld dnat
```
firewall-cmd --add-rich-rule `rule family="ipv4" source address="192.168.10.2" forward-port to-addr="172.16.10.2" to-port="53" protocol="tcp" port="53"' --permanent
firewall-cmd --reload
```
