# Topology 
![Debian-Domain](https://user-images.githubusercontent.com/62337797/140346203-f558fad1-5d00-46c7-8bf0-05c6606fb69d.png)
# WIN-SRV 

> configure AD

> configule DHCP

# Debian
```
hostnamectl set-hostname debian.angulema.fun
```
> set hostname 
```
apt install krb5-user samba winbind libpam-krb5 libpam-winbind libnss-winbind -y
```
> install reqired packages

#### /etc/krb5.conf:

```
[libdefaults]
	default_realm = ANGULEMA.FUN
	kdc_timesync = 1
	ccache_type = 4
	forwardable = true
	proxiable = true
	fcc-mit-ticketflags = true

[realms]
	ANGULEMA.FUN = {
		kdc = win-srv.angulema.fun
		admin_server = win-srv.angulema.fun
		}

```
> content 
```
kinit Administrator@ANGULEMA.FUN
```
> create kerberos ticket
#### /etc/samba/smb.conf:
```
[global]
   workgroup = ANGULEMA
   realm = ANGULEMA.FUN
   
   log file = /var/log/samba/log.%m
   max log size = 1000
   logging = file
   panic action = /usr/share/samba/panic-action %d

   security = ADS

   dns proxy = no 
   socket options = TCP_NODELAY

   domain master = no
   local master = no
   preferred master = no
   os level = 0


   load printers = no
   show add printer wizard = no
   printcap name = /dev/null
   disable spoolss = yes

   server role = member server
   obey pam restrictions = yes
```
> content

#### /etc/hosts
```
127.0.1.1  debian.angulema.fun debian
```
> add content
```
net ads join -U Administrator -D ANGULEMA.FUN 
```
> connect to ad 
#### /etc/samba/smb.conf
```
   idmap config * : range = 10000-20000
   idmap config * : backend = tdb 
   
   winbind enum groups = yes
   winbind enum users = yes

   winbind use default domain = yes

   template shell = /bin/bash
   template homedir = /home/%U

   winbind refresh tickets = yes
```
> add winbind config
 
#### /etc/nsswitch.conf 
```
passwd:         files systemd winbind
group:          files systemd winbind
shadow:         files winbind
gshadow:        files

hosts:          files dns
networks:       files

protocols:      db files
services:       db files
ethers:         db files
rpc:            db files

netgroup:       nis
```
> add winbind auth
```
pam-auth-update
```
> check the box create homedir
```
systemctl restart smbd
systemctl restart winbind
```
> restart services
# Sources 
https://help.ubuntu.ru/wiki/%D0%B2%D0%B2%D0%BE%D0%B4_%D0%B2_%D0%B4%D0%BE%D0%BC%D0%B5%D0%BD_windows
https://imbicile.pp.ru/ubuntu-16-04-active-directory/
