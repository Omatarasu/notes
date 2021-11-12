### /etc/ansible/ca.yml:
```
 - name: Distribute CA
   hosts: all
   become: yes

   tasks:
   - block: 

     - name: Copy CA
       copy: 
         src: "/etc/ca/ca.crt"
         dest: "/usr/local/share/ca-certificates/"
         
     - name: Update CA DB
       shell: update-ca-certificates

     when: ansible_distribution == "Debian"

   - block:
     
     - name: Copy CA
       copy:
         src: "/etc/ca/ca.crt"
         dest: "/etc/pki/ca-trust/source/anchors/"

     - name: Update CA DB
       shell: update-ca-trust extract       

     when: ansible_distribution == "CentOS" 
```
> need ca cert in /etc/ca/ca.crt
