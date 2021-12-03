# Cisco with Ubuntu 
### Cisco
```
interface tunnel 1
ip address 192.168.50.2
tunnel mode gre ip
tunnel source 10.1.0.10
tunnel destianation 10.0.0.10
```
> configure gre
```
crypto isakmp policy 1
  encr aes
  hash sha256
  authentication pre-share
  group 14
```
> ikev2 policy
```
crypto isakmp key cisco address 10.0.0.10
```
> PSK 
```
crupto ipsec transform-set GRE esp-aes esp-sha256-hmac
mode tunnel
```
> create transform-set
```
crypto ipsec profile GRE-IPSEC
set transfor-set GRE
```
> apply transform-set
```
interface tunnel 1 
tunnel protection ipsec profile GRE-IPSEC
```
> apply ipsec profile on gre tunnel
### Ubuntu
##### /etc/netplan/*.yaml
```
network:
  version: 2
  ethernets: 
    ens160:
      dhcp4: flase
      dhcp6: false
      addresses:
      - 10.0.0.10
      gateway4: 10.0.0.1
      nameservers: 
        addresses:
        - 8.8.8.8
        
  tunnels:
    my-tunnel:
      mode: gre
      local: 10.0.0.10
      remote: 10.1.0.10
      addresses:
      - 192.168.50.1/30
```
> configuring gre tunnel and netpwork interface
```
netplan generate
```
> check config
```
netplan apply 
```
> apply config
```
apt install libreswan -y
```
> install ipsec
##### /etc/ipsec.d/gre.conf
```
conn gre
    ikev2=no 
    auto=start
    authby=secret
    type=tunnel
    ike=aes-sha2;modp2048
    phase2=esp
    phase2alg=aes-sha2;modp2048
    left=10.0.0.10
    leftprotoport=gre
    right=10.1.0.10
    rightprotoport=gre
```
> config file for ipsec
##### /etc/ipsec.d/gre.secrets
```
10.0.0.10 10.1.0.10: PSK "cisco"
```
> PSK 
```
systemctl enable --now ipsec.service
systemctl restart ipsec.service
```
> start and enable ipsec.service
