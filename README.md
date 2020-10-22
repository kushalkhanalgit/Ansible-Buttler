## Ansible-Buttler
Create a light weight automation ecosystem using Ansible

#Install CentOS  
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

==================================
#install ansible via Python's pip package not EPEL library of CentOS  
$pip3 install ansible  
#verify installation  
$which ansible  
$anisble --version  

==================================  
