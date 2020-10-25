## Ansible-Buttler
Create a light weight automation ecosystem using Ansible

## Install CentOS  
a) Not as WSL but I recommend having a VM machine where you can spin-up your CentOS. I have used 8.3.1 version on VMware workstation.  
Use link : https://wiki.centos.org/Download , to download appropriate ISO.  
b) Simply have a new VM created - my VM has 20GB harddisk , 8GB RAM and 12 core CPUs; and point to your ISO. You can easily find guides in internet if you go wrong at some points.
But its pretty straight forward

## Install Python3 on CentOS

==============================================================================    
#dnf - dandified is new version of yum  
$ sudo dnf install python3  
#verify : where and which Python?  
$ python --version  
$ which python  

===============================================================================

## Install Ansible on the CentOS  

===============================================================================  
#install ansible via Python's pip package not EPEL library of CentOS  
$pip3 install ansible  
#verify installation  
$which ansible  
$anisble --version  
#Note that if ansible was installed via EPEL of CentOS, we would find files like ansible.cfg, hosts in /etc/ansible folder;  
#and it doesn't matter, you just need to point in the command where your host file is or your host with '-i' switch.  
#refer : https://github.com/ansible/ansible/issues/18512 ; 
#Further : Inventory files are explained here: http://docs.ansible.com/ansible/intro_inventory.html to learn how to add hosts

#+++++++++++++++++++ Example#1 : call host by IP +++++++++++++++++++  
#format is :   $ansible 'host1' -m command [-u user_name]
#[root@192-168-1-108 ansible-buttler]# ansible  '127.0.0.1' -m ping
#[WARNING]: No inventory was parsed, only implicit localhost is available
#127.0.0.1 | SUCCESS => {
#"changed": false,  
#"ping": "pong"  
#}  
#++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++     
#Note that above ping is not ICMP ping; for this ping to be sucess. the device to be pinged, should be reachable via SSH.  

#+++++ Example#2 : call host by group under file name ++++++++++++++++  
#format is :   $ansible 'host1' -i file_name group_name_in_file -m command [-u user_name]  
#[root@192-168-1-108 ansible-buttler]# ansible -i inventory linux_servers -m ping  
#192.168.1.102 | SUCCESS => {  
#"ansible_facts": {  
#"discovered_interpreter_python": "/usr/bin/python"  
#},  
#"changed": false,  
#"ping": "pong"  
#}  
#++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  

==================================================================================  

## Create free DevNet account in Cisco cloud network simulator : VIRL sandbox  

===================================================================================   

#Refer to following instrution from David on how to create it :  
#https://www.youtube.com/watch?v=TmGNtvh1eeY  
#Basically, we will now get a server where we can ssh onto ; then we use one sandbox     
#which has inventory of Cisco XE in order to perform some programming  
#Once you create your account and loginto : http://bit.ly/freecml , go to  
#'SANDBOX LABS' next to 'RESERVATIONS'. Remember we are not reserving a slot to  
#perform lab. On left to 'BROWSE BY CATEGORY' , in the drop-down select 'Always-On'.  
#Select 'IOS XE on CSR Recommended Code AlwaysOn'. Now in 'INSTRUCTIONS' tab, if you   
#browse down, you will have details how to connect to this IOS XE under 'Access Details'  

#test SSH to this offered device :  
$ssh -v developer@ios-xe-mgmt.cisco.com -p 8181  
# Test connection via Ansible
#prepare a file to be used for connection. Example : check 'inventory' in 
#files list.  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
#Ensure you have paramiko (for ssh sessions to NE) with : $pip3 show paramiko.    
#Else install it as : $pip3 install paramiko  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
#Ping test ( note: this is not ICMP, and Ansible needs to be able to ssh end  
#host for this to be success.  
$ansible -i inventory virl_router -m ping  

#now if we want to send ad-hoc commands as if we are inside router,where we need to  
#mention to i) file where IP element or servers are ii) which group we want to play  
#in the file iii)this being Cisco , command type is ios_command, then with switch 'a'  
#we mention what command we want to push  
$ansible -i inventory virl_router -m ios_command -a "commands='show ip interface brief'"                                  

============================================================================  
# Run playbooks for Ansible - "Hello world " kind
#Create some playbook in yaml or yml file. Refer into the repository : as
#basic_playbook_add_interface.yml and basic_playbook_add_interface_with_sanity.yml
#first one just configures a loopback and second one builds up: performs some sanity
#checks
$ansible-playbook -i inventory  basic_playbook_add_interface_with_sanity.yml






