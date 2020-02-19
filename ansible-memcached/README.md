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

5. Check Memcached usage

```
% memcached -vv
or
% echo stats | nc 127.0.0.1 11211  ---> Assuming the port is 11211
```

https://drupal.stackexchange.com/questions/228462/how-to-test-if-memcache-is-working
