# Networking
### \etc\netplan\*.yaml
```
network:
  version: 2
  ethernets:
    ens160:
      dhcp4: true
    ens192:
      dhcp4: false
      dhcp6: false
      addresses:
      - 192.168.10.1/24
```
