
### /etc/samba/smb.conf
```
...
[share]
	comment = My Share
	path = /mnt/smb
	read only = no 
	valid users = @"domain users" # group domain users
	writeable = yes
	browseable = yes
	create mask = 0660
  directory mask = 0770
```
> create samba share
```
mkdir /mnt/smb
chmod 0770 -R /mnt/smb
chown nobody:"domain users" -R /mnt/smb
```
### if you use centos disable selinux
### Allow samba port in firewall
