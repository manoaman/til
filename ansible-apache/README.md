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
- hosts: webservers
  vars_files:
    - vars/main.yml
  roles:
    - { role: geerlingguy.apache }
```

Inside vars/main.yml:

```
apache_listen_port: 8080
apache_vhosts:
  - {servername: "example.com", documentroot: "/var/www/vhosts/example_com"}
```
