# Connect-Ansible-with-EC2-Instance

Step 1: download the private key of ec2 instance

create a private key with "key Pairs" feature,
or while creating ec2 instance on AWS at the end of instance creating process aws ask 
to download the private key, with help of this key we can connect with instance.

Till here you launched your ec2 instance.

-----------------------------------------------------------------------------------
Step 2: remove read permission of (group user + other user) from the key
```	
[ ]# chmod g-r key_filename.pem

[ ]# chmod o-r key_filename.pem
```
-----------------------------------------------------------------------------------
Step 3: Setup inventory where you installed Ansible
```
[ ]# vi /etc/ansible/hosts
[aws]
ec2_public_ip ansible_user=ec2-user ansible_ssh_private_key_file=/root/Downloads/private_key.pem

```
Note: /root/Downloads/private_key.pem == paste the path of "private key"

-----------------------------------------------------------------------------------
Step 4: setup privilege_escalation in controlled node so we can run cmds with
	      "sudo" power behind the sence by Ansible in ec2 instance.
```
[ ]# vi /etc/ansible/ansible.cfg
	
# host_key_checking=False
	
[privilege_escalation]
become=True    
become_method=sudo
become_user=root
become_ask_pass=False

[ ]#
```

Note:
`#RRGGBB` become=True            <---- means i want to use become concept of becoming some other user.
`#RRGGBB` become_method=sudo     <---- i want to become some other user to gain extra power to run cmd's by using "sudo"
`#RRGGBB` become_user=root       <---- i want to become "root" user, you can change user name also as required.
`#RRGGBB`become_ask_pass=False  <---- means dont ask password to run cmd's after becoming some other user
                                to work this option need to setup inventory.

-----------------------------------------------------------------------------------------------------------------------------
Step 5: Now create any playbook or run any ad-hoc cmd it will run in the ec2 instance.


-----------------------------------------------------------------------------------------------------------------------------
That's all..!
          
          
          
          
          
          
          
          
  
