# UFW
### Default Policy
```
ufw default deny incoming
ufw default allow outgoing
```
> policy for incoming - deny, for outgoing - allow
```
ufw allow 22/tcp
```
> allow ssh
