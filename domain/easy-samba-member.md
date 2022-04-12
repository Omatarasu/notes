```
hostnamectl set-hostname centos.my.wsr
```
> set hostname
```
...
127.0.1.1 centos.my.wsr
```
> /etc/hosts
```
[libdefaults]
	default_realm = MY.WSR
```
> /etc/krb5.conf
```
kinit Administrator
```
> crete tgt
```
[global]
	workgroup = MY
	realm = MY.WSR
	security = ADS
	server role = member server
```
> /etc/samba/smb.conf
```
net ads join -U Administrator 
```
> connect to AD
```
...
	idmap config * : range = 10000-20000
	idmap config * : backend = tdb 

	template shell = /bin/bash
	template homedir = /home/%U

	winbind refresh tickets = yes
```
> /etc/samba/smb.conf
```
authconfig --enablewinbind  --enablewinbindauth --updateall
authconfig --enablewinbindusedefaultdomain --updateall
authconfig --enablemkhomedir --updateall
```
> add user mapping
```
systemctl restart smb
systemctl restart winbind
```
> restart services
