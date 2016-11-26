# java - spring

##### Build a VM and connect
* https://github.com/bachmeb/spring-gs/blob/master/docs/aws-vm.md

##### Install Java Open JDK 1.8
* https://github.com/bachmeb/spring-gs/blob/master/docs/jdk-1.8-install.md

##### Install Gradle
* https://github.com/bachmeb/spring-gs/blob/master/docs/gradle-install.md

##### Create a project directory
```
mkdir -p ~/git/rest-api-spring/project
cd ~/git/rest-api-spring/project
```

##### Create the directory structure
```
mkdir -p src/main/java/hello
```

##### Create the HelloWorld class
```
vim src/main/java/hello/HelloWorld.java
```
```java
package hello;

public class HelloWorld {
  public static void main(String[] args) {
    Greeter greeter = new Greeter();
    System.out.println(greeter.sayHello());
  }
}
```

##### Create the Greeter class
```
vim src/main/java/hello/Greeter.java
```
```
package hello;

public class Greeter {
  public String sayHello() {
    return "Hello world!";
  }
}
```
##### See the Gradle tasks that are available
```
gradle tasks
```
```

:tasks

------------------------------------------------------------
All tasks runnable from root project
------------------------------------------------------------

Build Setup tasks
-----------------
init - Initializes a new Gradle build. [incubating]
wrapper - Generates Gradle wrapper files. [incubating]

Help tasks
----------
buildEnvironment - Displays all buildscript dependencies declared in root project 'gs-gradle'.
components - Displays the components produced by root project 'gs-gradle'. [incubating]
dependencies - Displays all dependencies declared in root project 'gs-gradle'.
dependencyInsight - Displays the insight into a specific dependency in root project 'gs-gradle'.
help - Displays a help message.
model - Displays the configuration model of root project 'gs-gradle'. [incubating]
projects - Displays the sub-projects of root project 'gs-gradle'.
properties - Displays the properties of root project 'gs-gradle'.
tasks - Displays the tasks runnable from root project 'gs-gradle'.

To see all tasks and more detail, run gradle tasks --all

To see more detail about a task, run gradle help --task <task>

BUILD SUCCESSFUL

Total time: 2.428 secs
```

##### Create a build.gradle file
```
vim build.gradle
```
```
apply plugin: 'java'
```
##### Run the build task
```
gradle build
```
```

:compileJava
:processResources UP-TO-DATE
:classes
:jar
:assemble
:compileTestJava UP-TO-DATE
:processTestResources UP-TO-DATE
:testClasses UP-TO-DATE
:test UP-TO-DATE
:check UP-TO-DATE
:build

BUILD SUCCESSFUL

Total time: 5.608 secs
```

##### Initialize the wrapper scripts
```
gradle wrapper
```
```
:wrapper

BUILD SUCCESSFUL

Total time: 5.173 secs
```

##### Edit build.gradle
```
vim build.gradle
```
* Add gradle's application plugin to make the code runnable
```
apply plugin: 'java'
apply plugin: 'application'

mainClassName = 'hello.HelloWorld'
```

##### Run the wrapper script to perform the build task
```
./gradlew build
```

