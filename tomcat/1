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
