## How to install Tomcat with Ansible?

1. Install Ansible

```
% sudo apt-get update
% sudo apt-get install software-properties-common
% sudo apt-add-repository ppa:ansible/ansible
% sudo apt-get update
% sudo apt-get install ansible
% ansible 192.168.100.12 -m ping
```


2. Download Ansible Tomcat stuffs

```
% git clone https://github.com/jmutai/tomcat-ansible.git
% cd tomcat-ansible
```

3. Modify "hosts" file to make vagrant ssh user accessible and add target node ip

```
[all:vars]
ansible_connection=ssh
ansible_user=vagrant
ansible_ssh_pass=vagrant
# https://serverfault.com/questions/628989/how-to-set-default-ansible-username-password-for-ssh-connection


# [tomcat-nodes]
# 192.168.100.12 # Add Server IP address, one line per server
```

4. Run Ansible Playbook

```
% ansible-playbook -i hosts tomcat-setup.yml
```

https://medium.com/@atultyagi842/ansible-playbook-to-install-tomcat-and-run-application-on-ubuntu-16-04-ad8e5557f117
https://computingforgeeks.com/install-tomcat-on-ubuntu-centos-with-ansible/
https://github.com/mouseconnectomeproject/tomcat-ansible
