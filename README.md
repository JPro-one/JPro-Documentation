# GETTING STARTED


RUNNING JPRO LOCALLY
--------------------

### Using Gradle

The simplest way to begin is by using **Gradle** as your build tool.
JPro offers a plugin for Gradle that enables you to effortlessly launch JPro from an existing project.

JPro currently supports Gradle versions 4.x to 8.x. We recommend using version 8.x. Kotlin DSL is also supported.

For a straightforward reference project, consider exploring
the [HelloJPro-gradle](https://github.com/JPro-one/HelloJPro) example.
You can also [run it online](https://demos.jpro.one/helloworld.html).

Our public **ticket system** is available on [GitHub](https://github.com/JPro-one/JPro-Tickets).

[Here](https://github.com/JPro-one/JPro-Samples/) you can discover simple and helpful samples.

To get started and run your first app with JPro, complete the following **4 steps**:

1.  Install Gradle
2.  Create the Gradle script
3.  Create the JPro configuration file
4.  Run the app


#### Step `1`. Install Gradle

Gradle can be downloaded and installed [here](https://gradle.org/install/).


#### Step `2`. Create the Gradle scripts
Create the file `settings.gradle` and put it into your **project's root directory**.
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
    classpath "one.jpro:jpro-gradle-plugin:2024.4.0"
  }
}
```

Create the file `build.gradle` and put it into your **project's root directory**.
Then add the following configuration to the file:

```groovy
plugins {
  id 'org.openjfx.javafxplugin' version "0.1.0"
  id 'jpro-gradle-plugin'
}

version = "1.0-SNAPSHOT"
group = 'com.example'

compileJava {
  sourceCompatibility = 21
  targetCompatibility = 21
}

repositories {
  mavenCentral()
}

javafx {
  version = "23.0.1"
  modules = ['javafx.graphics', 'javafx.controls', 'javafx.fxml', 'javafx.media', 'javafx.web']
}

application {
  // Define the main class for the application.
  mainClassName = 'com.example.JavaFXApp'
}

jpro {
  // jpro server port
  port = 8080
}
```

#### Step `3`. Run the app

Start a **Terminal session**, move to the **main project directory** and enter the command:

```shell
./gradlew jproRun
```

Now you should see your app running inside your standard browser.



### Using Maven
JPro provides a plugin for Maven, which allows you to easily start JPro from an existing project,
which is obviously rather practical during the development process.

Currently, JPro Maven Plugin has been tested with versions `3.6.3`, `3.8.8`, `3.9.8` and `4.0.0-beta-3`.
We suggest to use the latest stable version **3.9.x**.

It is possible to configure the JPro server by passing arguments to a JPro related Maven goal via
`-Djpro.param=value`, where `param` is the name of the JPro related parameter and `value` is its value.

*Please note that if the parameter itself has already been configured via the JPro Maven Plugin inside the POM file,
the given `value` will **NOT** be taken in consideration.*

> As an example, to configure the `port` parameter before starting the server,
we can call the following command `mvn jpro:run -Djpro.port=9000`.

As a simple reference project, you could take a look at the simple
[HelloJPro-Maven](https://github.com/JPro-one/HelloJPro-Maven/)
and you can [run it online](https://demos.jpro.one/helloworld.html).

Our public **ticket system** can be found on [GitHub](https://github.com/JPro-one/JPro-Tickets).

To get started and run your first app with JPro, you should execute the following **3 steps**:

    * Install Maven
    * Create the Maven POM file
    * Add the JPro Maven plugin configuration section
    * Run the app 


#### Step `1`. Install Maven

Maven can be downloaded and installed [here](https://maven.apache.org/).


#### Step `2`. Create the Maven script

Create the file `pom.xml` and put it into your **project's root directory**.  
You can either download a template file [here](https://github.com/JPro-one/HelloJPro-Maven/blob/master/pom.xml) or just use the following:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.example</groupId>
  <artifactId>example-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>

  <properties>
    <jpro.version>2024.4.0</jpro.version>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <java.version>21</java.version>
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <maven.compiler.target>${java.version}</maven.compiler.target>
    <maven.compiler.release>${java.version}</maven.compiler.release>
    <javafx.version>23.0.1</javafx.version>
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
      <groupId>com.sandec.jpro</groupId>
      <artifactId>jpro-webapi</artifactId>
      <version>${jpro.version}</version>
      <scope>compile</scope>
    </dependency>
  </dependencies>
</project>
```

#### Step `3`. Run the app

Start a **Terminal session**, move to the **main project directory** and enter the command:

```groovy
mvn jpro:run
```

Now you should see your app running inside your standard browser.



## RUN JPRO REMOTELY


### Using Gradle

#### Step `1`. Prepare your server

To run JPro on linux, the server must be configured correctly.

Checkout the following chapters to configure your server correctly for JPro:

[DEPLOYING JPRO](/docs/current/2.6/DEPLOYING_JPRO)

[PREPARING LINUX FOR JPRO](/docs/current/2.7/PREPARING_LINUX_FOR_JPRO)

#### Step `2`. Create the binary

Create a zip which contains the application with the following command:
```shell
./gradlew jproRelease
```

The path of the zip-file is the following: `build/distributions/<app-name>-jpro.zip`

Now copy this file to your Server and unzip it.

#### Step `3`. Run JPro

In the unzipped folder you can find a start-script: `bin/start.sh`

By running `./bin/start.sh` you start the JPro Server on your server.

The JPro Server is now ready to serve your URLs entered in your browser.

```shell
./bin/start.sh
```


### Using Maven

#### Step `1`. Prepare your server

To run JPro on linux, the server must be configured correctly.

Checkout the following chapters to configure your server correctly for JPro:

[DEPLOYING JPRO](/docs/current/2.6/DEPLOYING_JPRO)

[PREPARING LINUX FOR JPRO](/docs/current/2.7/PREPARING_LINUX_FOR_JPRO)

#### Step `2`. Create the binary

Create a zip which contains the application with the following command:

```shell
mvn jpro:release
```

The path of the zip-file is the following: `target/<app-name>-jpro.zip`

Now copy this file to your Server and unzip it.

#### Step `3`. Run JPro

In the unzipped folder you can find a start-script: `bin/start.sh`

By running `./bin/start.sh` you start the JPro Server on your server.

The JPro Server is now ready to serve your URLs entered in your browser.

```shell
./bin/start.sh
```



## CREATE A PROJECT

The easiest way to set up a new JPro project for your apps is to use the **HelloJPro** project as your base,
for then to make some small adaptions to it.  This chapter will show you what you need to do if you
choose to go down that route. A bit later, you can decide whether you would use **Gradle or Maven** for your project.

As a start, take a look at your `index.html`, which can be downloaded
[here](https://github.com/JPro-one/HelloJPro/blob/master/src/main/resources/jpro/html/index.html)

### Starting an app from the index.html

The `index.html` file from the HelloJPro project looks like the following:

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
As you can see, the name of the app is provided in the tag `<jpro-app>`.

If your app is named `myApp`, then you need to modify the `<jpro-app>` as follows:

```html
<jpro-app href="/app/myApp" fullscreen="true"></jpro-app>
```
As a JPro session gets started, it will look for this app name inside the resource file called `jpro.conf`.

### jpro.conf

The `jpro.conf` of the HelloJPro project can be downloaded
[here](https://github.com/JPro-one/HelloJPro/blob/master/src/main/resources/jpro.conf).  It looks like the following:

```
jpro.applications {
    //jpro apps
    "hellojpro" = com.jpro.hellojpro.HelloJProFXML
}
```
In order to start an application from the `index.html` file, an entry for the name specified in the `<jpro-app>` tag
of `index.html` needs to be found in the `jpro.conf`.

Therefore, the line here needs to be modified to be

```
jpro.applications {
//jpro apps
  "myApp" = com.jpro.hellojpro.WhateverTheClassIsNamed
}
```
We would assume, in most cases the line would look like this:

```
jpro.applications {
//jpro apps
  "myApp" = com.jpro.hellojpro.MyApp
}
```

Now you are done and can run your `myApp`, by simply providing the command if you use Gradle:

```shell
./gradlew jproRun
```
or

```shell
gradle jproRun
```

and if you use Maven:

```shell
mvn jpro:run
```

from the **main project directory** in your terminal window.

See Step 4 of the
[RUN JPRO LOCALLY](/docs/current/1.1/RUN_JPRO_LOCALLY/Using_Gradle/) and
[JPRO GRADLE COMMANDS](/docs/current/2.1/JPRO_COMMANDS/Using_Gradle/)
for more details about how to run an app with `Gradle`.  
See Step 4 of the
[RUN JPRO LOCALLY](/docs/current/1.1/RUN_JPRO_LOCALLY/Using_Maven/) and
[JPRO MAVEN COMMANDS](/docs/current/2.1/JPRO_COMMANDS/Using_Maven/)
for more details about how to run an app with `Maven`.  See
[CONFIGURING JPRO](/docs/current/2.2/CONFIGURING_JPRO)
for more detailed information about `jpro.conf`.


### Starting an app from Gradle

1. The `settings.gradle` file of the HelloJPro project can be downloaded
   [here](https://github.com/JPro-one/HelloJPro/blob/main/settings.gradle). It looks like the following:

```groovy
buildscript {
  repositories {
    gradlePluginPortal()

    maven {
      url "https://sandec.jfrog.io/artifactory/repo"
    }
  }

  dependencies {
    classpath "one.jpro:jpro-gradle-plugin:$jproVersion"
  }
}
```

2. The `build.gradle` file of the HelloJPro project can be downloaded
   [here](https://github.com/JPro-one/HelloJPro/blob/master/build.gradle).  It looks like the following:

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

application {
  // Define the main class for the application.
  mainClassName = 'one.jpro.hellojpro.HelloJProFXML'
}

jpro {
  // jpro server port
  port = 8080
}
```

3. The `gradle.properties` file of the HelloJPro project holds all version strings can be downloaded
   [here](https://github.com/JPro-one/HelloJPro/blob/main/gradle.properties).  It looks like the following:

```properties
projectVersion = 1.0-SNAPSHOT
jproVersion = 2024.4.0
javafxPluginVersion = 0.1.0
javafxVersion = 23.0.1
```

If the JPro starter does not find any matching name in the `jpro.conf`, then it will look
for a specified `mainClassName` in the `build.gradle` to be started instead.


### Starting an app from Maven
The `pom.xml` file of the HelloJPro project can be downloaded
[here](https://github.com/JPro-one/HelloJPro-Maven/blob/master/pom.xml).  It looks like the following:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>one.jpro</groupId>
  <artifactId>hellojpro-maven</artifactId>
  <version>1.0-SNAPSHOT</version>
  <packaging>jar</packaging>

  <properties>
    <jpro.version>2024.4.0</jpro.version>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <java.version>21</java.version>
    <maven.compiler.source>${java.version}</maven.compiler.source>
    <maven.compiler.target>${java.version}</maven.compiler.target>
    <maven.compiler.release>${java.version}</maven.compiler.release>
    <javafx.version>23.0.1</javafx.version>
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
          <mainClassName>one.jpro.hellojpro.HelloJProFXML</mainClassName>
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
      <groupId>com.sandec.jpro</groupId>
      <artifactId>jpro-webapi</artifactId>
      <version>${jpro.version}</version>
      <scope>compile</scope>
    </dependency>
  </dependencies>
</project>
```

If the JPro starter does not find any matching name in the `jpro.conf`, then it will look
for a specified `<mainClassName>` in the `pom.xml` to be started instead.


## PC AS JPRO SERVER

After testing your app through localhost, a next practical step could be to make your PC host a JPro server
for external access.  This way you can make your current state of the app available for insight by people
located externally.  You can also see how the app behaves when it really uses a WLAN or the internet as
communication platform for your JPro server. To achieve this, follow these steps:

### Step `1`. Start JPro in localhost

Make sure the `index.html`, the `jpro.conf` and your tool specific file (either `gradle.build` or `pom.xml`)
are correctly setup to start your app. Check this by starting your JPro app as a normal app in your browser.  See
[RUN JPRO LOCALLY](/docs/current/1.1/RUN_JPRO_LOCALLY/) for more details.


### Step `2`. Start a local JPro server

Start the JPro server on your PC, to run in background, like this:

* for Gradle:
```shell
gradle jproRestart
```
* for Maven:
```shell
mvn jpro:restart
```

### Step `3`. Define the Port to be used for external access

Set up your in-house communication structure to support external access through one or more selected port numbers.


### Step `4`. Find out which IP address your PC is using

An easy way to find this out is to simply open the following URL from your browser:
```
https://www.iplocation.net/find-ip-address
```

### Step `5`. Access your JPro server from an external browser

Start the JPro app from an external browser, by using the URL:
```
<IP Address>:<Port Number>
```
Example:
```
2.206.149.6:8080
```
And, you are done!  You should now be able to use the app from your external device's browser.



## JPRO SCREENSHARING

Set up your app to be shared among external users.

### Step `1`. Setup your PC as a JPro server

Make sure everything is prepared for your PC to host a JPro server, as explained
[here](/docs/current/1.1/RUN_JPRO_LOCALLY).

### Step `2`. Setup for starting through the index.html

Modify the `index.html` to start your app with **screensharing**, simply by
adding an exclamation sign to your app specification in the `index.html`, like the following:
```
<jpro-app href="/app/myApp?singleton=true" fullscreen="true"></jpro-app>
```
and make sure you have specified the same app name in the `jpro.conf`, like the following:
```
jpro.applications {
  "myApp" = com.jpro.hellojpro.MyApp
}
```

### Step `3`. Let people participate from external browsers

Start the JPro app from a number of external browsers, all of them using the URL:
```
<IP Address>:<Port Number>
```
Example:
```
2.206.149.6:8080
```
You are done!  Now, everyone can participate to one and the same session of your app.



# JPRO DOCs


## JPRO COMMANDS

### Using Gradle
There are two ways of making Gradle accessible for your project:

* the files `gradlew` and `gradlew.bat` are parts of your project
  (see the [helloJPro example](https://github.com/JPro-one/HelloJPro))
* you have downloaded and installed gradle

The following ***JPro commands*** are supported by the `jpro-gradle-plugin`, to be started either from your IDE or
directly from your terminal(***):
* `gradle jproRun` **starts the currently specified application**(*) inside the browser.
  Before it starts the application it automatically **starts the JPro server**.
  The console output is visible in the console until the JPro server is closed (you can close the running app
  by typing `ctrl+c` in the terminal window).

* `gradle jproStart` **starts the JPro server** in the background(**).

* `gradle jproStop` **stops the JPro server** in the background.

* `gradle jproRestart` **restarts the JPro server**.  Should the JPro server already be running,
  it automatically gets stopped before restarted.

* `gradle jproRelease` **creates a zip-file**, which contains a build of the **current project**,
  including the dependencies for JPro and for the current project.
  It contains scripts for `start/stop/restart` of the ***deployed JPro servers***.
  The scripts are located in the *bin-folder*.

(*) the "currently specified application" is the `mainClassName` defined in the `build.gradle`.

(**) in this process we are dealing with a single JPro server, which is why no JPro server needs to be addressed
specifically.

(***) When you have installed Gradle, you can use the simple command prefix `gradle`, otherwise you must use `./gradlew`.  
In the list above, we assume you have installed gradle and therefore use `gradle`.

During development, when you iteratively check your last program changes etc., you basically do fine with
just using the `jproRun` command from your terminal window.  If required, it automatically starts your browser,
and opens a new tab with your app in it.  Which app to start is defined in the `mainClassName` of your `build.gradle`.

The browser's URL shows the `localhost` URL with whatever properties you have specified either
in your app or in your `build.gradle`.  You don't need to worry about starting a JPro server
etc., it is all handled by the `jproRun` command for you.

In a real world scenario, though, when your JPro server runs **remotely**, you will require the other commands,
like the `jproStart` etc.


### Using Maven

The following ***JPro commands*** are supported by the jpro-maven-plugin, to be started either from your IDE or
directly from your terminal:
* `mvn jpro:run` **starts the currently specified application**(*) inside the browser.
  Before it starts the application it automatically **starts the JPro server**.
  The console output is visible in the console until the JPro server is closed (you can close the running app
  by typing `ctrl+c` in the terminal window).

* `mvn jpro:start` **starts the JPro server** in the background(**).

* `mvn jpro:stop` **stops the JPro server** in the background.

* `mvn jpro:restart` **restarts the JPro server**.  Should the JPro server already be running,
  it automatically gets stopped before restarted.

* `mvn jpro:release` **creates a zip-file**, which contains a build of the **current project**,
  including the dependencies for JPro and for the current project.
  It contains scripts for `start/stop/restart` of the ***deployed JPro servers***.
  The scripts are located in the *bin-folder*.

(*) the "currently specified application" is the `mainClassName` defined in the `pom.xml`.

(**) in this process we are dealing with a single JPro server, which is why no JPro server needs to be addressed
specifically.

During development, when you iteratively check your last program changes, you basically do fine with
just using the `jproRun` command from your terminal window.  If required, it automatically starts your browser,
and opens a new tab with your app in it.  Which app to start is defined in the `mainClassName` of your `pom.xml`.

The browser's URL shows the `localhost` URL with whatever properties you have specified either
in your app or in your `pom.xml`.  You don't need to worry about starting a JPro server
etc., it is all handled by the `mvn jpro:run` command for you.

In a real world scenario, though, when your JPro server runs **remotely**, you will require the other commands,
like the `mvn jpro:start` etc.



## CONFIGURING JPRO

### build.gradle and pom.xml

The Gradle plugin is configured under the `jpro` tag of `build.gradle`.
The Maven plugin is configured under the `<plugin>` tag of `pom.xml`.  
The set of supported properties for Gradle and Maven are identical.

The following configuration properties are available:

| Property         | Default value                           | Description                                                                                                                                                                                                                                                                                                                                               |
|------------------|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| visible          | false                                   | If true, an additional window, beside the browser window, hosts the original javafx-application. This is for debugging, only. It impacts the performance negatively.                                                                                                                                                                                      |
| port             | 8080                                    | The port to which the server should listen.                                                                                                                                                                                                                                                                                                               |
| openURLOnStartup | true                                    | Tells JPro, whether the Browser should be opened after calling `jproRun`                                                                                                                                                                                                                                                                                  |
| openingPath      | "/"                                     | On `jproRun` the Browser is automatically opened. This variable defines the path of the opened URL.                                                                                                                                                                                                                                                       |
| useFontConfig    | false                                   | Tells the Server, whether the library fontconfig should be used to resolve fonts. It's deactivated by default to make sure, the font is always the same.                                                                                                                                                                                                  |
| useModuleSystem  | false                                   | When set to true, all dependencies are loaded as modules.                                                                                                                                                                                                                                                                                                 |
| useZGC           | true                                    | When set to true, the ZGC is used as the garbage collector.                                                                                                                                                                                                                                                                                               |
| jproVersion      | The version of the `jpro-gradle-plugin` | The JPro-version to be used.                                                                                                                                                                                                                                                                                                                              |
| javafxVersion    | "auto"                                  | Possible values are `auto`, `latest`, `15`, `14` and `11`.                                                                                                                                                                                                                                                                                                |
| JVMArgs          | []                                      | A list of arguments, which are used to run JPro.                                                                                                                                                                                                                                                                                                          |
| workingDir       |                                         | The working directory of the JPro application.                                                                                                                                                                                                                                                                                                            |
| verbose          | false                                   | If set to true, the start arguments of the JPro server are printed to the console.                                                                                                                                                                                                                                                                        |
| releaseName      |                                         | Sets the name of the zip generated by `jproRelease`. Also, `-jpro` postfix will be added to the resulting filename. If this property is not set, the project name will be used instead.                                                                                                                                                                   |
| releasePlatforms | ["current"]                             | Includes the binaries for the specified platforms in the release zip generated by `jproRelease`. Possible values are `linux`, `linux-aarch64`, `mac`, `mac-aarch64`, `win`. Default value is `current`, which means the current platform is included and can be used in combination with the others, otherwise use `all` as shortcut to include them all. |
| jproReleaseFiles | [:]                                     | A map of paths and files, which should be added to the zip, generated by `jproRelease`                                                                                                                                                                                                                                                                    |

On Gradle there is a configuration called `jproOnly` which is used to configure the dependencies which are only
used when running the application with JPro server.

```
................
dependencies {
  jproOnly "com.mycompany:some-library-jpro-implementation:1.0.0"
}
...............
```

#### A build.gradle example

Here an **example**:

```
jpro {
  visible = true                            // Enables for an extra JavaFX 
                                            // window to open beside the browser.
                                            // This might be helpful should there be 
                                            // differences in the rendering
                                            // between the browser and a native  
                                            // version of the app.
                                      
  port = 8083                               // The web-socket app to use.  

  jproVersion = "2024.4.0"  // The JPro version to use.  

  openURLOnStartup = false                  // This prevents the browser from opening 
                                            // when jproRun is called.    
                                              
  openingPath = "/fullscreen/"              // A prefix to use for the path in  
                                            // the Url for the browser.
                                      
  JVMArgs << '-Xmx3500m'                    // Lets set the memory for the JPro-Server
  
  // These two lines will add the file1.dat and file2.dat to the folder data in the zipfile.
  // The names of the files are changed to newname1.dat and newname2.dat.
  jproReleaseFiles << JProReleaseFile(new File("target/file1.dat"), "/data/newname1.dat")
  jproReleaseFiles << JProReleaseFile(new File("target/file2.dat"), "/data/newname2.dat")
  
  // The file is added to the folder named data, with the filename file3.dat.
  jproReleaseFiles << JProReleaseFile(new File("target/file3.dat"), "/data/")
}
```

#### A pom.xml example

See the previous chapter for more comments associated with the properties.

**NOTE**: Please note, that `mainClassName` is here set under the `<configuration>` tag, although,
for the gradle plugin it is not set where those other properties are set(under the `jpro` tag).

Here an **example**:

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

### jpro.conf

The following properties can be set in the `jpro.conf`:

| Property                               | Default value | Description                                                                                                                                                    |
|----------------------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| jpro.preventSystemExit                 | true          | Tells the JVM, to prevent calls to `java.lan.System.exit`.                                                                                                     |
| jpro.adminUsername                     | ""            | The username, to access logs, passwords etc.                                                                                                                   |
| jpro.adminPassword                     | ""            | The password, to access logs, passwords etc.                                                                                                                   |
| jpro.gcWorkaroundStage                 | true          | Activated a workaround for a memory leak in JavaFX when closing a stage.                                                                                       |
| jpro.logResourceAccess                 | false         | Log all access to resources under the path `jpro/html`.                                                                                                        |
| jpro.logUserInputEvents                | true          | Log all input events.                                                                                                                                          |
| jpro.logConsole                        | true          | Redirects the console output to the logging system.                                                                                                            |
| jpro.logToJUL                          | false         | Redirects the logging to the java.util.logging system.                                                                                                         |
| jpro.logToJsonFormat                   | false         | Logs the structured messages in JSON format.                                                                                                                   |
| jpro.logger.resource                   | ""            | Location of the new logging configuration accessed as a resource.                                                                                              |
| jpro.logger.file                       | ""            | Location of the new logging configuration accessed as a file.                                                                                                  |
| jpro.logger.url                        | ""            | Location of the new logging configuration accessed as a URL.                                                                                                   |
| jpro.onJVMStartup                      | null          | A string to a class, which should be executed during the startup of the JVM.                                                                                   |
| jpro.onFXStartup                       | null          | A string to a class, which should be executed during the startup of the application, on the JavaFX Application Thread, after the server has started.           |
| jpro.onJVMShutdown                     | null          | A string to a class, which should be executed during the shutdown of the JVM.                                                                                  |
| jpro.addInstanceID                     | false         | When true, all requests from the client, contain the current instance ID.                                                                                      |
| jpro.linkUnownedWindowsToFirstInstance | false         | When true, all unowned windows are linked to the first instance.                                                                                               |
| jpro.websocketMaxMessageSize           | 64kb          | The maximum size of websocket messages sent by JPro. Too big messages get split into multiples. Useful when somewhere is a limitation on the size of messages. |
| jpro.parent.pid                        | null          | The parent process id. When the parent process stops, the JPro server will also stop.                                                                          |

For example, The jpro.conf might look like the following to set up an admin login:
```
jpro.adminUsername = "admin"
jpro.adminPassword = "secret"
```

#### Declaring runnable applications

A jpro server is capable of running a set of different applications.
In the `jpro.conf` those **runnable applications** are declared, like in the following example:
```
jpro.applications {
  "appname1" = package.Application1
  "appname2" = package.Application2
}
```

As you can see, there are 2 ways in which you can declare which apps to be runnable and which app to actually
be started when you trigger a **starting option**.  The different options for starting an app in the browser are:

* using the `jproRun` or the `jpro:run` command (See [JPRO COMMANDS](/docs/current/2.1/JPRO_COMMANDS/))
* authoring a URL in the browser


A **typical localhost URL** looks like the following:

`https://localhost:8083/myApp`  or  `https://localhost:8083/fullscreen/myApp`


For an app to be **JPro enabled**, it must extend the class called `javafx.application.Application`.

After declaring an app as runnable in the `jpro.conf`, **it can be embedded into a webpage** by using the `<jpro-app>` tag
like follows:
```html
<jpro-app href="/app/appname1" />
```

### Changing the working directory after creating a release
We can change the working directory of a JPro application in different ways after creating a release by either calling
`jproRelease` in Gradle or `jpro:release` in Maven:
1. Define a `JPRO_WORKING_DIR` environment variable before starting the JPro server via the **start** script.
2. Via the `--working-dir` argument provided to the **start** script. Here is an example:
```shell
./start.sh --working-dir /path/to/working/dir
```

Go to the next chapter _**EMBEDDING JPRO**_ to see how to embed a runnable app into an existing webpage.


## EMBEDDING JPRO

JPro can be **embedded into an existing html-page** by using the tag `<jpro-app>`.
To activate the JPro-tag the following lines need to be introduced to the html-page:
```html
<link rel="stylesheet" type="text/css" href="/jpro/css/jpro.css">
<script src="/jpro/js/jpro.js" type="text/javascript"></script>
```

To embed JPro to your dom, you need to introduce to your html-file: `<jpro-app href="/app/default">`


### Supported attributes for the jpro-app tag

The jpro-app tag has a set of **attributes**, which can be set to control the jpro-app's behaviour:

| Attribute name             | Default value | Description                                                                                                                                                                            |
|----------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| href                       |               | The URL of the application to be started.  It is either the URL of the App's websocket connection `"wss://yourServer.com/app/myAppName"`, or it's the relative URL `"/app/myAppName"`. |
| loader                     |               | Defines whether or not to activate the loading animation for this JPro-app. Valid values are: `"default"` `"none"`                                                                     |
| loaderURL                  |               | Defines a gif file which can be used to replace the standard loader.                                                                                                                   |
| fullscreen                 | "false"       | When true, the JPro app is resized to the entire page. It also **sets autofocus** to true.                                                                                             |
| readonly                   | "false"       | When true, the user can NOT do any data authoring to the scene.                                                                                                                        |
| disableShadows             | "false"       | Disables all shadows in the JPro-renderer.  This might be useful, for rendering performance reasons.                                                                                   |
| disableEffects             | "false"       | Disables all effects in the JPro-renderer.  This might be useful, for rendering performance reasons.                                                                                   |
| disableClip                | "false"       | Disables all clips in the JPro-renderer. This is useful for debugging.                                                                                                                 |
| disablePointerCapture      | "false"       | Disables the usage of pointer capture to get the mouse events. This is useful for debugging.                                                                                           |
| disableVirtualKeyboard     | "false"       | Disables the virtual keyboard on mobile devices.                                                                                                                                       |
| autofocusEnabled           | "false"       | When true, the JPro-tag gets focused when the page is opened. This is useful for text-input, for example to enable the TextInput for a login-mask.                                     |
| nativescrolling            | "false"       | When true, the scroll events are managed by html. Otherwise they are managed by the JPro app.                                                                                          |
| nativezooming              | "false"       | When true, the zoom events are managed by html. Otherwise they are managed by the JPro app.                                                                                            |
| userSelect                 | "false"       | When true, the text selection is managed by html. Otherwise it is managed by the JPro app.                                                                                             |
| scale                      | "false"       | When true, the JPro app's scene is scaled to fit the html container. It works similar to `background-size: cover`in html.                                                              |
| stretch                    | "false"       | When true, the JPro app's scene is stretched to fit the html container.                                                                                                                |
| fxwidth                    | "false"       | When true, the width  of the JPro-tag is managed by the JPro app. Otherwise the width  is managed by html.                                                                             |
| fxheight                   | "false"       | When true, the height of the JPro-tag is managed by the JPro app. Otherwise the height is managed by html.                                                                             |
| fxContextMenu              | "true"        | When true, the context menu of the browser is suppressed and NOT shown. Is useful, when the JPro app itself has got a context-menu to show instead.                                    |
| setPrintJSCommands         | "false"       | When true, all js-commands executed through the WebAPI are logged on the browser console.                                                                                              |
| timeUntilReconnect         | "10000"       | It specifies after how much time, the client tries to reconnect, when he didn't hear anything from the server.                                                                         |
| snapshot                   | "auto"        | When set to true, the JPro app is rendered as a static image. On "auto" this only happens, when it's indexed and WebSocket is not available.                                           |
| rememberInstanceIDInCookie | "false"       | When set to true, only one instance of the app is created per browser.                                                                                                                 |
| syncStageAttributes        | "false"       | When set to true, the stage title and icons attributes are synchronized between the JPro app and the browser.                                                                          |

### Supported extra attributes

#### Node

Extra **attributes** are supported by calling `node.getProperties().put("attributeName", attributeValue)` in the JavaFX code
in order to control the browser behaviour for a specific node.

| Attribute name          | Default value | Description                                                                                                                                                                                                                                                                                 |
|-------------------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| translate               | true          | When false, disables the text translation from the browser. This is useful for example when we want to disable translation on a specified text-input control. The translation rule is inherited from the parent node.                                                                       |
| vkType                  | null          | Defines the virtual keyboard, used for a given `TextInputControl`. Check out [mdn web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) for possible values. Only values that change the virtual keyboard have an effect. Other values should not be used. | 

#### Window

The following **attributes** are supported by calling `window.getProperties().put("attributeName", attributeValue)` in the JavaFX code

| Attribute name | Default value | Description                                                                 |
|----------------|---------------|-----------------------------------------------------------------------------|
| jpro-hidden    | false         | When true, then the window is not rendered as part of it's owners instance. | 


### A web-page template

Here, **an example** (of course, to see an example, you could also just inspect the source of **this web-page**):

```html
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN"
        "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
<html lang="en">
<head>
    <meta charset="UTF-8">

    <title>this is a template</title>
    <link href="/myFavicon.png" rel="icon">

    <link rel="stylesheet" type="text/css" href="/jpro/css/jpro.css">
    <script src="/jpro/js/jpro.js" type="text/javascript"></script>

    <style>
    ...
</head>
<body>
<div>
    <jpro-app loader="none" href="/app/default" fullscreen="true" />
</div>
</body>
</html>
```


### Make Resources accessible as URLs

In order to **make resources publicly available as URLs**, you just need to understand and follow
some **simple conventions** defined for the jpro servers.  Because of those conventions, you are freed from
the burden of using separate web servers for your resources, be it images, html-files or any
other thinkable resource.

Any resource underneath the package `jpro/html` are publicly available through the jpro-server as a URL.
Another practical convention is that, when a file is named `index.html` the filename itself is redundant and
can therefore simply be skipped for the URL.

The following examples should explain well what is meant:

The JPro server can be reached with the url `http://localhost:8080`,

`jpro/html/myImage.jpg` with `http://localhost:8080/myImage.jpg`,

`jpro/html/folder/myImage.jpg` with `http://localhost:8080/folder/myImage.jpg` and

`jpro/html/index.html` with `http://localhost:8080/index.html` or

`jpro/html/index.html` with `http://localhost:8080/`.


### Publishing JPro applications

To make your JPro applications accessible via URL, you should create an “index.html” and place
it into `/jpro/html/index.html` or in the project structure under `src/main/resources/jpro/html/index.html`.
As mentioned in the last chapter, all files to be accessible via URL, be it HTML files, images, documents or others,
should be placed in the classpath on `/jpro/html`.


## THE WEBAPI
The main purpose of the WebAPI is to let you create individual Javascript code for the browser,
which can interoperate with JPro.  This means, should you want to bind your browser app to existing Javascript code,
then the WebAPI comes to play.  But, in addition, it offers some general methods, which you will find
useful when creating cross-platform solutions.

The following features are currently available:

* Detecting your current running platform, like `com.jpro.web.WebAPI.isBrowser`
* Information about your current **session**, **language** used, **cookies**, the current **URL**, etc.
* Bridges for **bidirectional communication** between client-side Javascript/browser code and server-based java code.
* You can **interchange data**, do **remote calling**, registering remote functions calls, to be used between   
  the client-side Javascript/browser and your server-based java code, and vice versa.

There are two ways to get access to the WebAPI:

* let your app `extend JProApplication` and call `getWebAPI()`, or
* call `WebAPI.getWebAPI(javafx.scene.Scene scene)` or
* call `WebAPI.getWebAPI(javafx.stage.Window window)`.

For exact details about the API itself, please go to the [WebAPI-documentation](/api/2024.4.0/jpro.webapi/com/jpro/webapi/WebAPI.html).


### Using the WebAPI without JPro
#### Using Gradle
The WebAPI can be imported as a jar, also when not using JPro. It can be introduced to the `build.gradle` by
the following statement:

```
dependencies {
    ...
    implementation "com.sandec.jpro:jpro-webapi:2024.4.0"
    ...
}
```

#### Using Maven
The WebAPI can be imported as a jar, also when not using JPro. It can be introduced to the `build.gradle` by
the following statement:

```xml
<dependencies>
    ...
    <dependency>
        <groupId>com.sandec.jpro</groupId>
        <artifactId>jpro-webapi</artifactId>
        <version>${jproVersion}</version>
        <scope>compile</scope>
    </dependency>
    ...
</dependencies>
```

#### Getting WebAPI as a Jar
You can download the WebAPI from our [repository](https://sandec.jfrog.io/ui/native/repo/com/sandec/jpro/jpro-webapi/).
This can be useful when you are using neither Maven nor Gradle.
Here is the [download link](https://sandec.jfrog.io/artifactory/repo/com/sandec/jpro/jpro-webapi/2024.4.0/jpro-webapi-2024.4.0.jar) for the latest version.


## DEBUGGING AND TESTING
The following tags can be added to the original URL of your JPro server.  
The JPro server responds to those tags in different ways, and thereby allows for system administrators and
developers to acquire useful information during runtime.

A `username` and `passwort` for the URLs (or pages) can be configured in the `jpro.conf`.
In production, the URLs (or pages) are only accessible, when a password is configured.

| url                            | content                                                                                                                                                          |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /status                        | Returns a page with some statistics about the running server.                                                                                                    |
| /status/alive                  | Asks the running server whether it's alive and ok., When the javafx-thread is not being blocked and running normally, the server responds with the word "alive". |
| /info/log/console.log          | Returns a log-file with all the console-output of the application. The logging of the console-output can be deactivated in the `jpro.conf`.                      |
| /info/log/info.log             | Returns a log-file with all the info-logs in the jpro-server.                                                                                                    |
| /info/log/warning.log          | Returns a log-file with all the warning-logs in the jpro-server.                                                                                                 |
| /info/log/error.log            | Returns a log-file with all the error-logs in the jpro-server.                                                                                                   |
| /info/log/activity.log         | Returns a log-file with all the activity-logs in the jpro-server.                                                                                                |
| /info/all.zip                  | Returns all files in the log-folder as a zip-file.                                                                                                               |
| /info/fxstack                  | Returns the whole stack-trace of the javafx-thread. Useful for debugging blocked javafx-threads.                                                                 |
| /info/minmemory                | Returns the memory-usage of the jvm, after running the garbage-collector.                                                                                        |
| /test/<appname>                | Creates a simple test-page, which opens the provided application.                                                                                                |
| /test/fullscreen/<appname>     | Creates a simple test-page, which opens the provided application in fullscreen.                                                                                  |
| /test/scrolling/<appname>      | Creates a simple test-page, which opens the provided application as natively scrollable.                                                                         |
| /info/heapdumps/heapdump.hprof | Downloads the heapdump of the server. Useful for finding memory-leaks with tools liks [VisualVM](https://visualvm.github.io/)                                    |
| /jpro/api/instances            | A list of all currently open instances.                                                                                                                          |

Here is an example of a command sent to a running JPro server called **https://www.jpro.one/status** (which is password protected)
which returns the following information about the JPro server:

```json
{
  "Start time" : "Sun Mar 17 21:12:03 CET 2019",
  "Time running" : "00:01:41.310",
  "Views created" : 2,
  "Views active" : 2,
  "Views afk" : 1,
  "Framerate" : 1,
  "Windows open" : 2,
  "Mediaplayers open" : 0,
  "Max memory" : "3641 mB",
  "Used memory(heap)" : "3.30%",
  "Used memory(non-heap)" : "56 mB",
  "Committed memory(non-heap)" : "59 mB",
  "JavaFX thread CPU usage" : "5.21%",
  "Java version" : "1.8.0_192",
  "JPro version" : "2018.1.12",
  "Latest JPro GIT commit" : "63f21b3c1fb79f82454462b654192efa15bd9a38",
  "Mode" : "dev",
  "Deployment" : "MAVEN-Normal",
  "Free system memory" : "31 mB",
  "Total system memory" : "16384 mB",
  "Free disk space" : "22669 mB",
  "Total disk space" : "239172 mB",
  "Default Java encoding" : "UTF-8",
  "Default Java local" : "en_DE",
  "Default Java timezone" : "Central European Time",
  "Open instances" : [ "hellojpro", "hellojpro" ]
}
```

Here are some useful commandline-tools if the server no longer responds:
```shell
jstack `cat RUNNING_PID`
jcmd  `cat RUNNING_PID` GC.heap_info
jmap -dump:format=b,file=heapdump.hprof `cat RUNNING_PID`
```


## DEPLOYING JPRO

### Deployment Requirements
Basically, JPro servers can run on any server with a JVM on it.  But, fact is, so far all our real world projects
are using Linux for the backend and therefore also for JPro.  For development purposes, we are mostly running our
JPro servers on macOS or Windows. Our recommended platform for the JPro servers at time being is
[Ubuntu 20.04](https://releases.ubuntu.com/20.04/). Other requirements are:

* JavaFX requires some libraries to run in a headless environment.
  Installing GTK and X11 is usually enough to run JavaFX.

* For production, it is highly recommended to use SSL.
  Why is this important?
  Because, some time proxies manipulate the traffic stream, and this would otherwise break the support of websockets.

## PREPARING LINUX/DOCKER FOR JPRO

### All linux versions
Install Java17 or Java21 on your linux server. We recommend using [Temurin 21](https://adoptium.net/temurin/releases/):

You can use the following Docker Script as a reference.
Most other linux distributions can be configured in a similar way.

All Linux distributions also work with ARM64.

#### Ubuntu 24.04
(22.04 and 20.04 also work)
```
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

#### Debian Bookworm
```
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

#### Fedora 39
```
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


## Apache2
We usually recommend using Nginx, but JPro can also be used with Apache as a webserver.
In this case, Apache is used as a Reverse Proxy, to forward the request from port 80/443 to the port of the JPro server.
To use Apache with JPro you have to install various plugins:

```shell
sudo a2enmod proxy proxy_http rewrite ssl proxy_wstunnel
```

Afterward, you can configure your webpage.
For example, it can be configured in the following file: `/etc/apache2/sites-enabled/000-default.conf`

```apacheconf
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

### Configure SSL
To configure the SSL we recommend the following tutorial for [Let's encrypt / Certbot](https://certbot.eff.org/)


## SSL by using NGINX

The setup defined below is tested with the nginx package contained in ubuntu 16.04.
In order to configure nginx for JPro, create the file `/etc/nginx/sites-enabled/jproconf.nginx.conf`

with the following content:
```
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

The following procedure can be used to help creating the file:

In order to configure the domain the way a JPro server needs it, please create the following file
(replace `yourdomain` with the real name): `/etc/nginx/sites-enabled/yourdomain_com.nginx.conf`

```
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

You can verify your configuration with the following command: `sudo nginx -t`



## JPro Close Instance Strategy Configuration

This documentation describes the JPro Close Instance Strategy configuration structure and explains each field in the configuration.
The configuration can be done in the `jpro.conf` file.

### Configuration Structure

The configuration is structured into three optional strategies: `short`, `medium`, and `long`. Each strategy contains the following properties:

- `until`: This property defines, until which duration the strategy is used. It must be not set, for the last strategy.
- `closeOnTabCloseAfter`: The second after which the instance will close if the tab is closed. -1 means it will not close after tab close.
- `closeOnDisconnectAfter`: The second after which the instance will close if a disconnect is detected. -1 means it will not close after disconnect.
- `closeOnAFKAfter`: The second after which the instance will close if a user is detected to be AFK (Away From Keyboard). -1 means it will not close after AFK.
- `closeOnBackgroundAfter`: The second after which the instance will close if the application goes to the background. -1 means it will not close after going to the background.

Here is the current default configuration:

```
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

## LOGGING

### Customizing Logback Configuration for JPro

To override the default JPro logging configuration, simply provide a new `logback.xml` file and specify its path
in the `jpro.conf` file using one of the following options:

1. `jpro.logger.resource` - to access the file as a resource in the classpath
2. `jpro.logger.file` - to access the file as an external file
3. `jpro.logger.url` - to access the file as a URL

Please be aware that if the new configuration includes a `console` output, you have two options to address this:

1. Disable the `jpro.logConsole` option by setting its value to `false`.
2. Set the `additivity` attribute for your `Console` logger to `false` as shown below:

```xml
<logger name="Console" additivity="false"/>
```

### Structured Logging

JPro provides a set of log messages, for which we guarantee stability.
If these log messages changed, these changes would be listed in the Changelog,
and this is only allowed to happen for a major release. But we might add additional information to the message.

| Log message      | Description               | Parameters                                                                                     |
|------------------|---------------------------|------------------------------------------------------------------------------------------------|
| Instance created | A new instance is created | app name, host name, instance id, browser, browser address, client address                     |
| Instance closed  | An instance is closed     | app name, host name, instance id, browser, browser address, client address, reason for closure |
| View created     | A new view is created     | app name, host name, instance id, browser, browser address, client address                     |
| View closed      | A view is closed          | app name, host name, instance id, browser, browser address, client address, reason for closure |
| Server started   | A server is started       | start time, operating system, jpro version                                                     |
| Server stopped   | A server is stopped       | running time, instances count, views count, operating system, jpro version, reason for stop    |

NOTE: Enabling the option `jpro.logToJsonFormat` in the `jpro.conf` file will cause these structured log messages to be
written in JSON format. This option is disabled by default. The following table gives a description of each parameter:

| Parameter          | JSON key        | Description                                                   |
|--------------------|-----------------|---------------------------------------------------------------|
| source             | source          | The source of the log message                                 |
| event              | event           | The event being logged                                        |
| app name           | app_name        | The name of the application                                   |
| host name          | host_name       | The name of the host                                          |
| instance id        | instance_id     | The ID of the instance                                        |
| browser            | browser         | The name of the browser used by the client                    |
| browser url        | browser_url     | The URL displayed on the client's browser                     |
| client address     | client_ip       | The ip address of the client                                  |
| start time         | start_time      | The time when the server was started                          |
| running time       | running_time    | The time when the server was stopped                          |
| instances count    | instances_count | The number of instances running on the server                 |
| views count        | views_count     | The number of views running on the server                     |
| operating system   | os_name         | The name operating system of the server                       |
| jpro version       | jpro_version    | The version of JPro running on the server                     |
| reason for closure | reason          | The reason why the instance/view/server was closed or stopped |


## PERFORMANCE TIPS

There are some things that can be done to improve the performance for JPro.
* Avoid shadow effects. They require quite long to be rendered correctly.
* Minimize the number of nodes that are used to represent the scenegraph.
* Try to reuse existing Nodes instead of creating new instances.
  The controls TableView and ListView are good examples for reusing existing Nodes.

## JPRO CHECKLIST
When using JPro, please be aware of the following important aspects:
* Your app **must NOT block** the javafx-thread.  Wait-, sleep-commands, showAndWaits in the javafx-thread are no-nos.
* Be careful when using **dialog boxes**. Make sure they don't use showAndWait (see above).
  [Here](https://github.com/JPro-one/JPro-Samples/tree/master/popups) you can see how to create a JPro agnostic popup.
  You can also use [this popup](http://www.jfoenix.com/documentation.html#Dialog) from the JFoenix library.
* Be careful with **statics**, because they would be shared between multiple instances
  (interesting enough, there are use cases in which this fact can be utilized as a very useful feature.
  But, it is important not to use them in the wrong way.)
* You can open **Stages** with the method `openStageAsPopup(Stage stage)` and `openStageAsTab(Stage stage)` of the
  [WebAPI](/api/2024.4.0/jpro.webapi/com/jpro/webapi/WebAPI.html).
  An alternative is, to create new windows or dialogues by using a StackPane at the root of your application.
  We have an example about popups in our [sample-project](https://github.com/JPro-one/JPro-Samples/tree/master/popups).
* The class WebView only works very limited with JPro.
  It should be replaced with `com.jpro.webapi.HTMLView`.
  [This sample ](https://github.com/JPro-one/JPro-Samples/tree/master/html-jpro) shows how to use
  the **HTMLView**.
* JPro currently requires at Least Java(FX) 11 or newer.
* JPro requires a JRE without JavaFX. This is the standard since Java11.
  Most JDK Vendors, which bundle JavaFX, also provide a version without JavaFX.

### Not yet supported JavaFX features
(this list refers to version 2024.4.0)
* MediaPlayer is now supported via the [JPro Media](https://github.com/JPro-one/jpro-platform/tree/main/jpro-media) module.
* The following Effect classes
  * Blend
  * Bloom
  * BoxBlur
  * ColorInput
  * DisplacementMap
  * Glow
  * ImageInput
  * Lighting
  * MotionBlur
  * PerspectiveTransform
  * Reflection
  * Shadow (is supported, but might be slow)
* JavaFX3D
* SwingNode
* FileChooser alternative is provided via the [JPro File](https://github.com/JPro-one/jpro-platform/tree/main/jpro-file) module.
* Clipboard
* [Dialog](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/Dialog.html) (check out our checklist
  above for alternatives.)
* WebView (Supported in its basic form, only. We recommend to use the
  [HTMLView](/api/2024.4.0/jpro.webapi/com/jpro/webapi/HTMLView.html), instead.)


# FAQ
## FAQ
```
I'm using a lot of java libraries in my app, like ControlsFX. Do they work in combination with jpro?
```
* JPro works well with any java library.

```
Does JPro work on mobile browser?
```
* JPro works very well on **mobile browsers**.

```
Does JPro work in combination with Gluon?
```
* JPro works without any problem with the [javafxmobile-plugin](https://bitbucket.org/javafxports/javafxmobile-plugin).
  But it currently doesn't work with the Charm library, specifically when the class
  [MobileApplication](https://docs.gluonhq.com/charm/javadoc/4.3.3/com/gluonhq/charm/glisten/application/MobileApplication.html) is used.

```
Does the ScenicView work in combination with JPro?
```
* Yes, the [ScenicView](https://github.com/JonathanGiles/scenic-view) works without any problems.

```
How do I handle browser specific differences?
```
* JPro handles most of the browser specifics internally and relieves the developer from those topics.
  NOTE: the code you write in javascript, obviously does not benefit from this.

```
The first Instance of my application starts fine, but as soon as the second instance is started, strange things happen. What can be the cause?
```
* It's most likely related to the use of static variables. In JPro, static variables are shared between multiple sessions.
  Therefore, variables declared as static become global to all sessions. This fact can cause problems. BUT, depending on
  how you use it, it can also be utilized as a welcomed feature.

```
My application slows down over time. After a while it some times even crashes. What could be the reason for such a behaviour?
```
* A common reason for this behaviour is a memory leak in your application.
  You can use tools like [VisualVM](https://visualvm.github.io/) to solve the issue in your application.

```
How can I use a IDE for my JPro-project?
```
The HelloWorld-Project is a simple gradle/java project, which can be imported by intellij or eclipse without any modifications.

# SUPPORT

## SUPPORT

Feel free to contact us at `info@jpro.one` for commercial support or any other related topic.

## What if I find bugs?

Should you find bugs in jpro, please inform us about any details through our
[jpro bug-tracker](https://github.com/JPro-one/jpro-issues).


# Links

## [JPro Platform](https://github.com/JPro-one/JPro-Platform)

## [JPro Samples](https://github.com/JPro-one/JPro-Samples/)

## [JPro Tickets](https://github.com/JPro-one/JPro-Tickets)

## [JavaFX](https://openjfx.io/)

## [JavaFX Version 21 API](https://openjfx.io/javadoc/21/index.html)

## [JavaFX Version 17 API](https://openjfx.io/javadoc/17/index.html)

## [JavaFX Version 11 API](https://openjfx.io/javadoc/11/index.html)

## Related projects

* [QF-Test](https://www.qfs.de/en/product/qf-test/java-testing/javafx.html) A commercial tool to test your JavaFX/JPro Application.
* [ControlsFX](https://github.com/controlsfx/controlsfx), a community library managed by
  [Jonathan Giles](https://jonathangiles.net/) and
  [Gluon](https://gluonhq.com/), with a set of controls. In 2017, it received the
  [Duke Choice Award](https://www.oracle.com/java/2017-dukes-choice-awards.html) for its awesome work.
* [Gluon's](https://gluonhq.com/) useful Java technologies, including the [Gluon Mobile](https://gluonhq.com/products/mobile/) library.
* [Dirk Lemmermann's](https://dlsc.com/) powerful projects:
  * [CalendarFX](https://dlsc.com/products/calendarfx/).
  * [PreferencesFX](https://github.com/dlemmermann/PreferencesFX).
  * [FormsFX](https://github.com/dlemmermann/FormsFX).
  * [FlexGanttFX](https://dlsc.com/products/flexganttfx/).
  * [WorkbenchFX](https://github.com/dlsc-software-consulting-gmbh/WorkbenchFX).
  * [PickerFX](https://github.com/dlsc-software-consulting-gmbh/PickerFX).
  * [GemsFX](https://github.com/dlsc-software-consulting-gmbh/GemsFX).
  * [UnitFX](https://github.com/dlsc-software-consulting-gmbh/UnitFX).
* [Harmonic Code](https://harmoniccode.blogspot.com/) is
  an impressive and dynamic blog from the Java Champion [Gerrit Grunwald](https://twitter.com/hansolo_?lang=de),
  which describes his cool components libraries.

A JPro **hello-world** project can be found [here](https://github.com/JPro-one/HelloJPro).

## [Curated JavaFX links](https://github.com/mhrimaz/AwesomeJavaFX#libraries-tools-and-projects)

## Blogs & Tutorials

* The JavaFX Champion und JavaOne Rockstar [Dirk Lemmermann](https://dlsc.com/blog/)'s interesting blog.
* [ScenicView](https://github.com/JonathanGiles/scenic-view) represents a very useful debugging tool for UI development.
* [Official JavaFX tutorials](https://docs.oracle.com/javafx/2/get_started/jfxpub-get_started.htm) from Oracle.
* Jakob Jenkov's many well written [JavaFX tutorials](http://tutorials.jenkov.com/javafx/index.html).
* [TutorialsPoint](https://www.tutorialspoint.com/javafx/index.htm).
* [Almas Baimagambetov](https://almasb.github.io/) [on GitHub](https://github.com/AlmasB), with cool games, tutorials and examples.
