### Docker

#### How to install and configure to start a Docker daemon (Ubuntu)

Remove the existing docker stuffs,

```
$ sudo apt-get remove docker docker-engine docker.io containerd runc

```

Add a repository,
```
sudo apt-get update
```
```
$ sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common
```
```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
```
$ sudo apt-key fingerprint 0EBFCD88
```
```
$ sudo add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable"
```

Install Docker CE,
```
$ sudo apt-get update
```
```
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
```

verify that the install is finished.
```
$ sudo docker run hello-world
```

https://docs.docker.com/install/linux/docker-ce/ubuntu/

#### Post installation steps for Docker CE

Manage Docker as a non-root user
```
$ sudo groupadd docker
```
```
$ sudo usermod -aG docker $USER
```

Verify without using `sudo`
```
$ docker run hello-world
```

#### Configure Docker to start on boot

Systemd

Enable
```
$ sudo systemctl enable docker
```

Disable
```
$ sudo systemctl disable docker
```

#### Configuring remote access with systemd unit file

Edit `docker.service`
```
sudo systemctl edit docker.service
```

Save with the following configuration.
```
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://127.0.0.1:2375
```

Reload the systemctl configuration.

```
 $ sudo systemctl daemon-reload
```

Restart Docker.
```
$ sudo systemctl restart docker.service
```

https://docs.docker.com/install/linux/linux-postinstall/#configure-docker-to-start-on-boot
https://docs.docker.com/config/daemon/

#### How to stop all the containers

```
% docker container stop $(docker container ls -aq)
```

https://linuxize.com/post/how-to-remove-docker-images-containers-volumes-and-networks/


#### Docker in Docker (dind) -- check this later...

https://stackoverflow.com/questions/47280922/role-of-docker-in-docker-dind-service-in-gitlab-ci
https://qiita.com/sugiyasu-qr/items/85a1bedb6458d4573407
https://stackoverflow.com/questions/48630005/how-to-run-docker-compose-inside-docker-in-docker-witch-runs-inside-gitlab-runne
https://stackoverflow.com/questions/21871479/docker-cant-connect-to-docker-daemon
https://docs.docker.com/v17.09/engine/reference/commandline/dockerd/
https://gitlab.com/charts/gitlab/issues/478
https://openedx.atlassian.net/wiki/spaces/TE/pages/98370090/Using+Docker+within+Docker
https://itnext.io/docker-in-docker-521958d34efd
https://github.com/ClusterHQ/dvol/issues/67
https://gitlab.com/gitlab-com/support-forum/issues/950
https://hub.docker.com/r/gitlab/gitlab-runner/tags?page=14
https://stackoverflow.com/questions/39868369/run-docker-compose-build-in-gitlab-ci-yml
https://docs.gitlab.com/runner/install/docker.html
https://stackoverflow.com/questions/31721752/gitlab-ci-multi-runner-start-docker-container?rq=1
https://docs.gitlab.com/runner/install/docker.html

https://www.joshmcarthur.com/til/2018/04/02/running-gitlab-ci-tests-with-docker-compose.html

#### How to register a Docker CI Runner?

```
sudo gitlab-runner register \
  --url "https://gitlab.example.com/" \
  --registration-token "PROJECT_REGISTRATION_TOKEN" \
  --description "docker-ruby-2.1" \
  --executor "docker" \
  --docker-image ruby:2.1 \
  --docker-postgres latest \
  --docker-mysql latest
