# node_0
```
vrrp_instance DOCKER_1 {
        state MASTER
        interface ens3
        virtual_router_id 51
        priority 255
        advert_int 1
        authentication {
              auth_type PASS
              auth_pass 12345
        }
        virtual_ipaddress {
              192.168.120.15/24
        } 
}
```
# node_1
```
vrrp_instance DOCKER_1 {
        state BACKUP
        interface ens3
        virtual_router_id 51
        priority 254
        advert_int 1
        authentication {
              auth_type PASS
              auth_pass 12345
        }
        virtual_ipaddress {
              192.168.120.15/24
        } 
}
```
