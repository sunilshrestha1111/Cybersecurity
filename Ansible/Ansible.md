- Generate a ssh key and store in a folder
  Command: ssh-keygen

- Create all the resources in the Azure Portal you need to set up a fully operational virtual Azure environment

- Utilize the public key that was previously generated to set up the jump-box virtual machine.
 
- SSH into the Jump Box machine
  Command: ssh -i <file path> azureuser@<jump-box ip address>

- Insert the docker container in Jump-box
  Command: 
  	sudo apt-get install docker.io
	sudo docker pull cybersecurity/ubuntu:bionic
	sudo docker run -ti cyberxsecurity/ubuntu:bionic bash
	sudo docker container list -a
	sudo docker start <identifier of docker image>
	sudo docker attach <identifier of docker image>

-  Once inside the docker container, generate a ssh key
   Command: ssh-keygen
  
- Navigate to /etc/ansible/hosts and edit the hosts file with the host ip address
   Command: nano hosts
  
- Navigate to /etc/ansible/ansible.cfg and update the "remote_user" = <username in VMs/Servers>

- Get the filebeat-config.yml and store in etc/ansible/files/filebeat-config.yml
  Command: curl https://gist.githubusercontent.com/slape/5cc350109583af6cbe577bbcc0710c93/raw/eca603b72586fbe148c11f9c87bf96a63cb25760/Filebeat  > /etc/ansible/files/filebeat-config.yml
 
 - Update filebeat-config.yml with
    "output.elasticsearch:
     # Boolean flag to enable or disable the output module.
     #enabled: true

     # Array of hosts to connect to.
     # Scheme and port can be left out and will be set to the default (http and 9200)
     # In case you specify and additional path, the scheme is required: http://localhost:9200/path
     # IPv6 addresses should always be defined as: https://[2001:db8::1]:9200
        hosts: ["10.1.0.5:9200"]
        username: "elastic"
        password: "changeme" # TODO: Change this to the password you set"
     
    Starting with Beats version 6.0.0, the dashboards are loaded via the Kibana API.
    # This requires a Kibana endpoint configuration.
       setup.kibana:
       host: "10.1.0.5:5601" # TODO: Change this to the IP address of your ELK server

-  Run the playbook using
   Command: ansible-playbook <playbook>

-  install-elk.yml playbook configures elk VM with Docker on elk server. This playbook installs docker.io, installs pip3, installs docker python module, and downloads and launch docker with elk container.

-  filebeat-playbook.yml playbook installs filebeat playbook on web servers. This playbook gets the filebeat from artifacts.elastic.co, copies the filebeat configuration from ansible to web server VMs, and sets the filebeat to start running upon boot. 

- pentest.yml playbook configures Web VM with docker.




 


     
        
 	



