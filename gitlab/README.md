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
