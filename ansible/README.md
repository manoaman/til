### Set up Ansible

1. SSH into controller

```
% vagrant ssh
```

2. Install Ansible

Ubuntu:

```
% yum install ansible

or 

% sudo apt-get update
% sudo apt-get upgrade -y
% sudo apt-get install ansible -y
% sudo apt-get install python -y
```

MacOS:

```
% curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
% python get-pip.py --user
% pip install --user ansible
```

https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#from-pip


3. Generate SSH key and send the public key

* Create an empty password
```
% ssh-keygen -t rsa
```

4. Copy a public key

```
% ssh-copy-id -i ~/.ssh/id_rsa.pub root@192.168.100.20
```

5. And try ssh again

```
% ssh 'root@192.168.100.20'
```

https://qiita.com/t_nakayama0714/items/fe55ee56d6446f67113c

### Try out Ansible

1. Create an inventory file (`hosts`) in controller

```
% ssh 'root@192.168.100.20'

% mkdir ansible    ----> /home/vagrant/ansible
% cd ansible

% mkdir inventory
```

2. Add target to `hosts`
```
[targets]
192.168.100.20 ansible_user=root
```

3. Test ping
```
% ansible all -i inventory/hosts -m ping
```

for debugging

```
% ansible all -i inventory/hosts -m ping -vvvv
```

### Ansible Playbook

1. Test Playbook

```
% ansible-playbook -i inventory/hosts test.yml
```

`targets.yml`

```
message: "Hello Ansible !"

fruits:
  apples:
    amount: 10
  bananas:
    amount: 20
  oranges:
    amount: 30
```

`test.yml` (Playbook)

```
- hosts: targets
  user: root
  tasks:
    - name: output message.
      debug: msg="{{ message }}"

    - name: output fruits
      debug: msg="We want {{ item.value.amount }} {{ item.key }} !"
      with_dict: "{{ fruits }}"
```

2. Do some real stuffs

`main.yml` (Playbook)

```
- hosts: targets
  user: root
  tasks:
  - name: install packages from yum
    yum: name={{ item }} state=latest
    with_items:
      - jq
      - ruby
      - httpd

  - name: register cron job
    cron: name="check ping" day="*/2" hour="12" minute="0" job="ping -c 3 192.168.100.10"

  - name: create directories
    file: path={{ item.path }} owner={{ item.owner }} group={{ item.group }} mode=0{{ item.mode }} state=directory
    with_items:
      - { "path":"/opt/ansible", "owner":"root", "group":"root", "mode":"755" }
      - { "path":"/opt/vagrant", "owner":"vagrant", "group":"vagrant", "mode":"755" }

  - name: copy files
    copy: src=./files/hoge dest=/opt/ansible/hoge owner=root group=root mode=0755

  - name: copy template files
    template: src=./templates/fuga.j2 dest=/opt/ansible/fuga owner=root group=root mode=0755
```

`fuga.j2` (Jinja)

```
This is a jinja template file.

{{ message }}

jinja template can extract variables. like, ...

{% for key,value in fruits.iteritems() %}
We want {{ value.amount }} {{ key }} !
{% endfor %}
```

3. Dry run with check mode

```
% ansible-playbook --check -i inventory/hosts main.yml

or 

% ansible-playbook --check -i inventory/hosts main.yml -vvv
```

4. Run

```
% ansible-playbook -i inventory/hosts main.yml
```

### Ansible roles

`master.yml`
```
- hosts: targets
  user: root
  tasks:
  - name: register cron job
    cron: name="check ping" day="*/2" hour="12" minute="0" job="ping -c 3 192.168.100.10"

  roles:
  - role-common
  - role-web
```

```
% ansible-playbook --check -i inventory/hosts master.yml
```

### What is a Ansible inventory file?

> The Ansible inventory file defines the hosts and groups of hosts upon which commands, modules, and tasks in a playbook operate.


### What is a Ansible playbook file?

> An Ansible playbook is an organized unit of scripts that defines work for a server configuration managed by the automation tool Ansible. Ansible is a configuration management tool that automates the configuration of multiple servers by the use of Ansible playbooks.

----



#### How to include Ansible ssh vagrant user in a config file?

```
[all:vars]
ansible_connection=ssh
ansible_user=vagrant
ansible_ssh_pass=vagrant
```
https://serverfault.com/questions/628989/how-to-set-default-ansible-username-password-for-ssh-connection


#### Ansible reference guide

1. connecting with a user name

```
% ansible all -m ping -u sammy
% ansible-playbook myplaybook.yml -u sammy

```

https://www.digitalocean.com/community/cheatsheets/how-to-use-ansible-cheat-sheet-guide

#### How to setup Tomcat?

https://github.com/manoaman/til/tree/master/ansible-tomcat

#### How do I see a list of all of the ansible_ variables?

```
% ansible -m setup hostname
```
https://docs.ansible.com/ansible/latest/reference_appendices/faq.html#how-do-i-see-a-list-of-all-of-the-ansible-variables
https://stackoverflow.com/questions/18839509/where-can-i-get-a-list-of-ansible-pre-defined-variables

----

### Resources

https://medium.com/@JohnFoderaro/macos-sierra-vagrant-quick-start-guide-2b8b78913be3
https://www.vagrantup.com/intro/getting-started/teardown.html
https://qiita.com/andrew954/items/1d9f460558da7b84768f
http://arika.hateblo.jp/entry/2014/06/08/220206


