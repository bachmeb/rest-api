# java - spring

##### Build a VM and connect
* https://github.com/bachmeb/spring-gs/blob/master/docs/aws-vm.md

##### Install Java Open JDK 1.8
* https://github.com/bachmeb/spring-gs/blob/master/docs/jdk-1.8-install.md

##### Install Gradle
* https://github.com/bachmeb/spring-gs/blob/master/docs/gradle-install.md

##### Create a project directory
```
mkdir -p ~/git/rest-api-spring/project1
cd ~/git/rest-api-spring/project1
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

Total time: 6.031 secs

This build could be faster, please consider using the Gradle Daemon: https://docs.gradle.org/2.10/userguide/gradle_daemon.html
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
```c
/*
:compileJava UP-TO-DATE
:processResources UP-TO-DATE
:classes UP-TO-DATE
:jar UP-TO-DATE
:startScripts
:distTar
:distZip
:assemble
:compileTestJava UP-TO-DATE
:processTestResources UP-TO-DATE
:testClasses UP-TO-DATE
:test UP-TO-DATE
:check UP-TO-DATE
:build

BUILD SUCCESSFUL

Total time: 6.372 secs

This build could be faster, please consider using the Gradle Daemon: https://docs.gradle.org/2.10/userguide/gradle_daemon.html
*/
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
##### Make a new project directory
```
mkdir -p ~/git/rest-api-spring/project2
cd ~/git/rest-api-spring/project2
pwd
```
##### Make a source directory
```
mkdir -p  src/main/java/hello
```

##### Create a resource representation class
```
vim src/main/java/hello/Greeting.java
```
```java
package hello;

public class Greeting {

    private final long id;
    private final String content;

    public Greeting(long id, String content) {
        this.id = id;
        this.content = content;
    }

    public long getId() {
        return id;
    }

    public String getContent() {
        return content;
    }
}
```

##### Create a resource controller
```
nano src/main/java/hello/GreetingController.java
```
```java
package hello;

import java.util.concurrent.atomic.AtomicLong;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class GreetingController {

    private static final String template = "Hello, %s!";
    private final AtomicLong counter = new AtomicLong();

    @RequestMapping("/greeting")
    public Greeting greeting(@RequestParam(value="name", defaultValue="World") String name) {
        return new Greeting(counter.incrementAndGet(),
                            String.format(template, name));
    }
}
```
##### Make the application executable
```
nano src/main/java/hello/Application.java
```
```java
package hello;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

##### Make a build file
```
nano build.gradle
```
```java
buildscript {
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.3.2.RELEASE")
    }
}

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'idea'
apply plugin: 'spring-boot'

