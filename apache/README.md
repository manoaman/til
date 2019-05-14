### How to enable mod_proxy_http?

```
sudo a2enmod proxy_http
```

and https based load balancer working, i had to enable the following:

```
sudo a2enmod ssl
sudo a2enmod proxy
sudo a2enmod proxy_balancer
sudo a2enmod proxy_http
```
https://stackoverflow.com/questions/23931987/apache-proxy-no-protocol-handler-was-valid

### How to check Apache modules are enabled and loaded?

```
---------------  On Debian based systems --------------- 
$ apache2ctl -t -D DUMP_MODULES   
OR 
$ apache2ctl -M
```

```
---------------  On RHEL based systems --------------- 
$ apachectl -t -D DUMP_MODULES   
OR 
$ httpd -M
$ apache2ctl -M
```

https://www.tecmint.com/check-apache-modules-enabled/

### How to use SSL proxying?

```
SSLProxyEngine on
ProxyPass /path1 https://hogehoge/somepath
ProxyPassReverse /path1 https://hogehoge/somepath
```

https://stackoverflow.com/questions/25107654/how-to-configure-apache-server-to-talk-to-https-backend-server/25107936

### How to redirect from Apache?

mod_proxy

```
<VirtualHost *:80>
    ServerName example.net
    ProxyPass "/"  "http://www.example.com/page2/"
    ProxyPassReverse "/"  "http://www.example.com/page2/"
</VirtualHost>
```

https://serverfault.com/questions/918033/redirect-web-page-to-another-site-without-changing-url
