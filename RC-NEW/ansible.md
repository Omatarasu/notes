# Initial Palybook
```
- name: My Playbook Part 1
  hosts: all
  
  tasks:
    - name: Disable selinux part 2
      lineinfile:
        path: '/etc/selinux/config'
        search_string: 'SELINUX=enforcing'
        line: 'SELINUX=permissive'
      notify: Disable running selinux
      when: ansible_facts['distribution'] == 'CentOS'
    - name: Switch ssh port
      lineinfile:
        path: '/etc/ssh/sshd_config'
        search_string: '#Port 22'
        line: 'Port 4444'
      notify: Restart sshd
  handlers: 
    - name: Restart sshd
      service:
        name: sshd
        state: restarted  
    - name: Disable running selinux
      shell: setenforce 0
      when: ansible_facts['distribution'] == 'CentOS'
```
> initiall ssh configuration
```
openssl passwd -salt suck -6 suck
```
> generate pass for user module
```
- name: My Playbook Part 2
  hosts: all
  vars:
    ansible_port: 4444
  tasks:
    - name: CentOS
      block:
        - name: Install epel-release
          dnf:
            name: "epel-release"
            state: latest
        - name: Update Packages
          dnf:
            name: "*"
            state: latest
        - name: Add User
          user:
            name: test
            shell: '/bin/bash'
            password: '$6$suck$Pg0pDB6Ruq.eoJCr8azNysBYcaaC01PcFGEVnrWm658QNRGPiwOzFHMvjmOxNARJ4Yx7LMJC2Ng/5EAbhSFjs1'
            groups: wheel
            append: yes
      when: ansible_facts['distribution'] == 'CentOS'
    - name: Ubuntu
      block:
        - name: Update Packages
          apt: 
            name: "*"
            state: latest
            update_cache: yes
        - name: Add User
          user:
            name: test
            shell: '/bin/bash'
            password: '$6$suck$Pg0pDB6Ruq.eoJCr8azNysBYcaaC01PcFGEVnrWm658QNRGPiwOzFHMvjmOxNARJ4Yx7LMJC2Ng/5EAbhSFjs1'
            groups: sudo
            append: yes
      when: ansible_facts['distribution'] == 'Ubuntu'

    - name: add ssh dir
      file:
        path: /home/test/.ssh
        state: directory
    - name: ssh keys add 
      copy:
        content: | 
          ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCbVjAU+X72BBG21JS0JLiicdlXMqZ8OiB4sB3JYmAb1l3TtpohSQH8K9aI3SM3qzqm7d4PfT+4AuH8FSum0+nFWcq/irVEu8N+EEk2wkYpMK3M2cFBUvRefv1zdL8PEQo5HKCH6U8pAFBG4NwJVWMpAcTuiAAevjk+Ov2Nfugc3gEIPd6pn71bkclXnh0M8wL0YoxfMAZ9WGRtudeGeDK6Hfi7HRxAljH8mjlI4avDoEWA6wi08lm/FdUsz/kS4BICLfMHUUvzjO6Sqn8UVavMQJB7slXSvjsxSddNdoEeeWsR+TNazvIQq9juPbV298bb6DAg3+IJljIPevBFVOYsVcUKjaYHum5gTanCKevV3uRK2HXrB8nyo/s8G3amXpAPg5cP4QCAij3TsF3mVgjlg1Nw0GOGyUkYNXjfpqCZalr9Aqi/37jrvjpKHDOD06Ff2oC+eC5eVNYZrmgTRO5gyf3XZFEw0KjopU8xseV6NogOveNIvw1+ekdytpxL8H8= root@test-centos
        dest: /home/test/.ssh/authorized_keys
```
> create users, update system, copy ssh keys
```

```
