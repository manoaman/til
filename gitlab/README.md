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


#### How to explicitly set JAVA_HOME in .gitlab-ci.yml?

```
before_script:
  - export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"
  - export PATH=$JAVA_HOME/bin:$M2_HOME/bin:/usr/local/bin:$PATH
```

#### How to upgrade the limit of logging?

Modify config.toml to set 10MB. (Values is in kb.)
```
[[runners]]
  output_limit = 10000
```
https://docs.gitlab.com/runner/configuration/advanced-configuration.html#the-runners-section


#### What are the acronyms in config.toml?

https://docs.gitlab.com/runner/configuration/advanced-configuration.html

#### What are the acronyms in .gitlab-ci.yml?

https://docs.gitlab.com/ee/ci/yaml/#only-and-except-simplified

#### How do I execute .gitlab-ci.yml jobs from a shell?

```
% cd /home/gitlab-runner/builds/cde0fc25/0/syamashi/mcpbigmap
% gitlab-ci-multi-runner exec shell test
```

https://gitlab.com/gitlab-org/gitlab-runner/issues/312


#### How to keep the built artifacts in GitLab and share with other jobs?

Use `artifacts` and `dependencies`.

https://stackoverflow.com/questions/42948062/stop-gitlab-runner-to-not-remove-a-directory
https://docs.gitlab.com/ce/ci/yaml/README.html#artifacts
https://docs.gitlab.com/ce/ci/yaml/README.html#dependencies

#### How to specify the wildcard artifact directories and files?

```
   artifacts:
     paths:
      - "./Dinoskin/target/*"
      - "./.m2/repository/*"
```
https://stackoverflow.com/questions/38009869/how-to-specify-wildcard-artifacts-subdirectories-in-gitlab-ci-yml


#### How to setup for Maven deployment to the server?

Since you want to use GitLab Runner to automatically deploy the application, you should create the file in the project’s home directory and set a command line parameter in .gitlab-ci.yml to use the custom location instead of the default one:

1. Create a folder called .m2 in the root of your repository
2. Create a file called settings.xml in the .m2 folder
3. Copy the following content into a settings.xml file:

```
 <settings xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.1.0 http://maven.apache.org/xsd/settings-1.1.0.xsd"
     xmlns="http://maven.apache.org/SETTINGS/1.1.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
   <servers>
     <server>
       <id>central</id>
       <username>${env.MAVEN_REPO_USER}</username>
       <password>${env.MAVEN_REPO_PASS}</password>
     </server>
   </servers>
 </settings>
```
https://docs.gitlab.com/ee/ci/examples/artifactory_and_gitlab/
