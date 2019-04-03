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
