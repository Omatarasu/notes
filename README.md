# Topology
![Untitled Diagram drawio](https://user-images.githubusercontent.com/62337797/139422875-d51cfde5-b257-4d01-8397-1fba1ca4db4f.png)
# node01
### Glusterfs
```
mkfs.xfs /dev/vdb 
```
> create file system 
```
mkdir -p /gluster/volumes/1
echo '/dev/vdb /gluster/volumes/1 xfs defaults 0 0' >> /etc/fstab
mount -a
```
> mount file system
```
df | grep vdb
```
> check mount
```
mkdir /gluster/volumes/1/node01
```
> create directory
```
dnf install epel-release -y
dnf install centos-release-gluster -y
dnf install yum-utils -y
```
> install additional repos and yum utils
```
dnf install glusterfs-server -y
```
> install glusterfs
```
systemctl enable --now glusterd
systemctl status glusterd
```
> start and enable glusterd
```
firewall-cmd --add-service=glusterfs --permanent 
firewall-cmd --reload
```
> add firewall rules for glusterfs
```
gluster peer probe node02
gluster peer probe node03
gluster peer status
```
> connect nodes
```
gluster volume create share \
replica 3 \
node01:/gluster/volumes/1/node01 \
node02:/gluster/volumes/1/node02 \
node03:/gluster/volumes/1/node03
```
> create share volume
```
gluster volume start share
gluster volume status share
```
> start share volume
```
gluster volume set share auth.allow 192.168.122.10,192.168.122.20,192.168.122.30
```
> allow mount volumes for node01,node02,node03
```
echo 'localhost:/share /mnt glusterfs defaults,_netdev 0 0' >> /etc/fstab
mount -a
df | grep share
```
> mount gluster volume
# node02

```
mkfs.xfs /dev/vdb 
```
> create file system 
```
mkdir -p /gluster/volumes/1
echo '/dev/vdb /gluster/volumes/1 xfs defaults 0 0' >> /etc/fstab
mount -a
```
> mount file system
```
df | grep vdb
```
> check mount
```
mkdir /gluster/volumes/1/node02
```
> create directory
```
dnf install epel-release -y
dnf install centos-release-gluster -y
dnf install yum-utils -y
```
> install additional repos and yum utils
```
dnf install glusterfs-server -y
```
> install glusterfs
```
systemctl enable --now glusterd
systemctl status glusterd
```
> start and enable glusterd
```
firewall-cmd --add-service=glusterfs --permanent 
firewall-cmd --reload
```
> add firewall rules for glusterfs
```
echo 'localhost:/share /mnt glusterfs defaults,_netdev 0 0' >> /etc/fstab
mount -a
df | grep share
```
> mount gluster volume

# node03

```
mkfs.xfs /dev/vdb 
```
> create file system 
```
mkdir -p /gluster/volumes/1
echo '/dev/vdb /gluster/volumes/1 xfs defaults 0 0' >> /etc/fstab
mount -a
```
> mount file system
```
df | grep vdb
```
> check mount
```
mkdir /gluster/volumes/1/node03
```
> create directory
```
dnf install epel-release -y
dnf install centos-release-gluster -y
dnf install yum-utils -y
```
> install additional repos and yum utils
```
dnf install glusterfs-server -y
```
> install glusterfs
```
systemctl enable --now glusterd
systemctl status glusterd
```
> start and enable glusterd
```
firewall-cmd --add-service=glusterfs --permanent 
firewall-cmd --reload
```
> add firewall rules for glusterfs
```
echo 'localhost:/share /mnt glusterfs defaults,_netdev 0 0' >> /etc/fstab
mount -a
df | grep share
```
> mount gluster volume

## All
```
sudo yum install -y yum-utils
sudo yum-config-manager \
--add-repo \
https://download.docker.com/linux/centos/docker-ce.repo
```
> add docker repo
```
sudo yum install docker-ce --allowerasing -y
```
> download docker
```
systemctl enable --now docker
systemctl status docker
```
> enbale docker
```
firewall-cmd --add-service=docker-swarm --permanent 
firewall-cmd --reload
```
> add firewall rules for docker swarm
```
docker swarm init ...
docker swarm join-token manager 
docker swarm join ...
```
> create docker swarm cluster 
