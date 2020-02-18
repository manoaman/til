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

#### Ansible?

https://github.com/manoaman/til/blob/master/ansible/README.md