```

https://docs.gitlab.com/ee/ci/docker/using_docker_images.html


#### Maven and Docker

https://hub.docker.com/_/maven/?tab=description
https://docs.gitlab.com/ee/ci/examples/artifactory_and_gitlab/
https://labs.consol.de/development/2017/07/14/gitlab-ci.html
https://stackoverflow.com/questions/33430487/how-to-use-gitlab-ci-to-build-a-java-maven-project

#### Docker logs

https://docs.docker.com/engine/reference/commandline/logs/


#### How to copy a file from a container to the host machine?

```
% docker cp <containerId>:/file/path/within/container /host/path/target
```

https://stackoverflow.com/questions/22907231/copying-files-from-host-to-docker-container

#### How to copy all the files in a folder from a host to a container?

```
% docker cp /path/to/files/. container_name:/path/to/dist
```

#### The Docker executor
https://docs.gitlab.com/runner/executors/docker.html


#### Apache Proxy in Docker container

https://www.digitalocean.com/community/tutorials/how-to-use-apache-as-a-reverse-proxy-with-mod_proxy-on-ubuntu-16-04
https://hub.docker.com/r/diouxx/apache-proxy/dockerfile
https://github.com/DiouxX/docker-apache-proxy/blob/master/Dockerfile
https://stackoverflow.com/questions/26474476/minimal-configuration-for-apache-reverse-proxy-in-docker-container

#### How to update /etc/hosts file in Docker image during “docker build”?

```
extra_hosts:
 - "somehost:162.242.195.82"
 - "otherhost:50.31.209.229"
```
https://stackoverflow.com/questions/38302867/how-to-update-etc-hosts-file-in-docker-image-during-docker-build

#### Linking Tomcat container and Apache

```
services:
    depends_on:
      - tomcat
```
      
And use in apache2.conf like,

```
ProxyPass /hogehoge/ http://tomcat:8080/hogehoge/
ProxyPassReverse /hogehoge/ http://tomcat:8080/hogehoge/
```

#### Run multiple applications with Apache Docker

https://medium.com/@jmarhee/running-multiple-web-applications-on-a-docker-host-with-apache-85f673f02803


#### How to mount multiple NFS mount points?

`docker-compose.yml`

```
volumes:
  nfs_test:
    driver: local
    driver_opts:
      type: "nfs"
      o: "addr=nfs-ifs.hogehoge.edu,ro"
      device: ":/hogehoge/hoge1"
  nfs_test2:
    driver: local
    driver_opts:
      type: "nfs"
      o: "addr=nfs-ifs.hogehoge.edu,ro"
      device: ":/hogehoge/hoge2"
  db-data:

services:  
  httpd_proxy:
    container_name: httpd-container2
    build: ./Apache_proxy
    ports:
      - "80:80"
    volumes:
      - "nfs_test:/ifs/hoge1"
      - "nfs_test2:/ifs/hoge2"  
    depends_on:
      - tomcat
```

https://www.reddit.com/r/docker/comments/asubnn/nfs_volumes_no_route_to_host/

---
#### Docker cheatsheet

Remove volumes:
```
docker system prune --volumes
```

Remove containers:
```
docker system prune -a
```

Shutting down composed Docker containers are
```
docker-compose down -v
```
or
```
docker-compose down
docker volume prune
```

```
docker-compose ps
docker-compose rm
```

https://linuxize.com/post/how-to-remove-docker-images-containers-volumes-and-networks/

---
#### Issues on Windows 10 Home and Docker

How to install?
https://forums.docker.com/t/installing-docker-on-windows-10-home/11722/2

How to use “localhost” instead of “192.168.99.100”?
https://stackoverflow.com/questions/42866013/docker-toolbox-localhost-not-working
https://forums.docker.com/t/how-to-use-localhost-instead-of-192-168-99-100/54098
https://www.jhipster.tech/tips/020_tip_using_docker_containers_as_localhost_on_mac_and_windows.html


#### Docker in Windows10 and issues with loading config files for MySQL due to 777 files permissions granted by VirtuablBox.

Dockerfile
```
FROM mysql:5.7

RUN touch /var/log/mysql/mysqld.log

