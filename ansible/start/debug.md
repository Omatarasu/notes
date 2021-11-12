# Debug 	
    - name: Vars Playbook
	  hosts: prod
 	  become: yes

	
	  vars: 
	    message: hello
   	    message_2: world
	    secret: fhdaksjfbvajdkf
   	    owner: Valg

	  tasks:
  	  - debug:
          var: secret # print value
  
	  - debug: 
          msg: "Secret is {{secret}}" print string with value

      - debug: 
          msg: "Owner this server -->{{ owner }}<--"
		
      - set_fact: 
          full_message: "{{message}} {{message_2}} {{owner}}" # creating new value
      - debug:
          var: full_message
      - debug:
          var: ansible_distribution
      - shell: uptime
	    register: result # record command result to this value
  	  - debug:
     	  var: result.stdout # json
