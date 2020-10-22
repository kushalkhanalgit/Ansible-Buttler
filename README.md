## Ansible-Buttler
Create a light weight automation ecosystem using Ansible

## Install CentOS  
a) Not as WSL but I recommend having a VM machine where you can spin-up your CentOS. I have used 8.3.1 version on VMware workstation.
Use link : https://wiki.centos.org/Download , to download appropriate ISO.  
b) Simply have a new VM created - my VM has 20GB harddisk , 8GB RAM and 12 core CPUs; and point to your ISO. You can easily find guides in internet if you go wrong at some points.
But its pretty straight forward

## Install Python3 on CentOS

=====================================================  
#dnf - dandified is new version of yum  
$ sudo dnf install python3  
#verify : where and which Python?  
$ python --version  
$ which python  

======================================================  

## Install Ansible on the CentOS  

======================================================================================================================================
#install ansible via Python's pip package not EPEL library of CentOS  
$pip3 install ansible  
#verify installation  
$which ansible  
$anisble --version  
#Note that if ansible was installed via EPEL of CentOS, we would find files like ansible.cfg, hosts in /etc/ansible folder;  
#and it doesn't matter, you just need to point in the command where your host file is or your host with '-i' switch.  
#refer : https://github.com/ansible/ansible/issues/18512 ; 
#Further : Inventory files are explained here: http://docs.ansible.com/ansible/intro_inventory.html to learn how to add hosts

#+++++++++++++++++++++++ Example#1 : call host by IP ++++++++++++++++++++++++++++++++++++++++++++++++++++++++
#format is :   $ansible 'host1' -m command [-u user_name]
#[root@192-168-1-108 ansible-buttler]# ansible  '127.0.0.1' -m ping
#[WARNING]: No inventory was parsed, only implicit localhost is available
#127.0.0.1 | SUCCESS => {
#"changed": false,  
#"ping": "pong"  
#}
#++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
#Note that above ping is not ICMP ping; for this ping to be sucess. the device to be pinged, should be reachable via SSH.  
#Example :
#+++++++++++++++++++++++++ Example#2 : call host by group under file name +++++++++++++++++++++++++++++++++  
#format is :   $ansible 'host1' -i file_name group_name_in_file -m command [-u user_name]  
#[root@192-168-1-108 ansible-buttler]# ansible -i inventory linux_servers -m ping  
#192.168.1.102 | SUCCESS => {  
#"ansible_facts": {  
#"discovered_interpreter_python": "/usr/bin/python"  
#},  
#"changed": false, 
#"ping": "pong"  
#}
#++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  

========================================================================================================================================  






