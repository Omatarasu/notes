# UFW
### Default Policy
```
ufw default deny incoming
ufw default allow outgoing
```
> policy for incoming - deny, for outgoing - allow
```
sudo ufw allow proto tcp from 192.168.10.0/24 to 192.168.10.1 port 22
```
> allow ssh
