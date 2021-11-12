```
conn gre 
	auto=start (autostart)
	authby=secret (auth by password)
	type=tunnel
	ike=aes-sha2;modp2048
	phase2=esp
	phase2alg=aes-sha2;modp2048
	left=10.0.0.2 (local)
	leftprotoport=gre
	right=10.0.1.2 (remote)
	rightprotoport=gre
```
```
10.0.0.2(local) 10.0.1.2(remote): PSK "/etc/ipsec.d/gre" # file with pass
```
