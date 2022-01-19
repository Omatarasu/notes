```
hostname SW1
```
> set hostname 
```
line console 0
password cisco
login
```
> set password on console line
```
line vty 0 15 
password cisco 
login
```
> set password on vty
```
enable secret class 
```
> set enable password
```
service password-encryption
```
> encrypt password
```
banner motd #Authorized Access Only#
```
> set banner 
```
```
interface vlan 1
ip address 192.168.1.10 255.255.255.0
no shutdown 
exit 
ip default-gateway 192.168.1.1
```
> ip configuration SVI
```
ping 192.168.1.1
```
> check connection (priv mode)

show run
```
> show running config
```
cory run start
```
> save config
