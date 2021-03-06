## Ubuntu


### Setting up unattended upgrades

1. Package Installation

sudo apt install unattended-upgrades


2. Configure unattended upgrades

```
sudo nano /etc/apt/apt.conf.d/50unattended-upgrades
```

The most important: uncomment the “updates” line by deleting the two slashes at the beginning of it:
"${distro_id}:${distro_codename}-updates";

Optional: You should uncomment and adapt the following lines to ensure you’ll be notified if an error happens:
```
Unattended-Upgrade::Mail "user@example.com";
Unattended-Upgrade::MailOnlyOnError "true";
```

Recommended: remove unused kernel packages and dependencies and make sure the system automatically reboots if needed by uncommenting and adapting the following lines:
```
Unattended-Upgrade::Remove-Unused-Kernel-Packages "true";
```

```
Unattended-Upgrade::Remove-Unused-Dependencies "true";
Unattended-Upgrade::Automatic-Reboot "true";
Unattended-Upgrade::Automatic-Reboot-Time "02:38";
```


Nano

```
To save your changes in nano, use Ctrl + O followed by Enter. To quit, use Ctrl + X.
```

3. Enable Automatic Updates

Enable automatic updates and set up update intervals by running:
```
sudo nano /etc/apt/apt.conf.d/20auto-upgrades
```

In most cases, the file will be empty. Copy and paste the following lines:

```
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Download-Upgradeable-Packages "1";
APT::Periodic::AutocleanInterval "7";
APT::Periodic::Unattended-Upgrade "1";
```

The time interval are specified in days, feel free to change the values. Save changes and exit.

4. Dry run

You can see if the auto-upgrades work by launching a dry run:
sudo unattended-upgrades --dry-run --debug

Another way to check if automatic updates work is waiting a few days and checking the unattended upgrades logs:
```
cat /var/log/unattended-upgrades/unattended-upgrades.log
```

https://libre-software.net/ubuntu-automatic-updates/


---

### NFS mount

In order to mount,
```
% sudo mount -a
```

Unmount,
```
% sudo unmount
```

mount information
```
% cat /proc/mounts

or

% df -h
```

Make sure you have `nfs-common` on the client,

```
% sudo apt update
% sudo apt install nfs-common
```
https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-18-04

Configure /etc/fstab

```
# /etc/fstab: static file system information.
# 
# Use 'blkid' to print the universally unique identifier for a
# device; this may be used with UUID= as a more robust way to name devices
# that works even if disks are added and removed. See fstab(5).
#
# <file system> <mount point>   <type>  <options>       <dump>  <pass>


nfs-hogehoge.edu:/ifs/abc/def/ghi              /ifs/abc        nfs     proto=tcp       0       0
nfs-hogehoge.edu:/ifs/abc/def    /ifs/abc/def    nfs     proto=tcp       0       0
```

---

### Kill a process listening to a certain port (8080)

```
% sudo kill `sudo lsof -t -i:8080`
```

check what process id is listening,
```
% fuser 8080/tcp
```

https://stackoverflow.com/questions/9346211/how-to-kill-a-process-on-a-port-on-ubuntu
https://stackoverflow.com/questions/11583562/how-to-kill-a-process-running-on-particular-port-in-linux

### How to enable/disable a service on system startup

Enable
```
% systemctl enable <service>
```

Disable
```
% systemctl disable <service>
```

Check what services are available
```
% service --status-all
```

List enabled ones
```
% systemctl list-unit-files | grep enabled
```

https://askubuntu.com/questions/698993/disable-services-on-startup-in-ubuntu
https://askubuntu.com/questions/795226/how-to-list-all-enabled-services-from-systemctl

#### How to force "yes" on installation?

```
apt-get --yes --force-yes install $something
```
https://superuser.com/questions/164553/automatically-answer-yes-when-using-apt-get-install

#### How to screen capture a selected area

```
Shift+PrtSc
```

https://askubuntu.com/questions/170163/how-do-i-set-a-shortcut-to-screenshot-a-selected-area

#### How to remove Tomcat?

```
sudo apt remove --purge tomcat8 tomcat8-docs
sudo apt autoremove
sudo apt autoclean
```

and some files can be manually deleted after you do,

```
sudo apt install locate && sudo updatedb
locate tomcat
```

#### How to install chromedriver?

https://tecadmin.net/setup-selenium-chromedriver-on-ubuntu/

Prerequisite
```
sudo apt-get update
sudo apt-get install -y unzip xvfb libxi6 libgconf-2-4

sudo apt-get install default-jdk 
```

Install Chrome

Install
```
wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add - 
sudo sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list'
sudo apt-get update 
sudo apt-get install google-chrome-stable
```

Update
```
sudo apt-get --only-upgrade install google-chrome-stable
```

Install via http://askubuntu.com/questions/510056/how-to-install-google-chrome

