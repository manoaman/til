### Linux


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
