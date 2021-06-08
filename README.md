## MODULE 6 - Ansible
## Homework 2
=====================
##Preparing playbooks as on the First level, but using roles
##On both levels, SSL terminating on the load balancer (self-signed or from Let's Encrypt) as a huge plus. 
=====================

 ###  Task's environment:
 #### AWS with four servers:
 #### 1. bastion - management-server with ansible
 #### 2. nginx - server with balancer
 #### 3. web_app - server with web application
 #### 4. db - server with database
 
 #### Type of virtual machines - Ubuntu Server 18.04 LTS (HVM)
 
 #### On the management-server port 22 must be available from the internet
 #### On the nginx server port 8080 must be available from the internet, and port 22 must be available for inner network
 #### On the database and web application servers 22 and 8080 ports must be available only from inner network
------
 ###  Preconditions:
 #### 1. python2.7 is installed on the all servers:
 ##### **sudo apt update && sudo apt install python2.7 mc nano net-tools wget curl -y**
 #### 2. Ansible is installed on the management-server:
 ##### **sudo apt update && sudo apt install software-properties-common && \**
 ##### **sudo apt-add-repository ppa:ansible/ansible && sudo apt install ansible**
 #### 3. All servers have user with sudo
 #### 4. On the management-server path to the private ssh-key was set in  /etc/ansible/ansible.cfg: 
 ##### private_key_file = path-to-private-key 
 ###### (don't forget about **chmod 600 path-to-private-key**)
------
 ###  Task's steps:
 #### On the management-server:
 #### 1. **git clone**
 #### 2. **cd repo_directory**
 #### 3. edit file ansible_hosts:
 ####   set inner ip addresses for nginx, web application and database servers:
 ####   *nginx ansible_host=172.31.XXX.XXX*
 ####   *web_app ansible_host=172.31.YYY.YYY*
 ####   *postgresql ansible_host=172.31.ZZZ.ZZZ*
 ####   
 ####   set fqdn(Public IPv4 DNS) for nginx server:
 ####   *nginx_fqdn=ec2-18-15-116-221.us-east-2.compute.amazonaws.com* - for example
 ####
 ####   set path to the python2.7 interpretor for all servers
 ####   *ansible_python_interpreter=/usr/bin/python2.7*
 ####   
 ####   set ip mask for the inner network:
 ####   *net_mask=172.31.0.0/16*
 ####
 ####   run playbook:
 ####   ***ansible-playbook -i ansible_hosts hw1.yml --vault-password-file ansible_password.txt***
------
### Apllication available with url:
### https://Nginx_Public_IPv4_DNS_here:8080/query
