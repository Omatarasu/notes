### Install
```
dnf install pam_mount cifs-utils -y
apt install libpam-mount cifs-utils -y
```
### /etc/pam.d/login
```
auth  optional  pam_mount.so
session optional  pam_mount.so
```
### /etc/security/pam_mount.conf.xml
```
<volume fstype="cifs" server="172.16.50.10" path="smb" mountpoint="/home/%(DOMAIN_USER)/smb" options="username=%(DOMAIN_USER)" />
```
> after Volume definitions