Install Chrome Driver
```
wget https://chromedriver.storage.googleapis.com/2.41/chromedriver_linux64.zip
unzip chromedriver_linux64.zip

sudo mv chromedriver /usr/bin/chromedriver
sudo chown root:root /usr/bin/chromedriver
sudo chmod +x /usr/bin/chromedriver
```

https://tecadmin.net/setup-selenium-chromedriver-on-ubuntu/

Install PhantomJS

Before installing PhantomJS, you will need to install some required packages on your system. You can install all of them with the following command:

```
sudo apt-get install build-essential chrpath libssl-dev libxft-dev libfreetype6-dev libfreetype6 libfontconfig1-dev libfontconfig1 -y
```

Next, you will need to download the PhantomJS. You can download the latest stable version of the PhantomJS from their official website. Run the following command to download PhantomJS:

```
sudo wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
```
Once the download is complete, extract the downloaded archive file to desired system location:

```
sudo tar xvjf phantomjs-2.1.1-linux-x86_64.tar.bz2 -C /usr/local/share/
```
Next, create a symlink of PhantomJS binary file to systems bin dirctory:
```
sudo ln -s /usr/local/share/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin/
```

https://www.vultr.com/docs/how-to-install-phantomjs-on-ubuntu-16-04


#### How to deal with disconnected ssh terminals?

```
% screen
```
and
```
% screen -r
```
https://serverfault.com/questions/19634/how-to-reconnect-to-a-disconnected-ssh-session
https://askubuntu.com/questions/315408/open-terminal-with-multiple-tabs-and-execute-application


#### How to copy files over to another location by excluding tif files?

```
rsync -av --exclude='*.tif' /hogehoge/tiffs /hogehoge2/nontiffs
```
https://open-groove.net/linux-command/rsync-exclude/

#### How to install PIP and Selenium?

```
$ sudo apt-get install python-pip
$ sudo pip install selenium
```

https://askubuntu.com/questions/937770/how-to-install-and-set-up-selenium-webdriver-on-ubuntu-16-04

#### Which application is using port 8080?

Find out what process is using 8080.

```
% lsof -i :8080 | grep LISTEN
% ps -ef | grep 10165
```

```
% netstat -nlp | grep 8080
```

https://www.mkyong.com/linux/linux-which-application-is-using-port-8080/


#### How to update sudoers with NOPASSWD?

```
myuser ALL=(ALL) NOPASSWD:ALL
```
https://askubuntu.com/questions/334318/sudoers-file-enable-nopasswd-for-user-all-commands


#### How to ssh login without password?

```
How to do it
First log in on A as user a and generate a pair of authentication keys. Do not enter a passphrase:

a@A:~> ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/a/.ssh/id_rsa): 
Created directory '/home/a/.ssh'.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/a/.ssh/id_rsa.
Your public key has been saved in /home/a/.ssh/id_rsa.pub.
The key fingerprint is:
3e:4f:05:79:3a:9f:96:7c:3b:ad:e9:58:37:bc:37:e4 a@A
Now use ssh to create a directory ~/.ssh as user b on B. (The directory may already exist, which is fine):

a@A:~> ssh b@B mkdir -p .ssh
b@B's password: 
Finally append a's new public key to b@B:.ssh/authorized_keys and enter b's password one last time:

a@A:~> cat .ssh/id_rsa.pub | ssh b@B 'cat >> .ssh/authorized_keys'
b@B's password: 
From now on you can log into B as b from A as a without password:

a@A:~> ssh b@B
```

http://www.linuxproblem.org/art_9.html

#### What do you do when the terminal doesn't launch?

Install `xterm` and check if `/var/log/syslog` has something.

https://qiita.com/TaroNakasendo/items/974c5a4de6b6ad566224

#### How to check Tomcat version?

```
% /usr/share/tomcat8/bin/version.sh 
/usr/share/tomcat8/bin/catalina.sh: 1: /usr/share/tomcat8/bin/setenv.sh: JAVA_OPTS: not found
Using CATALINA_BASE:   /usr/share/tomcat8
Using CATALINA_HOME:   /usr/share/tomcat8
Using CATALINA_TMPDIR: /usr/share/tomcat8/temp
Using JRE_HOME:        /usr
Using CLASSPATH:       /usr/share/tomcat8/bin/bootstrap.jar:/usr/share/tomcat8/bin/tomcat-juli.jar
Server version: Apache Tomcat/8.0.32 (Ubuntu)
Server built:   Dec 10 2018 14:08:07 UTC
Server number:  8.0.32.0
OS Name:        Linux
OS Version:     4.4.0-130-generic
Architecture:   amd64
JVM Version:    1.8.0_212-8u212-b03-0ubuntu1.16.04.1-b03
JVM Vendor:     Oracle Corporation
```
