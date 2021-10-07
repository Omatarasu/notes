# Handlers
	---
	- name: Install Apache
	  hosts: prod
	  become: yes

	  vars:
	    src: /etc/ansible/index.html
	    dest: /var/www/html

	  tasks:
	  - name: Install Apache 
	    dnf:
	     name: httpd
	     state: latest

	  - name: Copy My index.html
	    copy:
	      src: "{{ src }}"
	      dest: "{{ dest }}"
	      mode: 0555  
	    notify: Restart Apache # if state changed start handler

	  - name: Start And Enable
	    service:
	      name: httpd
	      state: started
	      enabled: yes

	  handlers:
	  - name: Restart Apache
	    service:
	      name: httpd
	      state: restarted

