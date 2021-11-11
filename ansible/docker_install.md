### /etc/ansible/docker.yml
```
 - name: Install Docker 
   hosts: nodes
   become: yes

   tasks:
   - block:

     - name: Add Docker Repo
       copy:
         src: /etc/ansible/docker-ce.repo
         dest: /etc/yum.repos.d/
     - name: Remove Some Package
       dnf:
         name: 
         - runc
         - podman
         - containers-common
         state: absent

     - name: Install Docker
       dnf:
         name: docker-ce
         state: present
     
     when: ansible_distribution == "CentOS"

   - block:
     
     - name: Install Additionals Package
       apt:
         name:
         - ca-certificates
         - curl
         - gnupg
         - lsb-release 
         update_cache: yes

     - name: Import GPG key
       apt_key:
         url: https://download.docker.com/linux/debian/gpg
         state: present

     - name: Import Repo
       apt_repository:
         repo: deb [arch=amd64] https://download.docker.com/linux/debian bullseye stable
         state: present 

     - name: Install Docker 
       apt: 
         name: docker-ce 
         state: present
         update_cache: yes

     when: ansible_distribution == "Debian"

   - name: Start And Enable Docker 
     service: 
       name: docker 
       state: started 
       enabled: yes

```
