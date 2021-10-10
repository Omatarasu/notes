# Topolgy
![dmvpn-1](https://user-images.githubusercontent.com/62337797/136694042-31dce17f-54d6-4dc7-8c97-5a2bf0f55936.png)
---
![dmvpn-2](https://user-images.githubusercontent.com/62337797/136694044-daa13313-b496-48d8-a651-f68ab9ee2ba3.png)

# HUB
#### mGRE
```
interface Tunnel 0
ip address 172.16.0.1 255.255.255.0
```
> creating Interface tunnel 
```
ip mtu 1416
```
> correcting MTU for tunnel
```
tunnel source Gi0/0/0
```
> source interface Gi0/0/0
```
tunnel mode gre multipoint
```
> mode mGRE

