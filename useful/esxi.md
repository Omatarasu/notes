### Creating esxi with virt-install
```
virt-install --virt-type=kvm --name=esxi1 \ 
--cpu host-passthrough \ 
--ram 4096 --vcpus=4 \
--virt-type=kvm --hvm \
--cdrom ~/Downloads/VMware-VMvisor-Installer-201912001-15160138.x86_64.iso \ 
--network network:default,model=e1000 \ 
--graphics vnc --video qxl \
--disk pool=default,size=80,sparse=true,bus=ide,format=qcow2 \ 
--boot cdrom,hd --noautoconsole --force
```