# This is a workaround for Windows10
# Config files won't load if you use Windows10/VirtualBox/Docker Toolbox due to 777 permissions
ADD ./conf.d/my.cnf /etc/mysql/conf.d/my.cnf
ADD ./conf.d/disable_strict_mode.cnf /etc/mysql/conf.d/disable_strict_mode.cnf
RUN chmod 644 /etc/mysql/conf.d/my.cnf
RUN chmod 644 /etc/mysql/conf.d/disable_strict_mode.cnf
```

And don't use `Volume:` from `docker-compose.yml`

https://qiita.com/koyo-miyamura/items/4d1430b9086c5d4a58a5


#### How to avoid failing npm run build in Docker?

Set `NODE_ENV` after `npm install`.

```
RUN npm install

ENV NODE_ENV=production
RUN npm run build
```

http://packpak.hatenablog.com/entry/2018/09/16/100052

#### How to write a Dockerfile with SSL enabled Tomcat8.5?

`Dockerfile`

```
FROM tomcat:8.5

RUN mkdir "$CATALINA_HOME/keystore"

RUN keytool  -genkey -noprompt -trustcacerts -keyalg RSA -alias tomcat -dname  "CN=Unknown, OU=Unknown, O=Unknown, L=Unknown, ST=Unknown, C=Unknown" -keypass changeit -keystore "$CATALINA_HOME/keystore/.keystore" -storepass changeit

COPY /config/server.xml "$CATALINA_HOME/conf/server.xml"
COPY /config/tomcat-users.xml "$CATALINA_HOME/conf/tomcat-users.xml"
COPY /config/manager.xml "$CATALINA_HOME/conf/Catalina/localhost/manager.xml"
COPY /config/host-manager.xml "$CATALINA_HOME/conf/Catalina/localhost/host-manager.xml"


EXPOSE 8443
```
http://palashray.com/tomcat-8-ssl-configuration-with-self-signed-certificate/
https://github.com/paawak/blog/blob/master/code/apache-http-client/src/main/docker/Dockerfile

#### How to enable Tomcat8.5's manager page?

`manager.xml`

````
<Context privileged="true" antiResourceLocking="false" docBase="${catalina.home}/webapps/manager">
    <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
</Context>
````

`host-manager.xml`

````
<Context privileged="true" antiResourceLocking="false" docBase="${catalina.home}/webapps/host-manager">
    <Valve className="org.apache.catalina.valves.RemoteAddrValve" allow="^.*$" />
</Context>
````

`tomcat-users.xml`

````
<?xml version='1.0' encoding='utf-8'?>

<tomcat-users>
  <role rolename="tomcat"/>
  <role rolename="role1"/>
  <role rolename="admin"/>
  <role rolename="manager-script"/>
  <role rolename="manager-gui"/>
  <role rolename="manager-jmx"/>
  <role rolename="manager-status"/>    
  <user username="tomcat" password="tomcat" roles="tomcat"/>
  <user username="both" password="tomcat" roles="tomcat,role1"/>
  <user username="role1" password="tomcat" roles="role1"/>
  <user username="admin" password="pass" roles="admin,manager,manager-script,manager-gui,manager-jmx,manager-status"/>
</tomcat-users>
````

https://serverfault.com/questions/803899/unable-to-access-tomcat-8-host-manager-i-can-access-manager-app-just-fine

#### How to rebuild an image and start one service from docker-compose?

```
$docker-compose up -d --no-deps --build <service_name>
--no-deps - Don't start linked services.

--build - Build images before starting containers.
```
https://stackoverflow.com/questions/36884991/how-to-rebuild-docker-container-in-docker-compose-yml

#### How to stop/remove docker containers at once?

```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

#### How to install vim on Alpine Docker?

```
RUN apt-get update && apt-get install vim -y &&
 apt-get install nmap -y
```
https://forums.docker.com/t/install-vim-in-docker-container-on-creation/60296

#### How to fix "max depth error" error?

Clean up docker images and volumes

https://blog.websandbag.com/entry/2018/05/15/235514
