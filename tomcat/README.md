#### Tomcat stuffs

####  How to handle PermGen space error?

```
Exception in thread "C3P0PooledConnectionPoolManager[identityToken->z8kfsxa51yrcnyha9bsan|4b34845c]-AdminTaskTimer" java.lang.OutOfMemoryError: PermGen space
Exception in thread "C3P0PooledConnectionPoolManager[identityToken->z8kfsxa51w6357dvsb03z|5803f6fa]-HelperThread-#0" java.lang.OutOfMemoryError: PermGen space
```

/etc/tomcat6/default

```
# Use a CMS garbage collector for improved response time
#JAVA_OPTS="${JAVA_OPTS} -XX:+UseConcMarkSweepGC"
#JAVA_OPTS="${JAVA_OPTS} -XX:+UseConcMarkSweepGC -Djava.net.preferIPv4Stack=true -Xmx1024m"
#JAVA_OPTS="${JAVA_OPTS} -XX:+UseConcMarkSweepGC -Djava.net.preferIPv4Stack=true -Xmx1024m -XX:PermSize=128m -XX:MaxPermSize=512m"
JAVA_OPTS="${JAVA_OPTS} -XX:+UseConcMarkSweepGC -Djava.net.preferIPv4Stack=true -Xmx1024m -XX:PermSize=512m -XX:MaxPermSize=1024m -XX:+CMSClassUnloadingEnabled -XX:+CMSPermGenSweepingEnabled"
```
#### How to configure Tomcat7 or 8 to use manager app?

`tomcat-users.xml`

```
<?xml version='1.0' encoding='utf-8'?>

<tomcat-users>
  <role rolename="tomcat"/>
  <role rolename="role1"/>
  <role rolename="admin"/>
  <role rolename="manager-script"/>
  <role rolename="manager-gui"/>
  <user username="tomcat" password="tomcat" roles="tomcat"/>
  <user username="both" password="tomcat" roles="tomcat,role1"/>
  <user username="role1" password="tomcat" roles="role1"/>
  <user username="admin" password="pass" roles="admin,manager,manager-script,manager-gui"/>
</tomcat-users>
```

`pom.xml`

```
<plugin>
    <groupId>org.apache.tomcat.maven</groupId>
    <artifactId>tomcat7-maven-plugin</artifactId>
    <version>2.2</version>
    <configuration>
        <url>http://your-server:8080/manager/text</url>
        <username>a-username</username>
        <password>a-password</password>
        <path>/a-path</path>
    </configuration>
</plugin>
```


https://stackoverflow.com/questions/14427351/cant-do-mvn-tomcatdeploy-because-of-http-response-405

#### How to configure Tomcat8 to use manager app?

Comment this valve in `/usr/local/tomcat/conf/context.xml`.

```
<?xml version="1.0" encoding="UTF-8"?>
<!--
  Licensed to the Apache Software Foundation (ASF) under one or more
  contributor license agreements.  See the NOTICE file distributed with
  this work for additional information regarding copyright ownership.
  The ASF licenses this file to You under the Apache License, Version 2.0
  (the "License"); you may not use this file except in compliance with
  the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

  Unless required by applicable law or agreed to in writing, software
  distributed under the License is distributed on an "AS IS" BASIS,
  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
  See the License for the specific language governing permissions and
  limitations under the License.
-->
<Context antiResourceLocking="false" privileged="true" >
<!--
  <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" />
-->				 
  <Manager sessionAttributeValueClassNameFilter="java\.lang\.(?:Boolean|Integer|Long|Number|String)|org\.apache\.catalina\.filters\.CsrfPreventionFilter\$LruCache(?:\$1)?|java\.util\.(?:Linked)?HashMap"/>
</Context>
```

#### How to fix a Dockerfile where Tomcat Docker is failing to get gpg_keys from the default keyserver?

Replace a line to use a different keyserver location.

```
		gpg --batch --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys "$key"; \
```


