# Getting Started

## Overview

JPro allows you to run your JavaFX applications directly in the browser - no rewriting required. Your app runs on the server, and the browser displays the UI in real time via WebSockets.

This means you can **write once** and deploy to **desktop and web** simultaneously. Users only need a modern browser; no plugins or installations are required.

---

### Key Points

> **Server-side runtime**
>
> Only your application’s UI is streamed to the browser. This keeps client devices lightweight and ensures your business logic stays secure.

> **Full JavaFX support**
>
> Most JavaFX APIs work out of the box. The [JPro Platform](https://github.com/JPro-one/JPro-Platform) open source libraries provide useful utilities for web-specific features.

> **Flexible scaling options**
>
> JPro's load balancer supports both multi-user and single-user JVMs, allowing you to scale efficiently according to your application's architecture.

### Prerequisites

Before you start, ensure you have:

| Requirement | Notes |
| --- | --- |
| **Java 17+** | JPro officially supports up to Java 25 |
| **JavaFX 17 - 25** | Ensure your project uses a supported JavaFX version |
| **Gradle or Maven** | Use whichever suits your preference |
| **Modern Browser** | JPro works on both desktop and mobile browsers so long as there is a stable internet connection |

### Hello World

The quickest way to get started is the [Hello World for Gradle](https://github.com/JPro-one/HelloJPro) or [Maven](https://github.com/JPro-one/HelloJPro-Maven). Clone either, then run:

```bash
# Gradle
./gradlew jproRun

# Maven
mvn jpro:run
```

Your JavaFX app will appear in the browser within seconds.


## Gradle setup

The simplest way to begin is by using **Gradle** as your build tool.
JPro offers a plugin for Gradle that enables you to effortlessly launch JPro from an existing project.

For a straightforward reference project, consider exploring the [HelloJPro-gradle](https://github.com/JPro-one/HelloJPro) example, which is also [available to view online](https://demos.jpro.one/helloworld.html) in our demos.

### `1` Set up Gradle

We generally recommend adding a Gradle wrapper for your project to keep version management simple for all developers.

To set this up for your project, you will need to [download & install Gradle](https://gradle.org/install/).

```html
$ gradle wrapper --gradle-version {gradleVersion} --distribution-type all
```

You only need to set this up once, and other users can use the project without having Gradle installed if they wish by using `./gradlew` commands.

### `2` Create the Gradle scripts

Create the file `settings.gradle` and put it into your **project’s root directory**.
Then add the following `buildscript` configuration to the file:

```groovy
buildscript {
  repositories {
    gradlePluginPortal()

    maven {
      url "https://sandec.jfrog.io/artifactory/repo"
    }
  }

  dependencies {
    classpath "one.jpro:jpro-gradle-plugin:2025.3.3"
  }
}
```

Create or open the `build.gradle` file in your **project’s root directory**, then add the following configuration.

```groovy
plugins {
    id 'org.openjfx.javafxplugin' version "$javafxPluginVersion"
    id 'jpro-gradle-plugin'
}

version = "$projectVersion"
group = 'one.jpro'

compileJava {
    sourceCompatibility = 21
    targetCompatibility = 21
}

repositories {
    mavenCentral()
}

javafx {
    version = "$javafxVersion"
    modules = ['javafx.graphics', 'javafx.controls', 'javafx.fxml', 'javafx.media', 'javafx.web']
}

dependencies {
    implementation "one.jpro:jpro-webapi:$jproVersion"
}

application {
    // Define the main class for the application.
    mainClassName = 'one.jpro.hellojpro.HelloJProFXML'
}

jpro {
    // jpro server port
    port = 8080
}
```

The `gradle.properties` file defines all necessary version strings. It looks like the following:

```
projectVersion = 1.0-SNAPSHOT
jproVersion = 2025.3.3
javafxPluginVersion = 0.1.0
javafxVersion = 24.0.2
```

### `3` Run the app

In a terminal session, navigate to the main project directory and enter the command:

```bash
./gradlew jproRun
```

Your app will start running and, by default, will automatically open in your default browser.

## Maven setup

JPro provides a plugin for Maven, which allows you to easily start JPro from an existing project.

For a straightforward reference project, consider exploring the [HelloJPro-Maven](https://github.com/JPro-one/HelloJPro-Maven/) example, which is also [available to view online](https://demos.jpro.one/helloworld.html) in our demos.

### `1` Install Maven

Maven can be downloaded and installed [here](https://maven.apache.org/).

### `2` Create the Maven script

Create the file `pom.xml` and put it into your **project’s root directory**.

You can either download a template file [here](https://github.com/JPro-one/HelloJPro-Maven/blob/master/pom.xml) or use the following:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>example-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>
  <properties>
    <jpro.version>2025.3.3</jpro.version>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <java.version>21</java.version>
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <maven.compiler.target>${java.version}</maven.compiler.target>
    <maven.compiler.release>${java.version}</maven.compiler.release>
    <javafx.version>24.0.2</javafx.version>
  </properties>
  <name>Hello JPro!</name>
  <url>https://www.jpro.one/</url>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
      </plugin>
      <plugin>
        <groupId>one.jpro</groupId>
        <artifactId>jpro-maven-plugin</artifactId>
        <version>${jpro.version}</version>
        <configuration>
          <mainClassName>com.example.JavaFXApp</mainClassName>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <pluginRepositories>
    <pluginRepository>
      <id>jpro - sandec repository</id>
      <url>https://sandec.jfrog.io/artifactory/repo</url>
    </pluginRepository>
  </pluginRepositories>
  <repositories>
    <repository>
      <id>jpro - sandec repository</id>
      <url>https://sandec.jfrog.io/artifactory/repo</url>
    </repository>
  </repositories>
  <dependencies>
    <dependency>
      <groupId>org.openjfx</groupId>
      <artifactId>javafx-controls</artifactId>
      <version>${javafx.version}</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.openjfx</groupId>
      <artifactId>javafx-web</artifactId>
      <version>${javafx.version}</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.openjfx</groupId>
      <artifactId>javafx-swing</artifactId>
      <version>${javafx.version}</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.openjfx</groupId>
      <artifactId>javafx-fxml</artifactId>
      <version>${javafx.version}</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.openjfx</groupId>
      <artifactId>javafx-media</artifactId>
      <version>${javafx.version}</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>one.jpro</groupId>
      <artifactId>jpro-webapi</artifactId>
      <version>${jpro.version}</version>
      <scope>compile</scope>
    </dependency>
  </dependencies>
</project>
```

### `3` Run the app

Start a **Terminal session**, move to the **main project directory** and enter the command:

```groovy
mvn jpro:run
```

Now you should see your app running inside your standard browser.

## Build commands

The `gradle` & `maven` JPro plugins provide simple commands to **run your application locally** during development as well as **create a production release**.

---

For users with Gradle installed, you can replace `./gradlew` with `gradle` for all commands.

### Local Development

To test your application during development, the `jproRun` command will run your app on [localhost](http://localhost).

| **JPro Command**                     | **Description**                                                                                                      |
|--------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| `./gradlew jproRun` / `mvn jpro:run` | Runs and opens the application in a new browser tab, defined by the `mainClassName` in your build.gradle or pom.xml. |
| `ctrl+c`                             | Stops the app / server process running in the current terminal.                                                      |

You can also run your server in the background and manage it using these commands:

| **JPro Command**                             | **Description** |
|----------------------------------------------| --- |
| `./gradlew jproStart` / `mvn jpro:start`     | Starts a single JPro server in the background. |
| `./gradlew jproRestart` / `mvn jpro:restart` | Automatically stops the currently running JPro server before restarting it. |
| `./gradlew jproStop` / `mvn jpro:stop`       | Stops the JPro server running in the background. |

### Production Release & Server Commands

When it’s time to release or run your JPro server remotely, you can use the following commands to create a **zip-file** containing a build of the your project, including dependencies for both JPro and the current project.

| Command                 | Release File Path                         |
|-------------------------|-------------------------------------------|
| `./gradlew jproRelease` | `build/distributions/<app-name>-jpro.zip` |
| `mvn jpro:release`      | `target/<app-name>-jpro.zip`              |

In the unzipped folder you can find a start-script: `bin/start.sh`. Run this to start your JPro server.

# Using JPro

## Build configuration

JPro properties below are available in both Gradle & Maven.

- The Gradle plugin is configured under the `jpro` tag of `build.gradle`.
- The Maven plugin is configured under the `<plugin>` tag of `pom.xml`.

| Property | Default value | Description |
| --- | --- | --- |
| jproVersion | The version of the `jpro-gradle-plugin` | The JPro-version to be used, for example: `2025.3.3` |
| javafxVersion | “auto” | Possible values are `auto`, `latest`, or a specific supported version number e.g. `21`. |
| openingPath | “/” | On `jproRun` the Browser is automatically opened. This variable defines the path of the opened URL. |
| port | 8080 | The port to which the server should listen. |
| workingDir |  | The working directory of the JPro application. |
| releaseName |  | Sets the name of the zip generated by `jproRelease`. Also, `-jpro` postfix will be added to the resulting filename. If this property is not set, the project name will be used instead. |
| releasePlatforms | [“current”] | Includes the binaries for the specified platforms in the release zip generated by `jproRelease`. Possible values are `linux`, `linux-aarch64`, `mac`, `mac-aarch64`, `win`. Default value is `current`, which means the current platform is included and can be used in combination with the others, otherwise use `all` as shortcut to include them all. |
| jproReleaseFiles | [:] | A map of paths and files, which should be added to the zip, generated by `jproRelease` |
| JVMArgs | [ ] | A list of arguments, which are used to run JPro. |
| openURLOnStartup | true | Tells JPro, whether the Browser should be opened after calling `jproRun` |
| visible | false | If true, an additional window, beside the browser window, hosts the original javafx-application. This is for debugging, only. It impacts the performance negatively. |
| useFontConfig | false | Tells the Server, whether the library fontconfig should be used to resolve fonts. It’s deactivated by default to make sure, the font is always the same. |
| useModuleSystem | false | When set to true, all dependencies are loaded as modules. |
| useZGC | true | When set to true, the ZGC is used as the garbage collector. |
| verbose | false | If set to true, the start arguments of the JPro server are printed to the console. |

### JPro-only dependencies with Gradle

In Gradle, `jproOnly` can be used to configure any dependencies which should only be used when running the application as a JPro server.

```jsx
...
dependencies {
  jproOnly "com.mycompany:some-library-jpro-implementation:1.0.0"
}
...
```

### Example `build.gradle` configuration

For Gradle, properties are set inside of `jpro { ... }`.

```jsx
jpro {
  visible = true
  port = 8083
  jproVersion = "2025.3.3"
  openURLOnStartup = false
  openingPath = "/fullscreen/"

  JVMArgs << '-Xmx3500m'    // Sets the memory for the JPro-Server
  

  // The following adds three files to the "data" folder, in the release zip.
  
  // These files have their names changed:
  jproReleaseFiles << JProReleaseFile(new File("target/file1.dat"), "/data/newname1.dat")
  jproReleaseFiles << JProReleaseFile(new File("target/file2.dat"), "/data/newname2.dat")

  // This adds a file with its default file name (file3.dat):
  jproReleaseFiles << JProReleaseFile(new File("target/file3.dat"), "/data/")
}
```

### Example `pom.xml` configuration

Note how for maven, the `version` is set directly under `<plugin>` while other properties are set under the `<configuration>` tag.

```xml
<plugin>
  <groupId>one.jpro</groupId>
  <artifactId>jpro-maven-plugin</artifactId>
  <version>${jproVersion}</version>
  <configuration>
      <visible>false</visible>
      <JVMArgs>
          <JVMArg>arg1</JVMArg>
          <JVMArg>arg2</JVMArg>
      </JVMArgs>
      <mainClassName>com.jpro.hellojpro.HelloJProFXML</mainClassName>
      <openingPath>/</openingPath>
      
      <jproReleaseFiles>
          <JProReleaseFile>
              <inputFile>${project.build.outputDirectory}/file1.dat</inputFile>
              <outputFile>/data/newname1.dat</outputFile>
          </JProReleaseFile>
          <JProReleaseFile>
              <inputFile>${project.build.outputDirectory}/file2.dat</inputFile>
              <outputFile>/data/newname2.dat</outputFile>
          </JProReleaseFile>
          
          <JProReleaseFile>
              <inputFile>${project.build.outputDirectory}/file3.dat</inputFile>
              <outputFile>/data/</outputFile>
          </JProReleaseFile>
      </jproReleaseFiles>
  </configuration>
</plugin>
```

## JPro config

The following properties can be set in the `jpro.conf` file:

| Property | Default value | Description |
| --- | --- | --- |
| jpro.preventSystemExit | true | Tells the JVM, to prevent calls to `java.lan.System.exit`. |
| jpro.adminUsername | "" | The username, to access logs, passwords etc. |
| jpro.adminPassword | "" | The password, to access logs, passwords etc. |
| jpro.gcWorkaroundStage | true | Activated a workaround for a memory leak in JavaFX when closing a stage. |
| jpro.logResourceAccess | false | Log all access to resources under the path `jpro/html`. |
| jpro.logUserInputEvents | true | Log all input events. |
| jpro.logConsole | true | Redirects the console output to the logging system. |
| jpro.logToJUL | false | Redirects the logging to the java.util.logging system. |
| jpro.logToJsonFormat | false | Logs the structured messages in JSON format. |
| jpro.logger.resource | "" | Location of the new logging configuration accessed as a resource. |
| jpro.logger.file | "" | Location of the new logging configuration accessed as a file. |
| jpro.logger.url | "" | Location of the new logging configuration accessed as a URL. |
| jpro.onJVMStartup | null | A string to a class, which should be executed during the startup of the JVM. |
| jpro.onFXStartup | null | A string to a class, which should be executed during the startup of the application, on the JavaFX Application Thread, after the server has started. |
| jpro.onJVMShutdown | null | A string to a class, which should be executed during the shutdown of the JVM. |
| jpro.addInstanceID | false | When true, all requests from the client, contain the current instance ID. |
| jpro.linkUnownedWindowsToFirstInstance | false | When true, all unowned windows are linked to the first instance. |
| jpro.websocketMaxMessageSize | 64kb | The maximum size of websocket messages sent by JPro. Too big messages get split into multiples. Useful when somewhere is a limitation on the size of messages. |
| [jpro.parent.pid](http://jpro.parent.pid) | null | The parent process id. When the parent process stops, the JPro server will also stop. |
| jpro.shortcutSource | “browser” | Possible values: “server” or “browser”. This choice determines whether the server’s or browser’s OS sets the shortcut key mapping. On Mac, it’s usually cmd. |

### Declaring multiple runnable applications

For an app to be **JPro enabled**, it must extend the class called `javafx.application.Application`.

It is possible to define multiple applications for JPro to run. Do do so, simply add multiple definitions under `jpro.applications`:

```jsx
jpro.applications {
  "appname1" = package.Application1
  "appname2" = package.Application2
}
```

By default, the `jproRun` or `jpro:run` command will run the app defined by the `mainClassName` set in your `build.gradle` or `pom.xml` respectively, as normal.

Specific applications can be accessed via URL, for example: "[https://localhost:8083/appname1](https://localhost:8083/appname1)" or "[https://localhost:8083/fullscreen/appname1](https://localhost:8083/fullscreen/appname1)"

Declared apps can also be specified in the `<jpro-app>` tag in your index.html or when embedded into another webpage by using the tag like follows:

```html
<jpro-app href="/app/appname1" />
```

## HTTP routes & resources

### Home route

In general, the `index.html` file is the default resource within each folder. This means that [http://localhost:8080/](http://localhost:8080/) will automatically point to `jpro/html/index.html`.

This is where your JPro app is typically embedded.

### Static resources

Any resources underneath `jpro/html/` are made publicly available by the JPro server. These can be accessed via URL based on their file path. For example:

`jpro/html/mypage.html` with "[http://localhost:8080/mypage.html](http://localhost:8080/)"

`jpro/html/myImage.jpg` with "[http://localhost:8080/myImage.jpg](http://localhost:8080/myImage.jpg)"

`jpro/html/folder/myImage.jpg` with "[http://localhost:8080/folder/myImage.jpg](http://localhost:8080/folder/myImage.jpg)"

### Adding a global default resource

JPro allows you to define a default resource that will be returned when a URL does not find a specific resource. This is most useful when used with the JPro Platform’s Routing library.

To do this, add a file named `defaultpage` (without file type suffix) under `jpro/html/`.

This is typically an HTML file with the same content & structure as your home `index.html`.

### Custom HTTP handlers

JPro allows you to add custom request handlers to the server API:

```jsx
ServerAPI.getServerAPI().addRequestHandler(request -> {
    if (request.getPath().equals("/test")) {
        return Response.of("Hello World!".getBytes());
    }

    return Response.empty();
});
```

You can then register this handler on startup, or anywhere inside the code of your website. This can be done by defining the `jpro.onFXStartup` flag inside your `build.gradle` file like this:

```jsx
jpro.onFXStartup = one.jpro.hellojpro.StartServer
```

The corresponding class should look like this:

```jsx
package one.jpro.hellojpro;

public class StartServer {

    public static void main(String[] args) {
        // your code
    }
}
```

Custom HTTP handlers can also be combined with the JPro load balancer to direct specific requests to specific JVMs. To do this, you first need to retrieve the instance ID:

```jsx
WebAPI.getWebAPI(stage).getInstanceID(); // e.g. 82489-1-1-1
```

Once you have the instance ID, you can add it as a query parameter to your request URL. The load balancer will then forward the request to the correct JVM:

```jsx
[object Object]
```

## JavaFX node attributes

In some cases, you may wish to override certain behavior for a specific element or area of your application instead of the entire application.

You can do this **from your JavaFX code** at either the Window or Node level by applying attributes that will only be used by JPro.

### **JavaFX Window Attributes**

The following can be set by calling `window.getProperties().put("attributeName", attributeValue)` in your JavaFX code:

| Attribute | Default value | Description |
| --- | --- | --- |
| jpro-hidden | false | When true, then the window is not rendered as part of it’s owners instance. |

### **JavaFX Node Attributes**

These attributes can be set by calling `node.getProperties().put("attributeName", attributeValue)` in your JavaFX code.

| Attribute | Default value | Description |
| --- | --- | --- |
| translate | true | When false, disables the text translation from the browser.

The translation rule is inherited from the parent node.

For example, this can be useful if want to disable translation for a specific text-input control. |
| vkType | null | Defines the virtual keyboard, used for a given `TextInputControl`.

Reference the [mdn web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) for possible values.

Only values that change the virtual keyboard have an effect. Other values will not work. |

## Instance close strategies

This documentation describes the structure for configuring the close instance strategies JPro should use under different circumstances, which can be set in the `jpro.conf` file.

The ideal configuration for your app will depend on how long you want sessions to persist for each user or browser tab. This may look very different for an internal back office tool with one instance per user versus a website with many visitors who may frequently open and close multiple tabs.

### Configuration Structure

JPro’s default configuration is structured into three optional strategies: `short`, `medium`, and `long`. Each strategy contains the following properties:

- `until`: This property defines the duration of each strategy. The last strategy **must not** have this value defined.
- `closeOnTabCloseAfter`: Number of seconds the instance will remain open after the tab is closed. `-1` means it will not close after tab close.
- `closeOnDisconnectAfter`: Number of seconds the instance will remain open if a disconnect is detected. `-1` means it will not close after disconnect.
- `closeOnAFKAfter`: Number of seconds the instance will remain open after a user is detected to be inactive / AFK (Away From Keyboard). `-1` means it will not close after AFK.
- `closeOnBackgroundAfter`: Number of seconds the instance will remain open if the application goes to the background. `-1` means it will not close after going to the background.

The current default configuration looks like this:

```jsx
jpro {
  closeInstanceStrategy = null // important to disable all values of the default strategy
  closeInstanceStrategy {
    short {
      until = 60
      closeOnTabCloseAfter = 0
      closeOnDisconnectAfter = 5
      closeOnAFKAfter = -1
      closeOnBackgroundAfter = -1
    }
    medium {
      until = 900
      closeOnTabCloseAfter = 0
      closeOnDisconnectAfter = 30
      closeOnAFKAfter = -1
      closeOnBackgroundAfter = -1
    }
    long {
      closeOnTabCloseAfter = 0
      closeOnDisconnectAfter = 180
      closeOnAFKAfter = -1
      closeOnBackgroundAfter = -1
    }
  }
}
```

## Debug utilities

JPro servers provide a variety of utilities that can be useful for debugging or for system administrators to monitor information at runtime. These can most easily be accessed via URL while your app is running.

> In production, these pages are only accessible if a password has been configured.
>

| URL | Content |
| --- | --- |
| /status | Returns a page with some statistics about the running server. |
| /status/alive | Asks the running server whether it’s alive and ok., When the javafx-thread is not being blocked and running normally, the server responds with the word “alive”. |
| /info/log/console.log | Returns a log-file with all the console-output of the application. The logging of the console-output can be deactivated in the `jpro.conf`. |
| /info/log/info.log | Returns a log-file with all the info-logs in the jpro-server. |
| /info/log/warning.log | Returns a log-file with all the warning-logs in the jpro-server. |
| /info/log/error.log | Returns a log-file with all the error-logs in the jpro-server. |
| /info/log/activity.log | Returns a log-file with all the activity-logs in the jpro-server. |
| /info/all.zip | Returns all files in the log-folder as a zip-file. |
| /info/fxstack | Returns the whole stack-trace of the javafx-thread. Useful for debugging blocked javafx-threads. |
| /info/minmemory | Returns the memory-usage of the jvm, after running the garbage-collector. |
| /test/ | Creates a simple test-page, which opens the provided application. |
| /test/fullscreen/ | Creates a simple test-page, which opens the provided application in fullscreen. |
| /test/scrolling/ | Creates a simple test-page, which opens the provided application as natively scrollable. |
| /info/heapdumps/heapdump.hprof | Downloads the heapdump of the server. Useful for finding memory-leaks with tools like [VisualVM](https://visualvm.github.io/) |
| /jpro/api/instances | A list of all currently open instances. |

For example, the `/status` route might return the following information:

```json
{
  "Start time" : "Thu, 9 Oct 2025 14:00:22 GMT",
  "Time running" : "00:01:41.310",
  "Instances created": 1016,
  "Instances active": 7,
  "Instances afk": 6,
  "Views created": 1039,
  "Views active": 7,
  "Views afk": 6,
  "Framerate": 1,
  "Windows open": 7,
  "Max memory": "3000 mB",
  "Used memory(heap)": "582 mB",
  "Used memory(% heap)": "19.41%",
  "Used memory(non-heap)": "28 mB",
  "Committed memory(non-heap)": "32 mB",
  "JavaFX thread CPU usage": "0.00%",
  "Java version": "24.0.2",
  "JavaFX version": "24.0.2-jpro+4",
  "JPro version": "2025.3.0",
  "Latest JPro GIT commit": "41baf2814ad516ef3668d44d7d8c22732e3973ca",
  "JPro build time": "Wed, 10 Sep 2025 07:41:53 GMT",
  "Server name": "X584",
  "Mode": "prod",
  "Deployment": "GRADLE-Distribution",
  "Free system memory": "282 mB",
  "Total system memory": "15610 mB",
  "System load": "4.27%",
  "JVM Load": "2.76%",
  "Free disk space": "128005 mB",
  "Total disk space": "153513 mB",
  "Default Java encoding": "UTF-8",
  "Default Java local" : "en_DE",
  "Default Java timezone" : "Central European Time",
  "Open instances" : [ "hellojpro", "hellojpro" ]
}
```

### Restricting access

Access can be restricted by a `username` and `password`. Your

This can be set up in the `jpro.conf` file, for example:

```jsx
jpro.adminUsername = "admin"
jpro.adminPassword = "secret"
```

### Additional utilities

> We find [ScenicView](https://github.com/JonathanGiles/scenic-view) very useful while developing, and it works perfectly in the web!
>

In the case that a server is no longer responding, these commands can be useful:

```bash
jstack `cat RUNNING_PID`
jcmd  `cat RUNNING_PID` GC.heap_info
jmap -dump:format=b,file=heapdump.hprof `cat RUNNING_PID`
```

## Logging

JPro provides the following a set of structured log messages out of the box:

| Log message | Description | Parameters |
| --- | --- | --- |
| Instance created | A new instance is created | app name, host name, instance id, browser, browser address, client address |
| Instance closed | An instance is closed | app name, host name, instance id, browser, browser address, client address, reason for closure |
| View created | A new view is created | app name, host name, instance id, browser, browser address, client address |
| View closed | A view is closed | app name, host name, instance id, browser, browser address, client address, reason for closure |
| Server started | A server is started | start time, operating system, jpro version |
| Server stopped | A server is stopped | running time, instances count, views count, operating system, jpro version, reason for stop |

### Custom logback configurations

To override the default JPro logging configuration, simply provide a new `logback.xml` file and specify its path in the `jpro.conf` file using one of the following options:

1. `jpro.logger.resource` - to access the file as a resource in the classpath
2. `jpro.logger.file` - to access the file as an external file
3. `jpro.logger.url` - to access the file as a URL

If the new configuration includes a `console` output, you have two options to address this:

1. Disable the `jpro.logConsole` option by setting its value to `false`.
2. Set the `additivity` attribute for your `Console` logger to `false` as shown below:

```xml
<logger name="Console" additivity="false"/>
```

### Logging to JSON

Enabling the `jpro.logToJsonFormat` option in your `jpro.conf` file will make JPro output its structured log messages in JSON format. This option is disabled by default.

The following table describes each parameter:

| Parameter | JSON key | Description |
| --- | --- | --- |
| source | source | The source of the log message |
| event | event | The event being logged |
| app name | app_name | The name of the application |
| host name | host_name | The name of the host |
| instance id | instance_id | The ID of the instance |
| browser | browser | The name of the browser used by the client |
| browser url | browser_url | The URL displayed on the client’s browser |
| client address | client_ip | The ip address of the client |
| start time | start_time | The time when the server was started |
| running time | running_time | The time when the server was stopped |
| instances count | instances_count | The number of instances running on the server |
| views count | views_count | The number of views running on the server |
| operating system | os_name | The name operating system of the server |
| jpro version | jpro_version | The version of JPro running on the server |
| reason for closure | reason | The reason why the instance/view/server was closed or stopped |

## Tips & Limitations

### Potential issues

- Wait-, sleep-, and showAndWait commands in the JavaFX thread stop your app from being accessible. Dialogue boxes are a common culprit here.
- JPro requires a JRE without JavaFX. This is the standard since Java11. Most JDK Vendors, which bundle JavaFX, also provide a version without JavaFX.
- Be careful with **static variables**, as they can be shared between multiple instances on a single JVM. This may impact your instance management & how you approach horizontal scaling.

### Working with stages

JavaFX **Stages** can be opened with the [WebAPI](/api/2025.3.3/jpro.webapi/com/jpro/webapi/WebAPI.html)’s `openStageAsPopup(Stage stage)` and `openStageAsTab(Stage stage)` methods. An alternative is to create new windows or dialogues using a StackPane at the root of your application.

We have an example of implementing JPro-ready popups in this [sample-project](https://github.com/JPro-one/JPro-Samples/tree/master/popups).

### Performance tips

Generally, the better your JavaFX app’s performance, the better its performance will be when running on the server & scaled to many users.

To help minimize the load on your servers, you can optimize your apps by trying to:

- Minimize the number of nodes that are used to represent the scenegraph.
- Reuse existing nodes instead of creating new instances when possible. The TableView and ListView controls are great examples of where this can be applied.
- Try to avoid excessive use of shadow effects, as they can slow rendering performance.

### Features with limited support

> JavaFX 3D support is currently in open beta.
>
- The WebView class is very limited with JPro. To avoid issues, it can be replaced with `com.jpro.webapi.HTMLView`, as shown in [this sample](https://github.com/JPro-one/JPro-Samples/tree/master/html-jpro).
- MediaPlayer can be implemented using the [JPro Media](https://github.com/JPro-one/jpro-platform/tree/main/jpro-media) module.
- FileChooser can be made to work on the web with the [JPro File](https://github.com/JPro-one/jpro-platform/tree/main/jpro-file) module.

### Unsupported JavaFX features

- SwingNode
- Clipboard
- The following effect classes may not work as intended:
  `Blend`, `Bloom`, `BoxBlur`, `ColorInput`, `DisplacementMap`, `Glow`, `ImageInput`, `Lighting`, `MotionBlur`, `PerspectiveTransform`, `Reflection`
- [Dialog](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/Dialog.html), due to potential issues with blocking the JavaFX thread.

# Web Integration

## Custom index.html

To make your JPro application accessible via URL, an “index.html” needs to exist in the project structure under `src/main/resources/jpro/html/index.html`. If none exists, JPro will automatically add a default to your project.

You may want customize this in order to adjust meta information, or add additional scripts for analytics or cookie banners.

### Index.html Structure

As an example, let’s look at the `index.html` file from the HelloJPro project:

```html
<!DOCTYPE html>
<html>

<head>    
	<title>jpro Application: Hello JPro</title>
	<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
	<link rel="stylesheet" type="text/css" href="/jpro/css/jpro-fullscreen.css">    
	<link rel="stylesheet" type="text/css" href="/jpro/css/jpro.css">    

	<script src="/jpro/js/jpro.js" type="text/javascript"></script>
</head>

<body>
	<jpro-app href="/app/hellojpro" fullscreen="true"></jpro-app>
</body>

</html>
```

There are two key elements to look at:

- The `jpro.js` script in the `<head>` is what loads JPro and starts your app on the page.
- The `<jpro-app>` tag in the `<body>` tells JPro which app to start, and where to place it in the DOM. JPro will automatically start the app specified in your `jpro.conf` file that matches the name in the tag’s  `href` property.

We also see some additional tags in the `<head>`, let’s break them down:

- The `<title>` tag describes the default title of your app shown on the browser tab or read by search engines. Your application can override this at runtime.
- The viewport `<meta>` tag ensures the browser’s scale is at default, and disallows the user from attempting to resize, as this behavior should typically be handled by your JavaFX app.
- The two stylesheet `<link>` elements prepares the browser to ready to render your app without any interfering default styles.

---

### Specifying the app name in jpro.conf

In order to start the app specified in your `index.html`, the name specified in the `<jpro-app>` tag must be defined in your `jpro.conf` file. It should point to the class that you want JPro to launch.

Continuing our example, the `jpro.conf` of the HelloJPro project includes the following:

```
jpro.applications {
    //jpro apps
    "hellojpro" = com.jpro.hellojpro.HelloJProFXML
}
```

## Embedding JPro

JPro can be **embedded into an existing html-page** by using the  `<jpro-app>` tag, similar to how it is included in a fullscreen app’s index.html.

To do so, your app must be running on a JPro server & publicly available via URL.

### Adding the JPro app tag to your HTML

First, the `jpro.js` script and `jpro.css` styling must be loaded from the server that is serving your JPro application. You can do this by adding the following to the HTML `<head>`:

```html
<link rel="stylesheet" type="text/css" href="/jpro/css/jpro.css">
<script src="/jpro/js/jpro.js" type="text/javascript"></script>
```

Second, add your JPro app to the HTML body where you wish to embed it. For example:

```html
<body>
	<h1>My JavaFX app in a website card</h1>
	<div class="Card">
		<!-- Your JPro will be loaded inside this div -->
		<jpro-app loader="none" href="/app/default" loader="false" />
	</div>
</body>
```

### Adjusting behavior with `<jpro-app>` tag attributes

The following attributes can be added to the HTML tag in order to customize how your app behaves when loaded.

| Attribute name | Default value | Description |
| --- | --- | --- |
| href |  | The URL of the application to be started. It is either the URL of the App’s websocket connection `wss://yourServer.com/app/myAppName`, or it’s the relative URL `/app/myAppName`. |
| fullscreen | “false” | When true, the JPro app is resized to the entire page. It also **sets autofocus** to true. |
| loader |  | Defines whether or not to activate the loading animation for this JPro-app. Valid values are: `"default"` `"none"` |
| loaderURL |  | Defines a gif file which can be used to replace the standard loader. |
| readonly | “false” | When true, the user can NOT do any data authoring to the scene. |
| disableShadows | “false” | Disables all shadows in the JPro-renderer. This might be useful, for rendering performance reasons. |
| disableEffects | “false” | Disables all effects in the JPro-renderer. This might be useful, for rendering performance reasons. |
| disableClip | “false” | Disables all clips in the JPro-renderer. This is useful for debugging. |
| disablePointerCapture | “false” | Disables the usage of pointer capture to get the mouse events. This is useful for debugging. |
| disableVirtualKeyboard | “false” | Disables the virtual keyboard on mobile devices. |
| autofocusEnabled | “false” | When true, the JPro-tag gets focused when the page is opened. This is useful for text-input, for example to enable the TextInput for a login-mask. |
| nativescrolling | “false” | When true, the scroll events are managed by html. Otherwise they are managed by the JPro app. |
| nativezooming | “false” | When true, the zoom events are managed by html. Otherwise they are managed by the JPro app. |
| userSelect | “false” | When true, the text selection is managed by html. Otherwise it is managed by the JPro app. |
| scale | “false” | When true, the JPro app’s scene is scaled to fit the html container. It works similar to `background-size: cover`in html. |
| stretch | “false” | When true, the JPro app’s scene is stretched to fit the html container. |
| fxwidth | “false” | When true, the width of the JPro-tag is managed by the JPro app. Otherwise the width is managed by html. |
| fxheight | “false” | When true, the height of the JPro-tag is managed by the JPro app. Otherwise the height is managed by html. |
| fxContextMenu | “true” | When true, the context menu of the browser is suppressed and NOT shown. Is useful, when the JPro app itself has got a context-menu to show instead. |
| printJSCommands | “false” | When true, all js-commands executed through the WebAPI are logged on the browser console. |
| timeUntilReconnect | “10000” | It specifies after how much time, the client tries to reconnect, when he didn’t hear anything from the server. |
| snapshot | “auto” | When set to true, the JPro app is rendered as a static image. On “auto” this only happens, when it’s indexed and WebSocket is not available. |
| rememberInstanceIDInCookie | “false” | When set to true, only one instance of the app is created per browser. |
| syncStageAttributes | “true” | When set to true, the stage title and icons attributes are synchronized between the JPro app and the browser. |
| image-render-quality | “” | It's value is forwarded to the image elements of JPro. Possibles values are for example `smooth` and `pixelated`. |

## WebAPI Overview

The WebAPI enables you to create custom JavaScript code that interoperates with JPro. It also allows you to make use of existing JavaScript code, and provides useful methods that help you build cross-platform solutions.

For example, the WebAPI allows you to:

- Detect the currently running platform, via `com.jpro.web.WebAPI.isBrowser`
- Get information about your current session, language, cookies, URL, etc.
- Communicate bi-directionally between client-side Javascript and server-based java code.

For details about the API itself, please reference the [WebAPI-documentation](/api/2025.3.3/jpro.webapi/com/jpro/webapi/WebAPI.html).

### Using the WebAPI with JPro

There are two ways to get access to the WebAPI:

- Let your app `extend JProApplication` and call `getWebAPI()`.
- Call either `WebAPI.getWebAPI(javafx.scene.Scene scene)` or
  `WebAPI.getWebAPI(javafx.stage.Window window)`.

### Using the WebAPI without JPro

The WebAPI can be imported as a jar without requiring JPro.

**Using Gradle**

```jsx
dependencies {
    ...
    implementation "one.jpro:jpro-webapi:2025.3.3"
    ...
}
```

**Using Maven**

```xml
<dependencies>
    ...
    <dependency>
        <groupId>one.jpro</groupId>
        <artifactId>jpro-webapi</artifactId>
        <version>${jproVersion}</version>
        <scope>compile</scope>
    </dependency>
    ...
</dependencies>
```

### Downloading the WebAPI Jar

If you need access to the WebAPI without Maven or Gradle, it can be downloaded from our [repository](https://sandec.jfrog.io/ui/native/repo/com/sandec/jpro/jpro-webapi/). Here is the [download link](https://sandec.jfrog.io/artifactory/repo/com/sandec/jpro/jpro-webapi/2025.3.3/jpro-webapi-2025.3.3.jar) for the latest version.

# Deployment

## Deploying on Linux

### Deployment Requirements

JPro can run on any server with a JVM. In most cases, Linux is used for production backends, and is thus also our go-to for JPro. Our recommended platform for JPro servers is Ubuntu.

Additional requirements include:

- JavaFX requires some libraries to run in a headless environment. Installing GTK and X11 is usually enough to run JavaFX.
- For production, it is highly recommended to use SSL. This is important as proxies sometimes manipulate the traffic stream, which may interfere with websockets functioning as intended.

### `1` Prepare your server

To run JPro on linux, the server must be configured correctly:

- Ensure you have all necessary dependencies installed. The simplest way to do this is to use one of our docker templates.
- Set up SSL using nginx (our recommendation) or apache. You can get free guides & SSL certificates from [Let’s encrypt / Certbot](https://certbot.eff.org/).

Use the guides in this section to put together the environment that suites your needs.

### `2` Create the binary

From your terminal, create a release ZIP containing your application. You can then copy the file to your server and unzip it.

| Command                 | Release File Path                         |
|-------------------------|-------------------------------------------|
| `./gradlew jproRelease` | `build/distributions/<app-name>-jpro.zip` |
| `mvn jpro:release`      | `target/<app-name>-jpro.zip`              |

### `3` Run JPro

In the unzipped folder you can find a start-script: `bin/start.sh`. Run this to start your JPro server.

## Docker templates

The following templates can be used as a reference and adjusted to your needs.

They assume you have a linux server with the appropriate Java version installed; we recommend using [Temurin](https://adoptium.net/temurin/releases/). Most other linux distributions can be configured in a similar way. All Linux distributions also work with ARM64.

### Ubuntu 24.04

(22.04 and 20.04 also work)

```docker
FROM amd64/ubuntu:24.04

RUN apt-get update
RUN apt-get install -y xorg libgtk-3-0
RUN apt-get install -y wget software-properties-common

# Add the Adoptium (Eclipse Temurin) APT repository and import the GPG key
RUN wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | apt-key add - && \
add-apt-repository --yes https://packages.adoptium.net/artifactory/deb/

# Install Temurin 21 JDK
RUN apt-get update && \
apt-get install -y temurin-21-jdk && \
apt-get clean && \
rm -rf /var/lib/apt/lists/*
```

### Debian Bookworm

```docker
FROM amd64/debian:bookworm

RUN apt-get update

RUN apt-get install -y xorg libgtk-3-0
RUN apt-get install -y wget software-properties-common

# Add the Adoptium (Eclipse Temurin) APT repository and import the GPG key
RUN apt-get install -y wget apt-transport-https gnupg
RUN wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | apt-key add -
RUN echo "deb https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | tee /etc/apt/sources.list.d/adoptium.list
# RUN wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | apt-key add - && \
#     add-apt-repository --yes https://packages.adoptium.net/artifactory/deb/

# Install Temurin 21 JDK
RUN apt-get update && \
    apt-get install -y temurin-21-jdk

RUN apt-get clean
```

### Fedora 39

```docker
FROM amd64/fedora:39

RUN dnf -y update
RUN dnf -y install gtk3 xorg-x11-server-Xvfb
RUN dnf -y install @base-x

RUN echo "[BellSoft]" > /etc/yum.repos.d/bellsoft.repo \
    && echo "name=BellSoft Repository" >> /etc/yum.repos.d/bellsoft.repo \
    && echo "baseurl=https://yum.bell-sw.com" >> /etc/yum.repos.d/bellsoft.repo \
    && echo "enabled=1" >> /etc/yum.repos.d/bellsoft.repo \
    && echo "gpgcheck=1" >> /etc/yum.repos.d/bellsoft.repo \
    && echo "gpgkey=https://download.bell-sw.com/pki/GPG-KEY-bellsoft" >> /etc/yum.repos.d/bellsoft.repo

RUN cat /etc/yum.repos.d/bellsoft.repo

RUN dnf -y update
RUN dnf -y install bellsoft-java21
```

## Nginx

In order to configure nginx for JPro, create & add the following content to `/etc/nginx/sites-enabled/jproconf.nginx.conf`:

```jsx
proxy_buffering    off;
proxy_set_header   X-Real-IP $remote_addr;
proxy_set_header   X-Forwarded-Proto $scheme;
proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
proxy_set_header   Host $http_host;
proxy_set_header   Upgrade $http_upgrade;
proxy_set_header   Connection "upgrade";
proxy_read_timeout 86400;
proxy_http_version 1.1;
```

Configure the domain for your JPro server by creating the following file and replacing `yourdomain` with your domain: `/etc/nginx/sites-enabled/yourdomain_com.nginx.conf`

```jsx
upstream jpro {
 server 127.0.0.1:8080;
}
server {
 listen 80;
 server_name yourdomain.com;  # List all domain names for this server #
 return 301 https://$host$request_uri;
}
server {
 listen 443;
 server_name yourdomain.com;
 tcp_nodelay on;

 ssl on;
 ssl_certificate     /path/ssl/yourdomain_com.chained.crt;
 ssl_certificate_key /path/ssl/yourdomain_com.key;

 location / {
   proxy_pass http://jpro;
 }
}
```

You can verify your configuration using the `sudo nginx -t` command from your terminal.

### SSL certificates & guides

You can get free guides & SSL certificates from [Let’s encrypt / Certbot](https://certbot.eff.org/).

## Apache2

While we typically recommend using nginx, JPro can also be used with Apache. In this case, Apache is used as a reverse proxy in order to forward the request from port 80/443 to the port used by your JPro server.

In order to use Apache with JPro you will need to install the following plugins:

```bash
sudo a2enmod proxy proxy_http rewrite ssl proxy_wstunnel
```

Once you’ve done this, you can configure your webpage in the file: `/etc/apache2/sites-enabled/000-default.conf`

```jsx
<VirtualHost *:80>

ServerAdmin webmaster@localhost
DocumentRoot /var/www/html

ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined
        
RewriteEngine On
ProxyPreserveHost On
ProxyRequests Off
SSLProxyEngine on

  # allow for upgrading to websockets
  RewriteEngine On
  RewriteCond %{HTTP:Upgrade} =websocket [NC]
  RewriteRule /(.*)           ws://localhost:8080/$1 [P,L]
  RewriteCond %{HTTP:Upgrade} !=websocket [NC]
  RewriteRule /(.*)           http://localhost:8080/$1 [P,L]

ProxyPass / http://localhost:8080/
ProxyPassReverse / http://localhost:8080/

</VirtualHost>
```

### SSL certificates & guides

You can get free guides & SSL certificates from [Let’s encrypt / Certbot](https://certbot.eff.org/).

# JPro Loadbalancer

## Overview & usage

The JPro Loadbalancer allows you to run multiple JPro Servers in parallel.

You can configure the ***maximum number of JPro Servers to automatically be started and stopped on demand*** by setting
the property `one.jpro.loadbalancer.localServerCount` inside the file named `application.properties` to your required
value. This provides you with a server landscape, which dynamically up and down scales according to current demand, but
still respects an overall system size limit.

You can configure the ***maximum number of sessions to be accepted per JPro Server*** by setting the property
`one.jpro.loadbalancer.sessionsPerServer` inside the file named `application.properties` to your required value.
This sets the rule for when additional JPro Servers should be available.

### Prerequisites

Make sure you already have a JPro project and a zip file, created with
the JProRelease command (either `./gradlew jproRelease`
or `./mvnw jpro:release`).

### Configure external servers

When configuring the `external servers` setup, ensure to set the `one.jpro.loadbalancer.localServerCount` property to 0.

To define additional external servers, utilize the prefix `one.jpro.loadbalancer.externalServer` followed by an index starting from 1.

This allows you to add as many external servers as required. There is no need to configure other non required properties, as the JPro Loadbalancer will automatically load the default values.

Use the following configuration as an example:

```
# Set the count of local servers to 0
one.jpro.loadbalancer.localServerCount=0
# Configure external servers
one.jpro.loadbalancer.externalServer1=http://server1.example.com:9101
one.jpro.loadbalancer.externalServer2=http://server2.example.com:9102
one.jpro.loadbalancer.externalServer3=http://server3.example.com:9103
one.jpro.loadbalancer.externalServer4=http://server4.example.com:9104
...
```

### Running your app with the loadbalancer

1. Create a new folder F and download the [JPro Loadbalancer](https://sandec.jfrog.io/artifactory/repo/one/jpro/jpro-loadbalancer/2025.3.3/jpro-loadbalancer-2025.3.3.jar) into it:
    ```shell
    curl -LO https://sandec.jfrog.io/artifactory/repo/one/jpro/jpro-loadbalancer/2025.3.3/jpro-loadbalancer-2025.3.3.jar
    ```
2. Create, or download from a template, a file named `application.properties` in the folder F. This file will be used to configure the JPro Loadbalancer.
3. Put the zip file created by the [JPro Release command](https://www.jpro.one/docs/current/2.1/JPRO_COMMANDS) into the folder F.
4. Start the JPro Loadbalancer:

```bash
java -jar <jpro-loadbalancer.jar>
```

### Enforce single Instance per JVM

With the JPro Loadbalancer you have the choice to set the ***maximum sessions to be accepted per JPro Server*** to 1. This ensures that your JPro Server never runs parallel sessions inside the same JVM.

Many apps, especially those initially built without web scaling in mind, may require this.

You can set this with the property `one.jpro.loadbalancer.sessionsPerServer = 1` in the [`application.properties`](http://application.properties) file.

## Configuration

### An application.properties example

The file `application.properties` might look like the following:

```
server.port=8080
one.jpro.loadbalancer.startPort=8100
one.jpro.loadbalancer.localServerCount=4
one.jpro.loadbalancer.sessionsPerServer=1
one.jpro.loadbalancer.warmedUpServers=1
one.jpro.loadbalancer.vmArguments=-Xmx500m
```

Use the following command to start the JPro Loadbalancer with the custom `application.properties`:

```bash
java -Dspring.config.location=file:/path/to/your/custom/application.properties -jar jpro-loadbalancer.jar
```

### Available Properties

The following parameters can be set in the `application.properties` file:

| Property | Default value | Description |
| --- | --- | --- |
| server.port | 8080 | The port used by the JPro Loadbalancer. |
| one.jpro.loadbalancer.zip | auto | The zip file containing the JPro Server. |
| one.jpro.loadbalancer.zipFolderName | auto | The folder of the zip file. |
| one.jpro.loadbalancer.vmFolder | vms | The folder which will contain the unzipped JPro Servers. |
| one.jpro.loadbalancer.startPort | 8100 | The first port used by the JPro Servers. |
| one.jpro.loadbalancer.localServerCount | 4 | The maximum amount of JPro Local servers to run in parallel. |
| one.jpro.loadbalancer.sessionsPerServer | 1 | The maximum amount of JPro sessions to run in parallel inside of one JPro Server. If `-1` is set, then virtually an unlimited number of sessions per server is allowed, limited only by the server CPU and memory resources. |
| one.jpro.loadbalancer.warmedUpServers | 1 | The number of JPro Servers to always be kept running, up and ready, before they are demanded. |
| one.jpro.loadbalancer.vmArguments | "" | A list of arguments provided to the JPro Server. They are split by ” ” and support escaping with “\” |
| one.jpro.loadbalancer.serverTimeoutTime | 60 | The server timeout is the time we wait to receive a response after sending a request |
| one.jpro.loadbalancer.maxMessageSize | 1000000 | The maximum size of a message in bytes. |
| one.jpro.loadbalancer.serverJavaHome | "" | The path to the Java home directory that will be used during the start of each local JPro Server. |
| one.jpro.loadbalancer.reuseUnzippedFolder | true | Control whether the JPro Loadbalancer should reuse the unzipped folder of the JPro Server. |
| one.jpro.loadbalancer.userHome | shared | The system user’s home directory is shared between JPro server instances. |
| one.jpro.loadbalancer.printEnvironment | false | Prints the environment values available for JPro Loadbalancer during startup. |
| one.jpro.loadbalancer.printConfig | false | Prints the configuration of the JPro Loadbalancer during startup. |
| one.jpro.loadbalancer.logToJsonFormat | false | Logs the structured messages in JSON format. |
| one.jpro.loadbalancer.parent.pid | "" | The PID of the parent process. When the parent process is stopped, the JPro Loadbalancer stops as well. |

### Configure `one.jpro.loadbalancer.userHome` property

The `one.jpro.loadbalancer.userHome` property controls how the user’s home directory is managed across JPro server instances. Below are the possible values and their descriptions:

| Value | Description |
| --- | --- |
| shared | The system user’s home directory is shared between JPro server instances. |
| shared:~/some/folder | The provided directory is shared between JPro server instances. The `~` can be used to reference the system user’s home directory. |
| isolated | The user’s home directory is isolated between JPro server instances. This is useful when each instance needs an empty user’s directory. |
| isolated:/some/file.zip | The user’s home directory is isolated between JPro server instances. The provided zip file content is extracted and used as an user’s home directory. |
| isolated:./some/folder | The user’s home directory is isolated between JPro server instances. The provided directory content is copied and used as an user’s home directory. |

Some example values for `one.jpro.loadbalancer.userHome` property;

```
one.jpro.loadbalancer.userHome = shared
one.jpro.loadbalancer.userHome = shared:~/some/folder
one.jpro.loadbalancer.userHome = shared:./some/folder
one.jpro.loadbalancer.userHome = isolated
one.jpro.loadbalancer.userHome = isolated:/some/file.zip
one.jpro.loadbalancer.userHome = isolated:./some/folder
```

### Logging properties

It is also possible to configure certain logging properties in the `application.properties`. For example:

```
logging.level.one.jpro.loadbalancer=debug
logging.level.root=debug
```

Because the JPro Loadbalancer is technically a simple [Spring Boot server](https://spring.io/projects/spring-boot), all the [configurations possible in Spring Boot](https://docs.spring.io/spring-boot/docs/3.2.x/reference/html/features.html#features.logging) can also be applied.

## Windows service

To use the [Windows service wrapper](https://github.com/winsw/winsw), we have to do 2 things as a preparation.
The steps happen in the same folder, which is used to place the application.conf and the jpro-loadbalancer jar.

First, download the WindowsServiceWrapper exe, and rename it to the name you want your service to have.
You can find the releases on its [GitHub Release page](https://github.com/winsw/winsw/releases).

```bash
curl -L --output myapp.exe https://github.com/winsw/winsw/releases/download/v2.12.0/WinSW-x64.exe
```

Second, create a configuration file and adapt it to your application.
Here is a template that you can use.

```
<service>
  <!--  ID of the service. It should be unique across the Windows system -->
  <id>myapp</id>
  <!--  Display name of the service  -->
  <name>MyApp Service (powered by WinSW)</name>
  <!--  Service description  -->
  <description>This service is a service created from a minimal configuration</description>
  <!--  Path to the executable, which should be started  -->
  <executable>java</executable>
  <arguments>-jar "%BASE%\jpro-loadbalancer<version>.jar"
  </arguments>
</service>
```

After you have created the configuration file and adapted it,
you can install the service:
`myapp.exe install`

Some other available commands are:
`myapp.exe uninstall`, `myapp.exe start`, `myapp.exe stop`, `myapp.exe restart`

For more details, take a look at the project homepage of [WinSW](https://github.com/winsw/winsw).

# QF-Test Integration
##  The JPro Integration Library - jpro-utils.qft

The **jpro-utils.qft** library enables QF-Test to run automated tests directly
against **JPro applications**, similar to testing standard desktop JavaFX apps.

It automatically:
- starts your JPro server,
- launches a browser containing your JPro UI,
- exposes it to QF-Test for automated testing.

---

### API Documentation

Full API documentation:  
**→ [[API Documentation](../../docs/jpro-utils_pkgdoc.html)]**

You can also read the package/procedure annotations directly in the `jpro-utils.qft` file.

---

### High-Level Overview

#### 1. `jpro.server` – Starting the JPro Server
QF-Test launches the JPro server (your JavaFX backend) and waits until it is ready.

- QF-Test calls this the **jproServer client**.
- Procedures are located under the **`jpro.server`** package.

#### 2. `jpro.client` – Launching the Browser
QF-Test starts a browser and loads your JPro application URL.

- QF-Test calls this the **jproClient client**.
- Procedures are located under the **`jpro.client`** package.

---

### Quickstart Guide

#### 1. Include the Library
Add `jpro-utils.qft` as an *Included file* (just like `qfs.qft`).

#### 2. (Optional) Add Conditional Execution
If your suite also tests non-JPro apps, wrap the JPro setup in a condition.

#### 3. Add the `jpro.running` Dependency
Attach the dependency to your Testcase or TestcaseSet and configure:

- **dir**  
  Folder from which the JPro run command is executed  
  (absolute or relative to your `.qft` file)

- **command**  
  Command that starts your JPro application  
  Example: `./gradlew jproRun`

- **serverAddress**  
  Address where the JPro server will run  
  Example: `http://localhost:8080`

- **browser**  
  Browser to open the JPro UI in  
  Example: `chrome`

---

### Writing Tests

Once the JPro server and browser client are running, write your tests as usual:
QF-Test will recognize windows, components, and UI structures of your JPro
application just like a normal JavaFX or web interface.%                                                                                                                            
