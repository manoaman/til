### MySQL


#### How to check the history of MySQL commands

```
 cat ~/.mysql_history
```

#### How to disable strict mode?

a. From a command line
```
$ mysql -u root -p -e "SET GLOBAL sql_mode = 'NO_ENGINE_SUBSTITUTION';" 

$ mysql -u root -p -e "SELECT @@GLOBAL.sql_mode;"
```
https://www.linode.com/community/questions/17070/how-can-i-disable-mysql-strict-mode

b. From a configuration files

/etc/mysql/conf.d/diable_strict_mode.cnf
```
[mysqld]
sql_mode=IGNORE_SPACE,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION
```
https://www.linode.com/community/questions/17070/how-can-i-disable-mysql-strict-mode

#### How to output MySQL query?

```
SELECT order_id,product_name,qty
FROM orders
WHERE foo = 'bar'
INTO OUTFILE '/var/lib/mysql-files/orders.csv'
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n';
```

`/var/lib/mysql-files/` is where files can be written on the server.

https://stackoverflow.com/questions/356578/how-to-output-mysql-query-results-in-csv-format


#### Workaround for missing definer?

Option 1. Create the user.
Option 2. Change the current definer to someone else.


https://stackoverflow.com/questions/10169960/mysql-error-1449-the-user-specified-as-a-definer-does-not-exist

#### How to restore database from ".sql.gz" file?

```
% zcat hogehoge.sql.gz | mysql -u root -p hogedataase
```
