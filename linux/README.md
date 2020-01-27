### Linux


#### How to find a file?

```
find / -name abc.dmg
```

#### How to list directories?

```
ls -ld /path/to/directory/*/
```
or
```
ls -l /hoge/hoge/* | grep '^d'
```


#### How to list groups?

```
% groups
```

```
% groups username
```


#### How to add a existing user to a group?

```
% usermod -a -G examplegroup exampleusername

```

#### YYYY-MM-dd format in shell script

```
# put current date as yyyy-mm-dd in $date
date=$(date '+%Y-%m-%d')

# put current date as yyyy-mm-dd HH:MM:SS in $date
date=$(date '+%Y-%m-%d %H:%M:%S')

# print current date directly
echo $(date '+%Y-%m-%d')
```

#### Test for empty directory

```
if [ -z "$(ls -A /path/to/dir)" ]; then
   echo "Empty"
else
   echo "Not Empty"
fi
```

#### What is a cron format?

```
# ┌───────────── minute (0 - 59)
# │ ┌───────────── hour (0 - 23)
# │ │ ┌───────────── day of the month (1 - 31)
# │ │ │ ┌───────────── month (1 - 12)
# │ │ │ │ ┌───────────── day of the week (0 - 6) (Sunday to Saturday;
# │ │ │ │ │                                   7 is also Sunday on some systems)
# │ │ │ │ │
# │ │ │ │ │
# * * * * * command to execute
```
https://en.wikipedia.org/wiki/Cron

Cron format online tester:

http://cron.schlitt.info/

Cron on Mac:
https://medium.com/better-programming/https-medium-com-ratik96-scheduling-jobs-with-crontab-on-macos-add5a8b26c30

#### How to debug and check if cron is working?


Check the log
```
sleep 60; grep crontab /var/log/syslog | tail
```
https://serverfault.com/questions/43733/is-there-a-way-to-validate-etc-crontab-s-format

```
/usr/local/bin/some_script.sh >> /tmp/cron.out
```

https://stackoverflow.com/questions/13280699/crontab-is-not-running-my-script/13285588

#### How to count CPU cores?

```
grep -c ^processor /proc/cpuinfo    
```

https://stackoverflow.com/questions/6481005/how-to-obtain-the-number-of-cpus-cores-in-linux-from-the-command-line

#### How to output in stderr and output in a file and the console?

```
% SomeCommand 2>&1 | tee SomeFile.txt

```
https://askubuntu.com/questions/420981/how-do-i-save-terminal-output-to-a-file

#### How do I run graphical programs remotely from a Linux server?

1. Install XQuartz on your Mac, which is the official X server software for Mac
2. Run Applications > Utilities > XQuartz.app
3. Right click on the XQuartz icon in the dock and select Applications > Terminal.  This should bring up a new xterm terminal windows.
4. ssh in

https://uisapp2.iu.edu/confluence-prd/pages/viewpage.action?pageId=280461906

https://www.xquartz.org/

https://unix.stackexchange.com/questions/9870/how-do-i-work-with-gui-tools-over-a-remote-server

#### How to use duc to look at disk space usage?

https://duc.zevv.nl/

Index
```
$ duc index /usr
```

List all the files and tree views
```
$ duc ls -Fg /usr/local

$ duc ls -R /usr/local
```

GUI
```
$ duc gui /usr/local
```

https://htmlpreview.github.io/?https://github.com/zevv/duc/blob/master/doc/duc.1.html#EXAMPLES


#### How to mount an external hard drive?

```
% sudo fdisk -l
% sudo mount /dev/sdxn /mnt
% sudo umount /mnt
```
Kill the process if mount is used.

```
% sudo fuser -km /mnt
```

#### How to unmount?

```
% umount -l /PATH/OF/BUSY-DEVICE
% umount -f /PATH/OF/BUSY-NFS(NETWORK-FILE-SYSTEM)
```

https://askubuntu.com/questions/867719/umount-target-is-busy

#### How to mount unmountable external drive?

Check fsck is runng.

```
% ps aux | grep fsck

% sudo kill -9 xxxx
(% sudo pkill -f fsck)
```
https://apple.stackexchange.com/questions/268998/external-hard-drive-wont-mount

#### USB drive format choices

```
If you absolutely, positively will only be working with Macs and no other system, ever: Use Mac OS Extended (Journaled).

If you need to transfer files larger than 4 GB between Macs and PCs: Use exFAT.

In all other cases: Use MS-DOS (FAT), aka FAT32.
```
https://www.engadget.com/2011/09/19/mac-101-format-choices-for-usb-flash-drives/?guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAEUslRePgVafLCIxwjto5VUkeo1NDwA3-CItjI0qZgVzayM6Aan9Ku8rvAAxq0VvCkixXdY-URkAy9zF5nGeOnm5xoFIwqdxQsl_-4DwtnZeEyAitgClxcxLWU_2FkB9ov4AKpn23zcGSe1E51hqYybUqyF48GG9Ru6EUgiCq2kS


#### inode limit issue on Ubuntu

```
% df -i
% for dir in `ll|grep ^d|grep -v "\./"|awk '{print $9}'`; do echo `sudo find ./$dir -true|wc -l` `pwd`/$dir; done | sort -nr
% sudo apt-get autoremove
```

https://qiita.com/kyrieleison/items/74b0a1035494b5885e05
http://lab.astamuse.co.jp/entry/2018/03/15/114500
https://thegeeksalive.com/how-to-find-the-inode-usage-on-linux/


#### How to copy and exclude multiple directories/files?

```
% rsync -av --progress sourcefolder /destinationfolder --exclude thefoldertoexclude

% rsync -a /etc/fstab /home/user/download bkp
```
https://stackoverflow.com/questions/4585929/how-to-use-cp-command-to-exclude-a-specific-directory
https://unix.stackexchange.com/questions/368210/how-to-rsync-multiple-source-folders

#### How to get hardware spec?

```
% uname
% lshw -short
% lscpu
% lsblk
```

https://vitux.com/get-linux-system-and-hardware-details-on-the-command-line/

#### How to install Glances and monitor with web gui?

```
% sudo apt install glances python-bottle	#Debian/Ubuntu
% sudo pip install bottle
% glances -w &

http://SERVER_IP:61208/
```

https://www.tecmint.com/glances-monitor-remote-linux-in-web-server-mode/

#### What are rsync options?

https://linux.die.net/man/1/rsync
