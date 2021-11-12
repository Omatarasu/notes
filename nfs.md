```
dnf install nfs-utils -y
```
> install nfs-server
```
systemctl enable --now nfs-server 
systemctl status nfs-server
```
> start and enable nfs-server
```
mkdir /mnt/nfs 
chown nobody:nobody -R /mnt/nfs
```
> create nfs directory
### /etc/exports
```
/mnt/nfs 192.168.121.0/24(rw,sync)
```
```
exportfs -arv
```
> export nfs
```
exportfs -s
```
> list of exports
```
dnf install nfs-utils nfs4-acl-tools -y
```
> on clients
```
showmount -e 192.168.121.10
```
> show nfs share on server
```
sudo mount -t nfs 192.168.121.10:/mnt/nfs /root/nfs
```
> mount nfs share
```
echo "192.168.121.10:/mnt/nfs /root/nfs nfs defaults 0 0" > /etc/fstab
mount -a
```
> mount with fstab
