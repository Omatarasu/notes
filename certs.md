### ( CentOS ) /etc/pki/tls/openssl.cnf: 
### ( Debian ) /etc/ssl/openssl.cnf: 
```
...
[ CA_default ]

dir             = /etc/ca
certs           = $dir/certs
crl_dir         = $dir/crl
database        = $dir/index.txt

new_certs_dir   = $dir/newcerts

certificate     = $dir/ca.crt
serial          = $dir/serial
crlnumber       = $dir/crlnumber

crl             = $dir/crl.pem
private_key     = $dir/private/ca.key

x509_extensions = usr_cert

name_opt        = ca_default
cert_opt        = ca_default


default_days    = 365
default_crl_days= 30
default_md      = sha256
preserve        = no

policy          = policy_anything
...
[ usr_cert ]
...
[ server_cert ]

basicConstraints=CA:FALSE

keyUsage = digitalSignature, keyEncipherment

subjectKeyIdentifier=hash

authorityKeyIdentifier=keyid,issuer

extendedKeyUsage=serverAuth
```
### CA Cert
```
mkdir /etc/ca
cd /etc/ca
mkdir certs newcerts private crl
touch index.txt
echo -n '00' > serial
```
> create ca directory
```
cd /etc/ca
openssl req -nodes \
-new \
-out ca.csr \
-keyout private/ca.key \
-extensions v3_ca
```
> generate ca req
```
cd /etc/ca
openssl ca -selfsign \
-in ca.csr \
-out ca.crt \
-extensions v3_ca
```
> sign ca cert
### Server Cert
```
openssl req -nodes \
-new \
-out www.angulema.fun.csr \
-keyout private/www.angulema.fun.key \
-extensions server_cert
```
> create server req 
```
openssl ca -in www.angulema.fun.csr \
-out www.angulema.fun.crt \
-extensions server_cert 
```
