# MySQL

1. Install Ansible Galaxy roles

```
% ansible-galaxy install geerlingguy.mysql
```


2. Clone Ansible roles repo from Ansible Galaxy

```
% git clone https://github.com/geerlingguy/ansible-role-mysql.git
```

https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html
https://dev.classmethod.jp/cloud/aws/ansible-galaxy-intro/
https://galaxy.ansible.com/geerlingguy/mysql


3. Fix pymysql

```
% vi tasks/setup-Debian.yml 
```
```
- name: Make sure pymysql is present
  become: true # needed if the other tasks are not played as root
  pip:
    name: pymysql
    state: present
```

https://stackoverflow.com/questions/56313083/ansible-ubuntu-18-04-mysql-the-pymysql-python-2-7-and-python-3-x-or-mys


4. Set root password

```
% vi vars/main.yml
```
```
mysql_root_password: super-secure-password
```
