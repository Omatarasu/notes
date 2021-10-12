# Topology
![openvpn](https://user-images.githubusercontent.com/62337797/136903975-e2618cfc-7460-4608-bf13-bfda0dcc383f.png)
# TASKS
- hostnames
- ip addresses
- configure firewall on all machines
- nat on CA_OPENVPN-SERVER, ISP 
- install epel-release on CentOS
- install openvpn
### CA
```
mkdir /etc/ca
cd /etc/ca
mkdir certs newcerts private crl
touch index.txt
echo -n '00' > serial
```
> create ca directory
```
openssl req -nodes \
-new \
-out ca.csr \
-keyout private/ca.key \
-extensions v3_ca
```
> create ca req
```
openssl ca -selfsign \
-in ca.csr \
-out ca.crt \
-extensions v3_ca
```
> 
