# Java / Spring Boot setup guide

## Contents

1. Pre-reqs
2. [Demo greenfield app](#demo-greenfield-app)
3. [Build, Run, and Debug](#building-running-and-debugging)
4. [Best Practices](#best-practices)
5. [Hot Reload Support](#hot-reload-support)
6. [Solutions to Possible Error Scenarios](#Solutions-to-Possible-Error-Scenarios)

## Pre-reqs

**Maven** - https://maven.apache.org/install.html
1. Go to the Link above, click downloads in the top right corner, download “Binary Zip Archive” for version 3.8.x
2. Unzip to `C:\devl\java`
3. Set MVN_HOME environment variable to folder (EX: `C:\devl\java\apache-maven-3.8.6-bin\apache-maven-3.8.6`)
4. Add `%MVN_HOME%\bin` to PATH variable.
5. Open MVN_HOME\conf and change settings.xml to the one listed at ___

**JDK** - https://www.oracle.com/java/technologies/downloads/

1. Download & run the latest Java JDK for Windows (x64 MSI Installer)
2. Set JAVA_HOME environment variable to new install folder (EX: `C:\Program Files\Java\jdk-19`)
3. Add `%JAVA_HOME%\bin` to PATH variable

**VS Code Extensions**

1. Spring Boot Extension Pack
2. Extension Pack for Java
3. SonarLint

**SSL Certs**

[Install internal certs into JDK]

## Demo greenfield app

https://spring.io/guides/gs/rest-service/

Manually initialize the project using the below config

Spring Initializer - https://start.spring.io/

1. Generate a new project like what's below
    * Project = Maven Project
    * Language = Java
    * Spring Boot = 3.0.2
    * Group Name = com.example
    * artifact name = demo
    * packaging = jar
    * Java = 19
    * Dependencies = Spring Web
2. Extract the folder to a location of your choice
3. Continue following the instructions in the demo
4. Once you have the 3 files in your project (DemoApplication.java, Greeting.java, and GreetingController.java) run `mvn spring-boot:run`
5. Ensure you can hit http://localhost:8080/greeting and http://localhost:8080/greeting?name=yourName

## Build Run and Debug

For any Spring Boot project, you need to build it with `mvn clean install` (or `mvn clean install -DskipTests=true` if that failed) before running/debugging. If your app has multiple projects, cd to the ____-build folder before running the install. If any resource fails to build in the terminal's build summary, troubleshoot with the VSCode PROBLEMS tab.

Once the terminal's build summary says BUILD SUCCESS, you can run apps from VSCode's Run tab at the top, or with the command `mvn spring-boot:run`. Optionally you can instead add the Spring Boot Dashboard extension, which adds an icon to vscode's left side panel, then use that to boot up/debug your app.

Note these are generic instructions: some existing apps might have a script or other instruction to run it.

See our separate guide to [Debug apps in VSCode]

## Best Practices

[other internal guides]

New Java apps need to have [security scanner] set up. See our [setup guide].

See our guide to [pipeline creation & requirements]

Our [chat channel] is a good resource if you have any questions.

## Hot Reload Support

https://docs.spring.io/spring-boot/docs/1.5.16.RELEASE/reference/html/using-boot-devtools.html

Add the dependency to your pom file
```
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-devtools</artifactId>
      <optional>true</optional>
    </dependency>
```

## Solutions to Possible Error Scenarios

1. **Maven- No plugin found for prefix 'spring-boot' in the current project and in the plugin groups.**

    If you are running the `mvn spring-boot:run` from the command line, make sure you are in the directory that contains the `pom.xml` file. Otherwise, you will run into `No plugin found for prefix 'spring-boot'` in the current project and in the plugin groups error.

2. **whitelabel error page spring boot**

    Make sure that your main class is in a root package above other classes. When you run a Spring Boot Application, (i.e. a class annotated with `@SpringBootApplication`), Spring will only scan the classes below your main class package. In the current scenario since the GroupName: `com.example`, the main application will be under `src\main\java\com\example\demo` so the Greeting controller package must be under `src\main\java\com\example\demo\web` (`web` can be any folder name you want). Follow this structure for both Greeting.java and GreetingController.java.

3. **SSL exception or PKIX errors**

    If you're having errors related to SSL, PKIX, or "trustAnchors" make sure your SSL certs are up to date (see pre-reqs section above). If you're still having issues after installing the current certs, you might need to move your Java installation to a folder that doesn't contain spaces (i.e. not Program Files).
