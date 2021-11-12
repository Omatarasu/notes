```
apt install nfs-kernel-server -y
```
> install nfs server
```
systemctl enable --now nfs-server
systemctl status nfs-server
```
> start and enable nfs
```
mkdir /mnt/nfs
chown -R nobody:nogroup /mnt/nfs
```
> create nfs directory
### /etc/exports
```
/mnt/nfs 	192.168.121.0/24(rw,sync,no_subtree_check,fsid=1)
```
```
exportfs -avr
```
> export nfs share
```
apt install nfs-common nfs4-acl-tools -y
```
> install client software
```
mount -t nfs 192.168.121.10:/mnt/nfs /root/nfs
```
> mount nfs share
```
echo "192.168.121.10:/mnt/nfs /root/nfs nfs defaults 0 0" >> /etc/fstab
mount -a
```
