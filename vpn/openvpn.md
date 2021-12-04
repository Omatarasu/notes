# Topology
![openvpn](https://user-images.githubusercontent.com/62337797/136903975-e2618cfc-7460-4608-bf13-bfda0dcc383f.png)
# TASKS
- hostnames
- ip addresses
- configure firewall on all machines
- nat on CA_OPENVPN-SERVER, ISP 
- install epel-release on CentOS
- install openvpn
- add port in firewall
- 
### CA
[openssl.cnf](https://github.com/Omatarasu/notes/files/7328751/openssl.txt)
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
> sign ca cert
```
openssl req -nodes \
-new \
-out server.csr \
-keyout private/server.key \
-extensions vpn_server
```
> create server req
```
openssl ca -in server.csr \
-out server.crt \
-extensions vpn_server
```
> sign server cert
```
openssl req -nodes \
-new \
-out client.csr \
-keyout private/client.key \
-extensions vpn_client
```
> create client req
```
openssl ca -in client.csr \
-out client.crt \
-extensions vpn_client
```
> sign client cert
# SERVER AND CLIENT
```
client
dev tun
proto udp
remote 192.168.10.2 1194
resolv-retry infinite
nobind
user nobody # CentOS
group nogroup
persist-key
persist-tun
ca /etc/openvpn/ca.crt
cert /etc/openvpn/client.crt
key /etc/openvpn/client.key
remote-cert-tls server
cipher AES-256-CBC
comp-lzo
# Set log file verbosity.
verb 3
# Silence repeating messages
;mute 20
```
> client config file 
```
local 192.168.10.2
port 1194
proto udp4
dev tun
ca /etc/openvpn/ca.crt
cert /etc/openvpn/server.crt
key /etc/openvpn/server.key  # This file should be kept secret
#   openssl dhparam -out dh2048.pem 2048
dh /etc/openvpn/dh.pem
topology subnet
server 10.0.0.0 255.255.255.0
# ifconfig-pool-persist ipp.txt
push "route 192.168.0.0 255.255.255.0"
duplicate-cn
keepalive 10 120
# Generate with:
#   openvpn --genkey --secret ta.key
# The second parameter should be '0'
# on the server and '1' on the clients.
# tls-auth ta.key 0 # This file is secret
data-ciphers-fallback AES-256-CBC
user nobody # Debian
group nobody
persist-key
persist-tun
status openvpn-status.log
;log-append  openvpn.log
# Set the appropriate level of log
# file verbosity.
#
# 0 is silent, except for fatal errors
# 4 is reasonable for general usage
# 5 and 6 can help to debug connection problems
# 9 is extremely verbose
verb 3
# Silence repeating messages.  At most 20
# sequential messages of the same message
# category will be output to the log.
;mute 20
# Notify the client that when the server restarts so it
# can automatically reconnect.
explicit-exit-notify 1
```
> server config file