##### Run the app
```
./gradlew run
```
```
:compileJava UP-TO-DATE
:processResources UP-TO-DATE
:classes UP-TO-DATE
:run
Hello World!

BUILD SUCCESSFUL

Total time: 5.428 secs
```
##### Edit the build file
```
nano build.gradle
```
```java
apply plugin: 'java'
apply plugin: 'application'
apply plugin: 'eclipse'
apply plugin: 'idea'
apply plugin: 'spring-boot'

mainClassName = 'hello.HelloWorld'

buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.3.2.RELEASE")
    }
}

jar {
    baseName = 'gs-rest-service'
    version =  '0.1.0'
}

repositories {
    mavenCentral()
}

sourceCompatibility = 1.8
targetCompatibility = 1.8

dependencies {
    compile("org.springframework.boot:spring-boot-starter-web")
    testCompile("junit:junit")
}

task wrapper(type: Wrapper) {
    gradleVersion = '2.10'
}
```
##### Build the project
```
./gradlew build
``` 
```c
/*
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-gradle-plugin/1.3.2.RELEASE/spring-boot-gradle-plugin-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-tools/1.3.2.RELEASE/spring-boot-tools-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-parent/1.3.2.RELEASE/spring-boot-parent-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-dependencies/1.3.2.RELEASE/spring-boot-dependencies-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/spring-framework-bom/4.2.4.RELEASE/spring-framework-bom-4.2.4.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/data/spring-data-releasetrain/Gosling-SR2A/spring-data-releasetrain-Gosling-SR2A.pom
Download https://repo1.maven.org/maven2/org/springframework/data/build/spring-data-build/1.7.3.RELEASE/spring-data-build-1.7.3.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/integration/spring-integration-bom/4.2.4.RELEASE/spring-integration-bom-4.2.4.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/security/spring-security-bom/4.0.3.RELEASE/spring-security-bom-4.0.3.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-loader-tools/1.3.2.RELEASE/spring-boot-loader-tools-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/io/spring/gradle/dependency-management-plugin/0.5.4.RELEASE/dependency-management-plugin-0.5.4.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/spring-core/4.2.4.RELEASE/spring-core-4.2.4.RELEASE.pom
Download https://repo1.maven.org/maven2/commons-logging/commons-logging/1.2/commons-logging-1.2.pom
Download https://repo1.maven.org/maven2/org/apache/commons/commons-parent/34/commons-parent-34.pom
Download https://repo1.maven.org/maven2/org/apache/apache/13/apache-13.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-gradle-plugin/1.3.2.RELEASE/spring-boot-gradle-plugin-1.3.2.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-loader-tools/1.3.2.RELEASE/spring-boot-loader-tools-1.3.2.RELEASE.jar
Download https://repo1.maven.org/maven2/io/spring/gradle/dependency-management-plugin/0.5.4.RELEASE/dependency-management-plugin-0.5.4.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/spring-core/4.2.4.RELEASE/spring-core-4.2.4.RELEASE.jar
Download https://repo1.maven.org/maven2/commons-logging/commons-logging/1.2/commons-logging-1.2.jar
:compileJava
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter-parent/1.3.2.RELEASE/spring-boot-starter-parent-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter-web/1.3.2.RELEASE/spring-boot-starter-web-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starters/1.3.2.RELEASE/spring-boot-starters-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter/1.3.2.RELEASE/spring-boot-starter-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter-tomcat/1.3.2.RELEASE/spring-boot-starter-tomcat-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter-validation/1.3.2.RELEASE/spring-boot-starter-validation-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-databind/2.6.5/jackson-databind-2.6.5.pom
Download https://repo1.maven.org/maven2/com/fasterxml/jackson/jackson-parent/2.6.2/jackson-parent-2.6.2.pom
Download https://repo1.maven.org/maven2/com/fasterxml/oss-parent/24/oss-parent-24.pom
Download https://repo1.maven.org/maven2/org/springframework/spring-web/4.2.4.RELEASE/spring-web-4.2.4.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/spring-webmvc/4.2.4.RELEASE/spring-webmvc-4.2.4.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot/1.3.2.RELEASE/spring-boot-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-autoconfigure/1.3.2.RELEASE/spring-boot-autoconfigure-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter-logging/1.3.2.RELEASE/spring-boot-starter-logging-1.3.2.RELEASE.pom
Download https://repo1.maven.org/maven2/org/yaml/snakeyaml/1.16/snakeyaml-1.16.pom
Download https://repo1.maven.org/maven2/org/apache/tomcat/embed/tomcat-embed-core/8.0.30/tomcat-embed-core-8.0.30.pom
Download https://repo1.maven.org/maven2/org/apache/tomcat/embed/tomcat-embed-el/8.0.30/tomcat-embed-el-8.0.30.pom
Download https://repo1.maven.org/maven2/org/apache/tomcat/embed/tomcat-embed-logging-juli/8.0.30/tomcat-embed-logging-juli-8.0.30.pom
Download https://repo1.maven.org/maven2/org/apache/tomcat/embed/tomcat-embed-websocket/8.0.30/tomcat-embed-websocket-8.0.30.pom
Download https://repo1.maven.org/maven2/org/hibernate/hibernate-validator/5.2.2.Final/hibernate-validator-5.2.2.Final.pom
Download https://repo1.maven.org/maven2/org/hibernate/hibernate-validator-parent/5.2.2.Final/hibernate-validator-parent-5.2.2.Final.pom
Download https://repo1.maven.org/maven2/org/jboss/arquillian/arquillian-bom/1.1.9.Final/arquillian-bom-1.1.9.Final.pom
Download https://repo1.maven.org/maven2/org/jboss/shrinkwrap/shrinkwrap-bom/1.2.2/shrinkwrap-bom-1.2.2.pom
Download https://repo1.maven.org/maven2/org/jboss/shrinkwrap/resolver/shrinkwrap-resolver-bom/2.1.1/shrinkwrap-resolver-bom-2.1.1.pom
Download https://repo1.maven.org/maven2/org/jboss/shrinkwrap/descriptors/shrinkwrap-descriptors-bom/2.0.0-alpha-7/shrinkwrap-descriptors-bom-2.0.0-alpha-7.pom
Download https://repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-annotations/2.6.5/jackson-annotations-2.6.5.pom
Download https://repo1.maven.org/maven2/com/fasterxml/jackson/jackson-parent/2.6.1/jackson-parent-2.6.1.pom
Download https://repo1.maven.org/maven2/com/fasterxml/oss-parent/23/oss-parent-23.pom
Download https://repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-core/2.6.5/jackson-core-2.6.5.pom
Download https://repo1.maven.org/maven2/org/springframework/spring-aop/4.2.4.RELEASE/spring-aop-4.2.4.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/spring-beans/4.2.4.RELEASE/spring-beans-4.2.4.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/spring-context/4.2.4.RELEASE/spring-context-4.2.4.RELEASE.pom
Download https://repo1.maven.org/maven2/org/springframework/spring-expression/4.2.4.RELEASE/spring-expression-4.2.4.RELEASE.pom
Download https://repo1.maven.org/maven2/ch/qos/logback/logback-classic/1.1.3/logback-classic-1.1.3.pom
Download https://repo1.maven.org/maven2/ch/qos/logback/logback-parent/1.1.3/logback-parent-1.1.3.pom
Download https://repo1.maven.org/maven2/org/slf4j/jcl-over-slf4j/1.7.13/jcl-over-slf4j-1.7.13.pom
Download https://repo1.maven.org/maven2/org/slf4j/slf4j-parent/1.7.13/slf4j-parent-1.7.13.pom
Download https://repo1.maven.org/maven2/org/slf4j/jul-to-slf4j/1.7.13/jul-to-slf4j-1.7.13.pom
Download https://repo1.maven.org/maven2/org/slf4j/log4j-over-slf4j/1.7.13/log4j-over-slf4j-1.7.13.pom
Download https://repo1.maven.org/maven2/javax/validation/validation-api/1.1.0.Final/validation-api-1.1.0.Final.pom
Download https://repo1.maven.org/maven2/org/jboss/logging/jboss-logging/3.3.0.Final/jboss-logging-3.3.0.Final.pom
Download https://repo1.maven.org/maven2/org/jboss/jboss-parent/15/jboss-parent-15.pom
Download https://repo1.maven.org/maven2/com/fasterxml/classmate/1.1.0/classmate-1.1.0.pom
Download https://repo1.maven.org/maven2/org/sonatype/oss/oss-parent/7/oss-parent-7.pom
Download https://repo1.maven.org/maven2/aopalliance/aopalliance/1.0/aopalliance-1.0.pom
Download https://repo1.maven.org/maven2/ch/qos/logback/logback-core/1.1.3/logback-core-1.1.3.pom
Download https://repo1.maven.org/maven2/org/slf4j/slf4j-api/1.7.13/slf4j-api-1.7.13.pom
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter-web/1.3.2.RELEASE/spring-boot-starter-web-1.3.2.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter/1.3.2.RELEASE/spring-boot-starter-1.3.2.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter-tomcat/1.3.2.RELEASE/spring-boot-starter-tomcat-1.3.2.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter-validation/1.3.2.RELEASE/spring-boot-starter-validation-1.3.2.RELEASE.jar
Download https://repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-databind/2.6.5/jackson-databind-2.6.5.jar
Download https://repo1.maven.org/maven2/org/springframework/spring-web/4.2.4.RELEASE/spring-web-4.2.4.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/spring-webmvc/4.2.4.RELEASE/spring-webmvc-4.2.4.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot/1.3.2.RELEASE/spring-boot-1.3.2.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-autoconfigure/1.3.2.RELEASE/spring-boot-autoconfigure-1.3.2.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/boot/spring-boot-starter-logging/1.3.2.RELEASE/spring-boot-starter-logging-1.3.2.RELEASE.jar
Download https://repo1.maven.org/maven2/org/yaml/snakeyaml/1.16/snakeyaml-1.16.jar
Download https://repo1.maven.org/maven2/org/apache/tomcat/embed/tomcat-embed-core/8.0.30/tomcat-embed-core-8.0.30.jar
Download https://repo1.maven.org/maven2/org/apache/tomcat/embed/tomcat-embed-el/8.0.30/tomcat-embed-el-8.0.30.jar
Download https://repo1.maven.org/maven2/org/apache/tomcat/embed/tomcat-embed-logging-juli/8.0.30/tomcat-embed-logging-juli-8.0.30.jar
Download https://repo1.maven.org/maven2/org/apache/tomcat/embed/tomcat-embed-websocket/8.0.30/tomcat-embed-websocket-8.0.30.jar
Download https://repo1.maven.org/maven2/org/hibernate/hibernate-validator/5.2.2.Final/hibernate-validator-5.2.2.Final.jar
Download https://repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-annotations/2.6.5/jackson-annotations-2.6.5.jar
Download https://repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-core/2.6.5/jackson-core-2.6.5.jar
Download https://repo1.maven.org/maven2/org/springframework/spring-aop/4.2.4.RELEASE/spring-aop-4.2.4.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/spring-beans/4.2.4.RELEASE/spring-beans-4.2.4.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/spring-context/4.2.4.RELEASE/spring-context-4.2.4.RELEASE.jar
Download https://repo1.maven.org/maven2/org/springframework/spring-expression/4.2.4.RELEASE/spring-expression-4.2.4.RELEASE.jar
Download https://repo1.maven.org/maven2/ch/qos/logback/logback-classic/1.1.3/logback-classic-1.1.3.jar
Download https://repo1.maven.org/maven2/org/slf4j/jcl-over-slf4j/1.7.13/jcl-over-slf4j-1.7.13.jar
Download https://repo1.maven.org/maven2/org/slf4j/jul-to-slf4j/1.7.13/jul-to-slf4j-1.7.13.jar
Download https://repo1.maven.org/maven2/org/slf4j/log4j-over-slf4j/1.7.13/log4j-over-slf4j-1.7.13.jar
Download https://repo1.maven.org/maven2/javax/validation/validation-api/1.1.0.Final/validation-api-1.1.0.Final.jar
Download https://repo1.maven.org/maven2/org/jboss/logging/jboss-logging/3.3.0.Final/jboss-logging-3.3.0.Final.jar
Download https://repo1.maven.org/maven2/com/fasterxml/classmate/1.1.0/classmate-1.1.0.jar
Download https://repo1.maven.org/maven2/aopalliance/aopalliance/1.0/aopalliance-1.0.jar
Download https://repo1.maven.org/maven2/ch/qos/logback/logback-core/1.1.3/logback-core-1.1.3.jar
Download https://repo1.maven.org/maven2/org/slf4j/slf4j-api/1.7.13/slf4j-api-1.7.13.jar
:processResources UP-TO-DATE
:classes
:jar
:findMainClass
:startScripts
:distTar
:distZip
:bootRepackage
:assemble
:compileTestJava UP-TO-DATE
:processTestResources UP-TO-DATE
:testClasses UP-TO-DATE
:test UP-TO-DATE
:check UP-TO-DATE
:build

BUILD SUCCESSFUL

Total time: 19.132 secs

This build could be faster, please consider using the Gradle Daemon: https://docs.gradle.org/2.10/userguide/gradle_daemon.html
*/
```

##### List the contents of the build/libs directory
```
ll build/libs/
```
```c
/*
total 13092
-rw-rw-r-- 1 bachmeb bachmeb 13394696 Nov 26 17:49 gs-rest-service-0.1.0.jar
-rw-rw-r-- 1 bachmeb bachmeb     1221 Nov 26 17:49 gs-rest-service-0.1.0.jar.original
-rw-rw-r-- 1 bachmeb bachmeb     1221 Nov 26 17:30 project.jar
*/
```
##### Run the project
```
./gradlew run
```
