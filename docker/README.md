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
docker cp <containerId>:/file/path/within/container /host/path/target
```

#### The Docker executor
https://docs.gitlab.com/runner/executors/docker.html