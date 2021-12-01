### /etc/iscsi/iscsid.conf
```
...
node.startup = automatic
...
node.session.auth.username = root
node.session.auth.password = toortoortoor
discovery.sendtargets.auth.username = root
discovery.sendtargets.auth.password = toortoortoor
```
> autostart and CHAP
```
iscsiadm -m discovery -t st -p 192.168.10.40
```
> discovery iscsi target
```
iscsiadm -m node 
```
> show discovered iscsi target
```
iscsiadm -m node --targetname "iqn.1991-05.com.microsoft:a-w01-share-target" --portal "192.168.10.40" --login
```
> mount iscsi
```
iscsiadm -m session -P 3 | less
```
> look info 
```
iscsiadm -m node --targetname "iqn.1991-05.com.microsoft:a-w01-share-target" -logout
iscsiadm -m discovery --portal 192.168.10.40 --op=delete
```
>delete iscsi
