### Maven

### Maven Reports

Add the reporting plugin and just show the failed tests.

```
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-report-plugin</artifactId>
                <version>3.0.0-M3</version>
            </plugin>

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>3.0.0-M3</version>
            </plugin>

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-site-plugin</artifactId>
                <version>3.7.1</version>
            </plugin>
```

Run the `test` to generated individual test reports under `/target/surefire-reports/` in both `.xml` and `.txt` files.
```
mvn clean test
```

Run the `surefire-report:report-only` to generate a report under `/target/site/surefire-report.html`.  However, this alone won't generate images and stying is not applied.
```
mvn surefire-report:report-only
```

Run the `site` to generate `images` and `css` for the reports.
```
mvn site -DgenerateReports=false
```

Note: Running above three Maven goals does not seem to generate `target/site` folder.  Not sure why...

Consolidated reports will be generated in, `target/site/surefire-report.html`.

https://stackoverflow.com/questions/2846493/is-there-a-decent-html-junit-report-plugin-for-maven/23958874#23958874

https://qiita.com/unhurried/items/b10d4597d62dea1b3a94

https://maven.apache.org/plugins/maven-site-plugin/index.html

https://maven.apache.org/surefire/maven-surefire-plugin/index.html

https://maven.apache.org/surefire/maven-surefire-report-plugin/index.html


### How to change default maven surefire plugin to higher version?

Use `pluginManagement`.

```
<build>
  <pluginManagement>
   <plugins>
     <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-surefire-plugin</artifactId>
       <version>{version}</version>
     </plugin>
     ...
   </plugins>
 </pluginManagement>
</build>
```


### POM.xml structure

```
<project xmlns="http://maven.apache.org/POM/4.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                      http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
 
  <!-- The Basics -->
  <groupId>...</groupId>
  <artifactId>...</artifactId>
  <version>...</version>
  <packaging>...</packaging>
  <dependencies>...</dependencies>
  <parent>...</parent>
  <dependencyManagement>...</dependencyManagement>
  <modules>...</modules>
  <properties>...</properties>
 
  <!-- Build Settings -->
  <build>...</build>
  <reporting>...</reporting>
 
  <!-- More Project Information -->
  <name>...</name>
  <description>...</description>
  <url>...</url>
  <inceptionYear>...</inceptionYear>
  <licenses>...</licenses>
  <organization>...</organization>
  <developers>...</developers>
  <contributors>...</contributors>
 
  <!-- Environment Settings -->
  <issueManagement>...</issueManagement>
  <ciManagement>...</ciManagement>
  <mailingLists>...</mailingLists>
  <scm>...</scm>
  <prerequisites>...</prerequisites>
  <repositories>...</repositories>
  <pluginRepositories>...</pluginRepositories>
  <distributionManagement>...</distributionManagement>
  <profiles>...</profiles>
</project>
```

https://maven.apache.org/pom.html

### How to run Maven in a non-intractive way?

```
mvn --batch-mode ...
```
https://maven.apache.org/maven-release/maven-release-plugin/examples/non-interactive-release.html

### How to test an individual file?

```
mvn test -Dtest=SomeTests
```
https://stackoverflow.com/questions/1873995/run-a-single-test-method-with-maven
