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

#### How to stop all the containers

```
% docker container stop $(docker container ls -aq)
```

https://linuxize.com/post/how-to-remove-docker-images-containers-volumes-and-networks/

