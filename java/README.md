### Java


#### How to figure out where the Java is installed?

```
% /usr/libexec/java_home -v 1.8
```

#### How to install OpenJDK

```
% sudo add-apt-repository ppa:openjdk-r/ppa  
% sudo apt-get update   
% sudo apt-get install openjdk-8-jdk 
```

#### Check alternative JDKs

```
% update-alternatives --list java
```

#### How to check certificate name and alias in keystore files?

````
% keytool -v -list -keystore .keystore
````

https://stackoverflow.com/questions/12893995/how-to-check-certificate-name-and-alias-in-keystore-files