jar {
    baseName = 'rest-api-spring'
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
##### Get a list of Gradle tasks
```
gradle tasks
```
```c
/*
:tasks

------------------------------------------------------------
All tasks runnable from root project
------------------------------------------------------------

Application tasks
-----------------
bootRun - Run the project with support for auto-detecting main class and reloading static resources

Build tasks
-----------
assemble - Assembles the outputs of this project.
bootRepackage - Repackage existing JAR and WAR archives so that they can be executed from the command line using 'java -jar'
build - Assembles and tests this project.
buildDependents - Assembles and tests this project and all projects that depend on it.
buildNeeded - Assembles and tests this project and all projects it depends on.
classes - Assembles main classes.
clean - Deletes the build directory.
jar - Assembles a jar archive containing the main classes.
testClasses - Assembles test classes.

Build Setup tasks
-----------------
init - Initializes a new Gradle build. [incubating]

Documentation tasks
-------------------
javadoc - Generates Javadoc API documentation for the main source code.

Help tasks
----------
buildEnvironment - Displays all buildscript dependencies declared in root project 'project2'.
components - Displays the components produced by root project 'project2'. [incubating]
dependencies - Displays all dependencies declared in root project 'project2'.
dependencyInsight - Displays the insight into a specific dependency in root project 'project2'.
help - Displays a help message.
model - Displays the configuration model of root project 'project2'. [incubating]
projects - Displays the sub-projects of root project 'project2'.
properties - Displays the properties of root project 'project2'.
tasks - Displays the tasks runnable from root project 'project2'.

IDE tasks
---------
cleanEclipse - Cleans all Eclipse files.
cleanIdea - Cleans IDEA project files (IML, IPR)
eclipse - Generates all Eclipse files.
idea - Generates IDEA project files (IML, IPR, IWS)

Verification tasks
------------------
check - Runs all checks.
test - Runs the unit tests.

Other tasks
-----------
cleanIdeaWorkspace
dependencyManagement
wrapper

Rules
-----
Pattern: clean<TaskName>: Cleans the output files of a task.
Pattern: build<ConfigurationName>: Assembles the artifacts of a configuration.
Pattern: upload<ConfigurationName>: Assembles and uploads the artifacts belonging to a configuration.

To see all tasks and more detail, run gradle tasks --all

To see more detail about a task, run gradle help --task <task>

BUILD SUCCESSFUL

Total time: 7.299 secs

This build could be faster, please consider using the Gradle Daemon: https://docs.gradle.org/2.10/userguide/gradle_daemon.html
*/
```
##### Build the project
```
gradle build
``` 
```c
/*
:compileJava
:processResources UP-TO-DATE
:classes
:findMainClass
:jar
:bootRepackage
:assemble
:compileTestJava UP-TO-DATE
:processTestResources UP-TO-DATE
:testClasses UP-TO-DATE
:test UP-TO-DATE
:check UP-TO-DATE
:build

BUILD SUCCESSFUL

Total time: 10.425 secs

This build could be faster, please consider using the Gradle Daemon: https://docs.gradle.org/2.10/userguide/gradle_daemon.html
*/
```

##### List the contents of the project directory
```
ls -lahR
```
```c
/*

.:
total 24K
drwxrwxr-x 5 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 5 bachmeb bachmeb 4.0K Nov 26 19:21 ..
drwxrwxr-x 6 bachmeb bachmeb 4.0K Nov 26 19:31 build
-rw-rw-r-- 1 bachmeb bachmeb  598 Nov 26 19:29 build.gradle
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:22 .gradle
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:26 src

./build:
total 24K
drwxrwxr-x 6 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 5 bachmeb bachmeb 4.0K Nov 26 19:31 ..
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:31 classes
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:31 dependency-cache
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:31 libs
drwxrwxr-x 4 bachmeb bachmeb 4.0K Nov 26 19:31 tmp

./build/classes:
total 12K
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 6 bachmeb bachmeb 4.0K Nov 26 19:31 ..
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:31 main

./build/classes/main:
total 12K
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:31 ..
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:31 hello

./build/classes/main/hello:
total 20K
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:31 ..
-rw-rw-r-- 1 bachmeb bachmeb  670 Nov 26 19:31 Application.class
-rw-rw-r-- 1 bachmeb bachmeb  576 Nov 26 19:31 Greeting.class
-rw-rw-r-- 1 bachmeb bachmeb 1.2K Nov 26 19:31 GreetingController.class

./build/dependency-cache:
total 8.0K
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 6 bachmeb bachmeb 4.0K Nov 26 19:31 ..

./build/libs:
total 13M
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 6 bachmeb bachmeb 4.0K Nov 26 19:31 ..
-rw-rw-r-- 1 bachmeb bachmeb  13M Nov 26 19:31 rest-api-spring-0.1.0.jar
-rw-rw-r-- 1 bachmeb bachmeb 2.1K Nov 26 19:31 rest-api-spring-0.1.0.jar.original

./build/tmp:
total 16K
drwxrwxr-x 4 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 6 bachmeb bachmeb 4.0K Nov 26 19:31 ..
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:31 compileJava
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:31 jar

./build/tmp/compileJava:
total 12K
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 4 bachmeb bachmeb 4.0K Nov 26 19:31 ..
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:31 emptySourcePathRef

./build/tmp/compileJava/emptySourcePathRef:
total 8.0K
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:31 ..

./build/tmp/jar:
total 12K
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:31 .
drwxrwxr-x 4 bachmeb bachmeb 4.0K Nov 26 19:31 ..
-rw-r--r-- 1 bachmeb bachmeb   25 Nov 26 19:31 MANIFEST.MF

./.gradle:
total 12K
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:22 .
drwxrwxr-x 5 bachmeb bachmeb 4.0K Nov 26 19:31 ..
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:22 2.10

./.gradle/2.10:
total 12K
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:22 .
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:22 ..
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:24 taskArtifacts

./.gradle/2.10/taskArtifacts:
total 76K
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:24 .
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:22 ..
-rw-rw-r-- 1 bachmeb bachmeb   30 Nov 26 19:22 cache.properties
-rw-rw-r-- 1 bachmeb bachmeb   17 Nov 26 19:31 cache.properties.lock
-rw-rw-r-- 1 bachmeb bachmeb  21K Nov 26 19:31 fileHashes.bin
-rw-rw-r-- 1 bachmeb bachmeb  27K Nov 26 19:31 fileSnapshots.bin
-rw-rw-r-- 1 bachmeb bachmeb  19K Nov 26 19:31 outputFileStates.bin
-rw-rw-r-- 1 bachmeb bachmeb  20K Nov 26 19:31 taskArtifacts.bin

./src:
total 12K
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:26 .
drwxrwxr-x 5 bachmeb bachmeb 4.0K Nov 26 19:31 ..
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:26 main

./src/main:
total 12K
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:26 .
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:26 ..
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:26 java

./src/main/java:
total 12K
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:26 .
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:26 ..
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:28 hello

./src/main/java/hello:
total 20K
drwxrwxr-x 2 bachmeb bachmeb 4.0K Nov 26 19:28 .
drwxrwxr-x 3 bachmeb bachmeb 4.0K Nov 26 19:26 ..
-rw-rw-r-- 1 bachmeb bachmeb  297 Nov 26 19:28 Application.java
-rw-rw-r-- 1 bachmeb bachmeb  667 Nov 26 19:27 GreetingController.java
-rw-rw-r-- 1 bachmeb bachmeb  328 Nov 26 19:27 Greeting.java
*/
```

##### Initialize the wrapper scripts
```
gradle wrapper
```
```
:wrapper

BUILD SUCCESSFUL

Total time: 7.236 secs

This build could be faster, please consider using the Gradle Daemon: https://docs.gradle.org/2.10/userguide/gradle_daemon.html
```
##### List the contents of the project directory
```
ll
```
```c
/*total 28
drwxrwxr-x 6 bachmeb bachmeb 4096 Nov 26 19:31 build
-rw-rw-r-- 1 bachmeb bachmeb  598 Nov 26 19:29 build.gradle
drwxrwxr-x 3 bachmeb bachmeb 4096 Nov 26 20:33 gradle
-rwxrwxr-x 1 bachmeb bachmeb 4971 Nov 26 20:33 gradlew
-rw-rw-r-- 1 bachmeb bachmeb 2404 Nov 26 20:33 gradlew.bat
drwxrwxr-x 3 bachmeb bachmeb 4096 Nov 26 19:26 src
```

##### Build the application
```
./gradlew build
```
```
:compileJava
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

Total time: 12.447 secs

This build could be faster, please consider using the Gradle Daemon: https://docs.gradle.org/2.10/userguide/gradle_daemon.html
```
##### See if anything is running on port 8080
```
sudo lsof -P -n -iTCP
```

##### Run the JAR file
```
java -jar build/libs/rest-api-spring-0.1.0.jar
```
```c
/*


  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v1.3.2.RELEASE)

2016-11-26 20:42:42.983  INFO 21111 --- [           main] hello.Application                        : Starting Application on api.proximal.us with PID 21111 (/home/bachmeb/git/rest-api-spring/project2/build/libs/rest-api-spring-0.1.0.jar started by bachmeb in /home/bachmeb/git/rest-api-spring/project2)
2016-11-26 20:42:42.999  INFO 21111 --- [           main] hello.Application                        : No active profile set, falling back to default profiles: default
2016-11-26 20:42:43.160  INFO 21111 --- [           main] ationConfigEmbeddedWebApplicationContext : Refreshing org.springframework.boot.context.embedded.AnnotationConfigEmbeddedWebApplicationContext@7cdd964e: startup date [Sat Nov 26 20:42:43 EST 2016]; root of context hierarchy
2016-11-26 20:42:44.415  INFO 21111 --- [           main] o.s.b.f.s.DefaultListableBeanFactory     : Overriding bean definition for bean 'beanNameViewResolver' with a different definition: replacing [Root bean: class [null]; scope=; abstract=false; lazyInit=false; autowireMode=3; dependencyCheck=0; autowireCandidate=true; primary=false; factoryBeanName=org.springframework.boot.autoconfigure.web.ErrorMvcAutoConfiguration$WhitelabelErrorViewConfiguration; factoryMethodName=beanNameViewResolver; initMethodName=null; destroyMethodName=(inferred); defined in class path resource [org/springframework/boot/autoconfigure/web/ErrorMvcAutoConfiguration$WhitelabelErrorViewConfiguration.class]] with [Root bean: class [null]; scope=; abstract=false; lazyInit=false; autowireMode=3; dependencyCheck=0; autowireCandidate=true; primary=false; factoryBeanName=org.springframework.boot.autoconfigure.web.WebMvcAutoConfiguration$WebMvcAutoConfigurationAdapter; factoryMethodName=beanNameViewResolver; initMethodName=null; destroyMethodName=(inferred); defined in class path resource [org/springframework/boot/autoconfigure/web/WebMvcAutoConfiguration$WebMvcAutoConfigurationAdapter.class]]
2016-11-26 20:42:45.556  INFO 21111 --- [           main] s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat initialized with port(s): 8080 (http)
2016-11-26 20:42:45.588  INFO 21111 --- [           main] o.apache.catalina.core.StandardService   : Starting service Tomcat
2016-11-26 20:42:45.589  INFO 21111 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet Engine: Apache Tomcat/8.0.30
2016-11-26 20:42:45.752  INFO 21111 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2016-11-26 20:42:45.752  INFO 21111 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 2607 ms
2016-11-26 20:42:46.303  INFO 21111 --- [ost-startStop-1] o.s.b.c.e.ServletRegistrationBean        : Mapping servlet: 'dispatcherServlet' to [/]
2016-11-26 20:42:46.312  INFO 21111 --- [ost-startStop-1] o.s.b.c.embedded.FilterRegistrationBean  : Mapping filter: 'characterEncodingFilter' to: [/*]
2016-11-26 20:42:46.313  INFO 21111 --- [ost-startStop-1] o.s.b.c.embedded.FilterRegistrationBean  : Mapping filter: 'hiddenHttpMethodFilter' to: [/*]
2016-11-26 20:42:46.313  INFO 21111 --- [ost-startStop-1] o.s.b.c.embedded.FilterRegistrationBean  : Mapping filter: 'httpPutFormContentFilter' to: [/*]
2016-11-26 20:42:46.313  INFO 21111 --- [ost-startStop-1] o.s.b.c.embedded.FilterRegistrationBean  : Mapping filter: 'requestContextFilter' to: [/*]
2016-11-26 20:42:46.843  INFO 21111 --- [           main] s.w.s.m.m.a.RequestMappingHandlerAdapter : Looking for @ControllerAdvice: org.springframework.boot.context.embedded.AnnotationConfigEmbeddedWebApplicationContext@7cdd964e: startup date [Sat Nov 26 20:42:43 EST 2016]; root of context hierarchy
2016-11-26 20:42:46.945  INFO 21111 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/greeting]}" onto public hello.Greeting hello.GreetingController.greeting(java.lang.String)
2016-11-26 20:42:46.950  INFO 21111 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/error],produces=[text/html]}" onto public org.springframework.web.servlet.ModelAndView org.springframework.boot.autoconfigure.web.BasicErrorController.errorHtml(javax.servlet.http.HttpServletRequest,javax.servlet.http.HttpServletResponse)
2016-11-26 20:42:46.953  INFO 21111 --- [           main] s.w.s.m.m.a.RequestMappingHandlerMapping : Mapped "{[/error]}" onto public org.springframework.http.ResponseEntity<java.util.Map<java.lang.String, java.lang.Object>> org.springframework.boot.autoconfigure.web.BasicErrorController.error(javax.servlet.http.HttpServletRequest)
2016-11-26 20:42:47.016  INFO 21111 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/webjars/**] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
2016-11-26 20:42:47.017  INFO 21111 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/**] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
2016-11-26 20:42:47.096  INFO 21111 --- [           main] o.s.w.s.handler.SimpleUrlHandlerMapping  : Mapped URL path [/**/favicon.ico] onto handler of type [class org.springframework.web.servlet.resource.ResourceHttpRequestHandler]
2016-11-26 20:42:47.268  INFO 21111 --- [           main] o.s.j.e.a.AnnotationMBeanExporter        : Registering beans for JMX exposure on startup
2016-11-26 20:42:47.373  INFO 21111 --- [           main] s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat started on port(s): 8080 (http)
2016-11-26 20:42:47.384  INFO 21111 --- [           main] hello.Application                        : Started Application in 5.382 seconds (JVM running for 6.102)
*/
```

##### Test the service
* Go to http:// [ec2 ip address] :8080/greeting
```
{"id":1,"content":"Hello, World!"}
```
* Provide a name query string parameter with http://[ec2 ip address]:8080/greeting?name=Brian  
```
{"id":2,"content":"Hello, Brian!"}
```
