### ansible.cfg:

	[defaults]
	host_key_checking = false
	inventory         = /etc/ansible/hosts
### hosts:
	[master] # group of hosts
	node01 ansible_host=192.168.101.10

	[slave]
	node02 ansible_host=192.168.101.20
	node03 ansible_host=192.168.101.30

	[prod:children] # group of groups
	slave
	master
### group_vars/slave:
	ansible_user			:	root 
	ansible_ssh_private_key_file	:	/root/.ssh/id_ed25519
> filename matches the group name from hosts

### host_vars/mode01
	ansible_user: user
	ansible_ssh_private_key_file: /root/.ssh.id_rsa

> filename matches the hostname in hosts
   
### ansible easy playbook example
 	---
 	- name: Test Connection
 	 hosts: prod
 	 become: yes

	 tasks:
     - name: Ping My Prod
     ping:

