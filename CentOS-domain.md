# Topology
![CentOS-Domain](https://user-images.githubusercontent.com/62337797/140320114-1bc033f9-3561-4998-999b-23b17c0316df.png)
# WIN-SRV 

> configure AD

> configule DHCP

# CentOS
```
hostnamectl set-hostname centos.angulema.fun
```
> set hostname
```
dnf install realmd -y
```
> install realmd
```
realm discover angulema.fun
Output:
angulema.fun
  type: kerberos
  realm-name: ANGULEMA.FUN
  domain-name: angulema.fun
  configured: no
  server-software: active-directory
  client-software: sssd
  required-package: oddjob
  required-package: oddjob-mkhomedir
  required-package: sssd
  required-package: adcli
  required-package: samba-common-tools

```
> show required packages
```
dnf install sssd oddjob oddjob-mkhomedir adcli samba-common-tools -y
```
> install required packages
```
realm join --user=Administrator angulema.fun
```
> join to domain
```
vim /etc/sssd/sssd.conf
  use_fully_qualified_names = False
  fallback_homedir = /home/%u
```
> correct some param
```
systemctl restart sssd
```
> restart sssd

# Addition
> time and date same on all machines 

> correct configure dns 
# Source
https://www.golinuxcloud.com/add-linux-to-windows-ad-domain-realm/
