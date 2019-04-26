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