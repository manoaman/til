## Ansible Apache

1. Install Ansible Galaxy roles

```
% ansible-galaxy install geerlingguy.apache
```

2. Clone the repo

```
% https://github.com/geerlingguy/ansible-role-apache
```

3. Example Playbook

```
- hosts: apache-nodes
  become: yes
  vars_files:
    - vars/main.yml
  roles:
    - { role: geerlingguy.apache }
```

Inside vars/main.yml:

```
apache_listen_port: 80
apache_vhosts:
  - {servername: "example.com", documentroot: "/var/www/vhosts/example_com"}
```

Note: Don't forget to make `sudo` eligible.

Ansible 1.9.4 : Failed to lock apt for exclusive operation
https://stackoverflow.com/questions/33563425/ansible-1-9-4-failed-to-lock-apt-for-exclusive-operation
