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


