# java - spring

### Build a VM and connect
* https://github.com/bachmeb/spring-gs/blob/master/docs/aws-vm.md

### Install Java Open JDK 1.8
* https://github.com/bachmeb/spring-gs/blob/master/docs/jdk-1.8-install.md

### Install Gradle
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

##### Run the wrapper script to perform the build task
```
./gradlew build
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
