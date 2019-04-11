### GitLab

#### Get started

Clone the repo into your local machine,
```
% git clone PASTE HTTPS OR SSH HERE
(% git git@hostname.come:username/reponame.git)
```
https://docs.gitlab.com/ee/gitlab-basics/command-line-commands.html

---

#### Manual install of the gitlab-ci-multi-runner

Download deb file,
```
wget https://gitlab-ci-multi-runner-downloads.s3.amazonaws.com/v1.11.1/deb/gitlab-ci-multi-runner_i386.deb
```

and then install,
```
sudo dpkg -i /path/to/deb/file followed by sudo apt-get install -f.
```

https://gitlab-ci-multi-runner-downloads.s3.amazonaws.com/v1.11.1/index.html
https://unix.stackexchange.com/questions/159094/how-to-install-a-deb-file-by-dpkg-i-or-by-apt

#### Register gitlab-ci-multi-runner


Configuration file will be placed in `/etc/gitlab-runner/config.toml`.

```
concurrent = 1
check_interval = 0

[[runners]]
  name = "hogehoge-gitlab-ci-multi-runner"
  url = "https://git.host.com/ci"
  token = "xxxxxxxxx"
  executor = "shell"
  [runners.cache]
```

#### How to start/stop gitlab-ci-multi-runner process

```
% sudo gitlab-ci-multi-runner start &
```

```
% sudo killall -SIGHUP gitlab-ci-multi-runner
```

https://docs.gitlab.com/runner/commands/


#### Executors

https://docs.gitlab.com/runner/executors/README.html#i-am-not-sure


#### How to register gitlab-ci-multi-runner

https://docs.gitlab.com/runner/register/index.html
