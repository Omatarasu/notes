# Topolgy
![dmvpn-1](https://user-images.githubusercontent.com/62337797/136694042-31dce17f-54d6-4dc7-8c97-5a2bf0f55936.png)
---
![dmvpn-3](https://user-images.githubusercontent.com/62337797/136789314-5259a543-b5c3-4684-88d7-415ee4c3a712.png)


# HUB
## mGRE
``` 
interface tunnel 0
ip address 172.16.0.1 255.255.255.0
ip mtu 1400
tunnel source Gi0/0/0
tunnel mode gre multipoint
```
> create mGRE

## NHRP
```
interface tunnel 0
ip nhrp network-id 100
ip nhrp authentication CISCO123
ip nhrp map multicast dynamic
```
## IPSEC
```
crypto ikev2 keyring DMVPN
peer DMVPN
address 0.0.0.0 0.0.0.0
pre-shared-key CISCO123
```
> generate pre-share

```
crypto ikev2 profile DMVPN-IKE
keyring local DMVPN
authentication local pre-share
authentication remote pre-share
match address local 10.0.0.1
match identity remote address 0.0.0.0 0.0.0.0
```
> create IKE profile 
```
crypto ipsec profile DMVPN-IPSEC
set ikev2-profile DMVPN-IKE
```
> apply IKE profile for IPSEC 
```
interface Tunnel 0
tunnel protection ipsec profile DMVPN-IPSEC
```
> apply IPSEC profile to Tunnel 0 

# SPOKE1
## mGRE
``` 
interface tunnel 0
ip address 172.16.0.2 255.255.255.0
ip mtu 1400
tunnel source Gi0/0/0
tunnel mode gre multipoint
```
> create mGRE

## NHRP
```
interface tunnel 0
ip nhrp network-id 100
ip nhrp map 172.16.0.1 10.0.0.1 # tunnel local
ip nhrp map multicast 10.0.0.1
ip nhrp authentication CISCO123
```
## IPSEC
```
crypto ikev2 keyring DMVPN
peer DMVPN
address 0.0.0.0 0.0.0.0
pre-shared-key CISCO123
```
> generate pre-share
```
crypto ikev2 profile DMVPN-IKE
keyring local DMVPN
authentication local pre-share
authentication remote pre-share
match address local 10.0.0.2
match identity remote address 0.0.0.0 0.0.0.0
```
> create IKE profile 
```
crypto ipsec profile DMVPN-IPSEC
set ikev2-profile DMVPN-IKE
```
> apply IKE profile for IPSEC 
```
interface Tunnel 0
tunnel protection ipsec profile DMVPN-IPSEC
```
> apply IPSEC profile to Tunnel 0 

# SPOKE2
## mGRE
``` 
interface tunnel 0
ip address 172.16.0.3 255.255.255.0
ip mtu 1400
tunnel source Gi0/0/0
tunnel mode gre multipoint
```
> create mGRE

## NHRP
```
interface tunnel 0
ip nhrp network-id 100
ip nhrp map 172.16.0.1 10.0.0.1 # tunnel local
ip nhrp map multicast 10.0.0.1
ip nhrp authentication CISCO123
```
## IPSEC
```
crypto ikev2 keyring DMVPN
peer DMVPN
address 0.0.0.0 0.0.0.0
pre-shared-key CISCO123
```
> generate pre-share
```
crypto ikev2 profile DMVPN-IKE
keyring local DMVPN
authentication local pre-share
authentication remote pre-share
match address local 0.0.0.0
match identity remote address 0.0.0.0 0.0.0.0
```
> create IKE profile 
```
crypto ipsec profile DMVPN-IPSEC
set ikev2-profile DMVPN-IKE
```
> apply IKE profile for IPSEC 
```
interface Tunnel 0
tunnel protection ipsec profile DMVPN-IPSEC
```
> apply IPSEC profile to Tunnel 0 
