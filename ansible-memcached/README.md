## Ansible Memcached

1. Install Ansible Memcached roles

```
% ansible-galaxy install geerlingguy.memcached
```

https://galaxy.ansible.com/geerlingguy/memcached

2. Download repo

```
% git clone https://github.com/geerlingguy/ansible-role-memcached
```

3. Example Playbook

```
% vi memcached-playbook.yml

- hosts: memcached-nodes 
  become: yes
  roles:
    - { role: geerlingguy.memcached }
```

4. Run

```
% ansible-playbook -i hosts memcached-playbook.yml
```
