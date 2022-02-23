### Install 
```
dnf install targetcli -y
```
> CentOS
```
apt install targetcli-fb -y
```
> Debian
### Enable 
```
systemctl enable --now targetclid.service
```
### Create 
```
dd if=/dev/zero of=/mnt/iscsi bs=1M count=1000
```
> create 1000Mb file
```
targetcli
```
> enter
```
/backstores/fileio create storage1 /mnt/iscsi
```
> create storage (if block storage use /backstores/block) 
```
/iscsi create
```
> create target
```
luns/ create /backstores/fileio/storage1
```
> create lun
```
portals/ delete ip_address=0.0.0.0 ip_port=3260
```
> delete default portal
```
portals/ create ip_address=$you_host_address ip_port=3260
```
> create portal
```
cat /etc/iscsi/initiatorname.iscsi
```
> see iqn in linux
```
acls/ create $iqn
```
> access permission
# Sources
https://www.saqwel.ru/articles/linux/nastrojka-linux-iscsi-posredstvom-targetcli/
