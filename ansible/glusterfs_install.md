### /etc/ansible/glusterfs.yml
```
---
- name: Install Glusterfs
  hosts: nodes
  become: yes

  tasks:
  - block:

    - name: Install Additional Repos
      dnf:
        name:
        - epel-release
        - centos-release-gluster
        - yum-utils
        state: present

    - name: Install Glusterfs
      dnf:
        name: glusterfs-server
        state: present

    - name: Add Firewall Ports
      firewalld:
        zone: public
        service: glusterfs
        permanent: true
        state: enabled
      notify: Restart Firewalld

    when: ansible_distribution == "CentOS"


  - block:

    - name: Install Glustefs
      apt:
        name: glusterfs-server
        state: present

    when: ansible_distribution == "Debian"

  - name: Start And Enable Glusterfs
    service:
      name: glusterd
      state: started
      enabled: yes

  handlers:
  - name: Restart Firewalld
    service: 
      name: firewalld
      state: restarted
```
