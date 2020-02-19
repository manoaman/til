## Vagrant stuffs

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

CentOS
```
% vagrant box add centos6.7 https://github.com/CommanderK5/packer-centos-template/releases/download/0.6.7/vagrant-centos-6.7.box
```

or find a box from Vagrant Cloud.

```
% vagrant init {box name}
// % vagrant init ubuntu/bionic64 # 18.04
```

https://app.vagrantup.com/boxes/search?utf8=%E2%9C%93&sort=downloads&provider=&q=ubuntu


4. Start vagrant

```
% vagrant up
% vagrant status
```
https://qiita.com/takakuda/items/671b25c85378756daa97
https://qiita.com/imasaaki/items/2fd8dd3c251446f557c5

#### How to look at list of boxes?

```
% vagrant box list
```

#### How to portforward with Vagrant?

host (localhost)
guest (e.g.)192.168.100.12)
```
config.vm.network :forwarded_port, guest: 8000, host: 8000
```

https://qiita.com/tn1117/items/e0a03cbd71b842fef57e


### Vargrant commands

```
% vagrant init
% vagrant up
% vagrant halt

% vagrant ssh {host_name}
% vagrant destroy
% vagrant suspend
% vagrant reload
% vagrant resume

% vagrant box list
% vagrant box add ubuntu/bionic64 ---> Ubuntu 18.04

% vagrant status
```

https://qiita.com/w2-yamaguchi/items/191830191f8af05ac4dd
https://qiita.com/tn1117/items/e0a03cbd71b842fef57e

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

-----

#### Ansible?

https://github.com/manoaman/til/blob/master/ansible/README.md
