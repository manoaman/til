### Apple

#### How to show hidden files?

1. Open Terminal found in Finder > Applications > Utilities.
2. In Terminal, paste the following: defaults write com.apple.finder AppleShowAllFiles YES.
3. Press return.
4. Hold the 'Option/alt' key, then right click on the Finder icon in the dock and click Relaunch.

#### How to upgrade chromedriver?

```
% npm install chromedriver
% sudo ln -s /Users/seita/node_modules/chromedriver/lib/chromedriver/chromedriver /usr/local/bin/chromedriver
% /usr/local/bin/chromedriver -version
ChromeDriver 74.0.3729.6 (255758eccf3d244491b8a1317aa76e1ce10d57e9-refs/branch-heads/3729@{#29})
```
https://www.kenst.com/2015/03/installing-chromedriver-on-mac-osx/

#### How to diagnose WiFi connection on Mac?

`alt + (click on the WiFi menu)`

https://support.apple.com/en-us/HT202663#howto


#### How to count CPU cores and RAM size from terminal?

```
% sysctl -n hw.ncpu
4

% sysctl hw.memsize
hw.memsize: 8589934592

```

https://serverfault.com/questions/112711/how-can-i-get-cpu-count-and-total-ram-from-the-os-x-command-line


#### How to delete old back ups from TimeMachine?

```
tmutil delete /Volumes/BackupDriveName/Backups.backupdb/MacComputerName/YYYY-MM-DD-HHMMSS/
```

#### How to allow a remote computer to access your Mac

>Set up Remote Login on your Mac
>On your Mac, choose Apple menu  > System Preferences, click Sharing, then select Remote Login.

>Select the Remote Login checkbox.

>Selecting Remote Login also enables the secure FTP (sftp) service.

>Specify which users can log in:

>All users: Any of your computer’s users and anyone on your network can log in.

>Only these users: Click the Add button , then choose who can log in remotely. Users & Groups includes all the users of your Mac. Network Users and Network Groups include people on your network.

https://support.apple.com/guide/mac-help/allow-a-remote-computer-to-access-your-mac-mchlp1066/mac

