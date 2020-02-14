### Set up VirutalBox and Vagrant

1. Set up VirtualBox

```
% /Applications/VirtualBox.app/Contents/MacOS/VBoxManage -v

6.0.12r133076
```

2. Install vagrant

```
% brew cask install vagrant
% vagrant -v
```

3. Add a box

```
% vagrant box add centos6.7 https://github.com/CommanderK5/packer-centos-template/releases/download/0.6.7/vagrant-centos-6.7.box
```

or find a box from Vagrant Cloud.

```
% vagrant init {box name}
```

https://app.vagrantup.com/boxes/search?utf8=%E2%9C%93&sort=downloads&provider=&q=ubuntu


4. Start vagrant

```
% vagrant up
% vagrant status
```

### Set up Ansible

1. SSH into controller

```
% vagrant ssh
```

2. Install Ansible

```
% yum install ansible

or 

% sudo apt-get update
% sudo apt-get ansible install
```

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

## Vagrant stuffs

### Vargrant commands

```
% vagrant init
% vagrant up
% vagrant ssh
% vagrant halt
% vagrant destroy
% vagrant suspend
% vagrant reload
% vagrant resume

% vagrant box list
% vagrant box add ubuntu/bionic64 ---> Ubuntu 18.04
```

https://qiita.com/w2-yamaguchi/items/191830191f8af05ac4dd

### What to do if Vagrant cannot be installed?

```
% sudo sed -i "s/mirrorlist=https/mirrorlist=http/" /etc/yum.repos.d/epel.repo
% yum install ansible
```
$ sudo sed -i "s/mirrorlist=https/mirrorlist=http/" /etc/yum.repos.d/epel.repo


### What is Vagrant mainly used for?

> Vagrant is a tool for building and managing virtual machine environments in a single workflow. With an easy-to-use workflow and focus on automation, Vagrant lowers development environment setup time, increases production parity, and makes the "works on my machine" excuse a relic of the past.

### cowsay + Ansible

```
% yum install cowsay
```

Set up
```
% vi ~/.bash_profile

export ANSIBLE_COW_SELECTION=stegosaurus
```

To check what's in
```
% cowsay -l
```

### Resources

https://medium.com/@JohnFoderaro/macos-sierra-vagrant-quick-start-guide-2b8b78913be3
https://www.vagrantup.com/intro/getting-started/teardown.html
https://qiita.com/andrew954/items/1d9f460558da7b84768f
http://arika.hateblo.jp/entry/2014/06/08/220206
