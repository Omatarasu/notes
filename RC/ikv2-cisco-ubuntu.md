# Ubuntu
### Install
```
apt install libreswan -y
```
### /etc/ipsec.d/gre-to-csr.conf
```
conn gre-to-csr
    auto=start
    authby=secret
    type=tunnel
    ike=aes-sha512;modp4096
    phase2=esp
    phase2alg=aes-sha512;modp4096
    left=10.22.12.103
    leftprotoport=gre
    right=10.22.12.131
    rightprotoport=gre
```
### /etc/ipsec.d/gre-to-csr.secrets
```
10.22.12.103 10.22.12.131: PSK "fajd&#R^6b(Cfx649abx(NFfz561fd93adx4rf8mGdabuyer"
```
### Enable
```
systemctl enable --now ipsec.service 
```

# Cisco
### Create pre-shared-key
```
crypto ikev2 keyring GRE-KEYS
peer A-L00
address 10.22.12.103
pre-share-key fajd&#R^6b(Cfx649abx(NFfz561fd93adx4rf8mGdabuyer
```
### Create Alg Set for IKEv2
```
crypto ikev2 proposal default
encryption aes-cbc-256
integrity sha512
group 16
```
> create proposal
```
crypto ikev2 policy default
proposal default
```
> apply proposal
### Create IKEv2 Profile
```
crypto ikev2 profile A-L00-PROFILE
keyring local GRE-KEYS
authentication local pre-share
authentication remote pre-share
match address local 10.22.12.131
match identity remote address 10.22.12.103
```
### Create Alg Set for IPSEC
```
crypto ipsec transform-set default esp-aes 256 esp-sha512-hmac
mode tunnel 
```
### Create IPSEC Profile
```
crypto ipsec profile A-L00
set ikev2 profile A-L00-PROFILE
set transform-set default
```
### Apply IPSEC Profile on GRE
```
interface tunnel 1
tunnel protection ipsec profile A-L00
```
