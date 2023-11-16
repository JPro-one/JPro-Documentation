# GETTING STARTED

RUN JPRO LOCALLY
--------------------

### Using Gradle

The simplest way to begin is by using **Gradle** as your build tool.
JPro offers a plugin for Gradle that enables you to effortlessly launch JPro from an existing project.

JPro currently supports Gradle versions 4.x to 8.x. We recommend using version 8.x. Kotlin DSL is also supported.

For a straightforward reference project, consider exploring
the [HelloJPro-gradle](https://github.com/JPro-one/HelloJPro) example.
You can also [run it online](https://demos.jpro.one/helloworld.html).

Our public **ticket system** is available on [GitHub](https://github.com/JPro-one/JPro-tickets).

[Here](https://github.com/JPro-one/JPro-Samples/) you can discover simple and helpful samples.

To get started and run your first app with JPro, complete the following **4 steps**:

1. Install Gradle
2. Create the Gradle script
3. Create the JPro configuration file
4. Run the app

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
        classpath "one.jpro:jpro-gradle-plugin:2023.3.1"
    }
}
```

Create the file `build.gradle` and put it into your **project's root directory**.
Then add the following configuration to the file:

```groovy
plugins {
    id 'org.openjfx.javafxplugin' version '0.1.0'
    id 'jpro-gradle-plugin'
}

version = '1.0-SNAPSHOT'
group = 'com.example'

compileJava {
    sourceCompatibility = 17
    targetCompatibility = 17
}

repositories {
    mavenCentral()
}

javafx {
    version = '21.0.1'
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

Currently, JPro Maven Plugin has been tested with versions `3.6.3`, `3.8.8`, `3.9.5` and `4.0.0-alpha-8`.
We suggest to use the latest stable version **3.9.x**.

It is possible to configure the JPro server by passing arguments to a JPro related Maven goal via
`-Djpro.param=value`, where `param` is the name of the JPro related parameter and `value` is its value.

*Please note that if the parameter itself has already been configured via the JPro Maven Plugin inside the POM file,
the given `value` will **NOT** be taken in consideration.*

> As an example, to configure the `port` parameter before starting the server,
> we can call the following command `mvn jpro:run -Djpro.port=9000`.

As a simple reference project, you could take a look at the
simple [HelloJPro-Maven](https://github.com/JPro-one/HelloJPro-Maven/)
and you can [run it online](https://demos.jpro.one/helloworld.html).

Our public **ticket system** can be found on [GitHub](https://github.com/JPro-one/JPro-tickets).

To get started and run your first app with JPro, you should execute the following **3 steps**:

    * Install Maven
    * Create the Maven POM file
    * Add the JPro Maven plugin configuration section
    * Run the app 

#### Step `1`. Install Maven

Maven can be downloaded and installed [here](https://maven.apache.org).

#### Step `2`. Create the Maven script

Create the file `pom.xml` and put it into your **project's root directory**.  
You can either download a template file [here](https://github.com/JPro-one/HelloJPro-Maven/blob/master/pom.xml) or just
use the following:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>example-maven</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <properties>
        <jpro.version>2023.3.1</jpro.version>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <java.version>17</java.version>
        <maven.compiler.source>${java.version}</maven.compiler.source>
        <maven.compiler.target>${java.version}</maven.compiler.target>
        <maven.compiler.release>${java.version}</maven.compiler.release>
        <javafx.version>17.0.9</javafx.version>
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

```shell
mvn jpro:run
```

Now you should see your app running inside your standard browser.

## RUN JPRO REMOTELY

### Using Gradle

#### Step `1`. Prepare your server

To run JPro on linux, the server must be configured correctly.

Checkout the following chapters to configure your server correctly for JPro:

[DEPLOYING JPRO](#deploying-jpro)

[PREPARING LINUX FOR JPRO](#preparing-linux-for-jpro)

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

[DEPLOYING JPRO](#deploying-jpro)

[PREPARING LINUX FOR JPRO](#preparing-linux-for-jpro)

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
for then to make some small adaptions to it. This chapter will show you what you need to do if you
choose to go down that route. A bit later, you can decide whether you would use **Gradle or Maven** for your project.

As a start, take a look at your `index.html`, which can be downloaded
[here](https://github.com/JPro-one/HelloJPro/blob/master/src/main/resources/jpro/html/index.html)

### Starting an app from the index.html

The `index.html` file from the HelloJPro project looks like the following:

```
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

```
<jpro-app href="/app/myApp" fullscreen="true"></jpro-app>
```

As a JPro session gets started, it will look for this app name inside the resource file called `jpro.conf`.

### jpro.conf

The `jpro.conf` of the HelloJPro project can be downloaded
[here](https://github.com/JPro-one/HelloJPro/blob/master/src/main/resources/jpro.conf). It looks like the following:

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
[RUN JPRO LOCALLY](#using-gradle) and
[JPRO GRADLE COMMANDS](#using-gradle-2)
for more details about how to run an app with `Gradle`.  
See Step 4 of the
[RUN JPRO LOCALLY](#using-maven) and
[JPRO MAVEN COMMANDS](#using-maven-2)
for more details about how to run an app with `Maven`. See
[CONFIGURING JPRO](#configuring-jpro)
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
   [here](https://github.com/JPro-one/HelloJPro/blob/master/build.gradle). It looks like the following:

```groovy
plugins {
    id 'org.openjfx.javafxplugin' version "$javafxPluginVersion"
    id 'jpro-gradle-plugin'
}

version = "$projectVersion"
group = 'one.jpro'

compileJava {
    sourceCompatibility = 17
    targetCompatibility = 17
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
   [here](https://github.com/JPro-one/HelloJPro/blob/main/gradle.properties). It looks like the following:

```properties
projectVersion=1.0-SNAPSHOT
jproVersion=2023.3.1
javafxPluginVersion=0.1.0
javafxVersion=17.0.9
```

If the JPro starter does not find any matching name in the `jpro.conf`, then it will look
for a specified `mainClassName` in the `build.gradle` to be started instead.

### Starting an app from pom.xml (Maven)

The `pom.xml` file of the HelloJPro project can be downloaded
[here](https://github.com/JPro-one/HelloJPro-Maven/blob/master/pom.xml). It looks like the following:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>one.jpro</groupId>
    <artifactId>hellojpro-maven</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <properties>
        <jpro.version>2023.3.1</jpro.version>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <java.version>17</java.version>
        <maven.compiler.source>${java.version}</maven.compiler.source>
        <maven.compiler.target>${java.version}</maven.compiler.target>
        <maven.compiler.release>${java.version}</maven.compiler.release>
        <javafx.version>17.0.9</javafx.version>
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
for external access. This way you can make your current state of the app available for insight by people
located externally. You can also see how the app behaves when it really uses a WLAN or the internet as
communication platform for your JPro server. To achieve this, follow these steps:

### Step `1`. Start JPro in localhost

Make sure the `index.html`, the `jpro.conf` and your tool specific file (either `gradle.build` or `pom.xml`)
are correctly setup to start your app. Check this by starting your JPro app as a normal app in your browser. See
[RUN JPRO LOCALLY](#run-jpro-locally) for more details.

### Step `2`. Start a local JPro server

Start the JPro server on your PC, to run in background, like this:

, for Gradle:

```
gradle jproRestart
```

, for Maven:

```
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
[here](#run-jpro-locally).

### Step `2`. Setup for starting through the index.html

Modify the `index.html` to start your app with **screensharing**, simply by
adding an exclamation sign to your app specification in the `index.html`, like the following:

```
<jpro-app href="/app/!myApp" fullscreen="true"></jpro-app>
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
  (see the [HelloJPro example](https://github.com/JPro-one/HelloJPro))
* you have downloaded and installed gradle

The following ***JPro commands*** are supported by the `jpro-gradle-plugin`, to be started either from your IDE or
directly from your terminal(***):

* `gradle jproRun` **starts the currently specified application**(*) inside the browser.
  Before it starts the application it automatically **starts the JPro server**.
  The console output is visible in the console until the JPro server is closed (you can close the running app
  by typing `ctrl+c` in the terminal window).

* `gradle jproStart` **starts the JPro server** in the background(**).

* `gradle jproStop` **stops the JPro server** in the background.

* `gradle jproRestart` **restarts the JPro server**. Should the JPro server already be running,
  it automatically gets stopped before restarted.

* `gradle jproRelease` **creates a zip-file**, which contains a build of the **current project**,
  including the dependencies for JPro and for the current project.
  It contains scripts for `start/stop/restart` of the ***deployed JPro servers***.
  The scripts are located in the *bin-folder*.

(*) the "currently specified application" is the `mainClassName` defined in the `build.gradle`.

(**) in this process we are dealing with a single JPro server, which is why no JPro server needs to be addressed
specifically.

(***) When you have installed Gradle, you can use the simple command prefix `gradle`, otherwise you must
use `./gradlew`.  
In the list above, we assume you have installed gradle and therefore use `gradle`.

During development, when you iteratively check your last program changes etc., you basically do fine with
just using the `jproRun` command from your terminal window. If required, it automatically starts your browser,
and opens a new tab with your app in it. Which app to start is defined in the `mainClassName` of your `build.gradle`.

The browser's URL shows the `localhost` URL with whatever properties you have specified either
in your app or in your `build.gradle`. You don't need to worry about starting a JPro server
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

* `mvn jpro:restart` **restarts the JPro server**. Should the JPro server already be running,
  it automatically gets stopped before restarted.

* `mvn jpro:release` **creates a zip-file**, which contains a build of the **current project**,
  including the dependencies for JPro and for the current project.
  It contains scripts for `start/stop/restart` of the ***deployed JPro servers***.
  The scripts are located in the *bin-folder*.

(*) the "currently specified application" is the `mainClassName` defined in the `pom.xml`.

(**) in this process we are dealing with a single JPro server, which is why no JPro server needs to be addressed
specifically.

During development, when you iteratively check your last program changes, you basically do fine with
just using the `jproRun` command from your terminal window. If required, it automatically starts your browser,
and opens a new tab with your app in it. Which app to start is defined in the `mainClassName` of your `pom.xml`.

The browser's URL shows the `localhost` URL with whatever properties you have specified either
in your app or in your `pom.xml`. You don't need to worry about starting a JPro server
etc., it is all handled by the `mvn jpro:run` command for you.

In a real world scenario, though, when your JPro server runs **remotely**, you will require the other commands,
like the `mvn jpro:start` etc.

## CONFIGURING JPRO

### Gradle and Maven

The Gradle plugin is configured under the `jpro` tag of `build.gradle`.
The Maven plugin is configured under the `<plugin>` tag of `pom.xml`.  
The set of supported properties for Gradle and Maven are identical.

The following configuration properties are available:

| Property         | Default value                           | Description                                                                                                                                                                             |
|------------------|-----------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| visible          | false                                   | If true, an additional window, beside the browser window, hosts the original javafx-application. This is for debuggig, only. It impacts the performance negatively.                     |
| port             | 8080                                    | The port to which the server should listen.                                                                                                                                             |
| openURLOnStartup | true                                    | Tells JPro, whether the Browser should be opened after calling `jproRun`                                                                                                                |
| openingPath      | "/"                                     | On `jproRun` the Browser is automatically opened. This variable defines the path of the opened URL.                                                                                     |
| useFontConfig    | false                                   | Tells the Server, whether the library fontconfig should be used to resolve fonts. It's deactivated by default to make sure, the font is always the same.                                |
| useModuleSystem  | false                                   | When set to true, all dependencies are loaded as modules.                                                                                                                               |
| jproVersion      | The version of the `jpro-gradle-plugin` | The JPro-version to be used.                                                                                                                                                            |
| javafxVersion    | "auto"                                  | Possible values are `auto`, `latest`, `15`, `14` and `11`.                                                                                                                              |
| JVMArgs          | []                                      | A list of arguments, which are used to run JPro.                                                                                                                                        |
| verbose          | false                                   | If set to true, the start arguments of the JPro server are printed to the console.                                                                                                      |
| releaseName      |                                         | Sets the name of the zip generated by `jproRelease`. Also, `-jpro` postfix will be added to the resulting filename. If this property is not set, the project name will be used instead. |
| releasePlatform  |                                         | Sets the platforms of the zip generated by `jproRelease`. Possible values are `linux`, `linux-aarch64`, `mac`, `mac-aarch64`, `win`.                                                    |
| jproReleaseFiles | [:]                                     | A map of paths and files, which should be added to the zip, generated by `jproRelease`                                                                                                  |

On Gradle there is a configuration called `jproOnly` which is used to configure the dependencies which are only
used when running the application with JPro server.

```groovy
dependencies {
  jproOnly "com.mycompany:some-library-jpro-implementation:1.0.0"
}
```

#### A build.gradle example

Here an **example**:

```
jpro {
  visible = true                      // Enables for an extra JavaFX 
                                      // window to open beside the browser.
                                      // This might be helpful should there be 
                                      // differences in the rendering
                                      // between the browser and a native  
                                      // version of the app.
                                      
  port = 8083                         // The web-socket app to use.  

  jproVersion = "2023.3.1"            // The JPro version to use.  

  openURLOnStartup = false            // This prevents the browser from opening 
                                      // when jproRun is called.    
                                              
  openingPath = "/fullscreen/"        // A prefix to use for the path in  
                                      // the Url for the browser.
                                      
  JVMArgs << '-Xmx3500m'              // Lets set the memory for the JPro-Server
  
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

| Property                               | Default value | Description                                                                                                                                          |
|----------------------------------------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| jpro.preventSystemExit                 | true          | Tells the JVM, to prevent calls to `java.lang.System.exit`.                                                                                          |
| jpro.adminUsername                     | ""            | The username, to access logs, passwords etc.                                                                                                         |
| jpro.adminPassword                     | ""            | The password, to access logs, passwords etc.                                                                                                         |
| jpro.gcWorkaroundStage                 | true          | Activated a workaround for a memory leak in JavaFX when closing a stage.                                                                             |
| jpro.logResourceAccess                 | false         | Log all access to resources under the path `jpro/html`.                                                                                              |
| jpro.logUserInputEvents                | true          | Log all input events.                                                                                                                                |
| jpro.logConsole                        | true          | Redirects the console output to the logging system.                                                                                                  |
| jpro.logToJUL                          | false         | Redirects the logging to the java.util.logging system.                                                                                               |
| jpro.logToJsonFormat                   | false         | Logs the structured messages in JSON format.                                                                                                         |
| jpro.logger.resource                   | ""            | Location of the new logging configuration accessed as a resource.                                                                                    |
| jpro.logger.file                       | ""            | Location of the new logging configuration accessed as a file.                                                                                        |
| jpro.logger.url                        | ""            | Location of the new logging configuration accessed as a URL.                                                                                         |
| jpro.onJVMStartup                      | null          | A string to a class, which should be executed during the startup of the JVM.                                                                         |
| jpro.onFXStartup                       | null          | A string to a class, which should be executed during the startup of the application, on the JavaFX Application Thread, after the server has started. |
| jpro.onJVMShutdown                     | null          | A string to a class, which should be executed during the shutdown of the JVM.                                                                        |
| jpro.addInstanceID                     | false         | When true, all requests from the client, contain the current instance ID.                                                                            |
| jpro.workingDir                        | null          | The working directory of the application.                                                                                                            |
| jpro.linkUnownedWindowsToFirstInstance | false         | When true, all unowned windows are linked to the first instance.                                                                                     |

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
be started when you trigger a **starting option**. The different options for starting an app in the browser are:

* using the `jproRun` or the `jpro:run` command (See [JPRO COMMANDS](#jpro-commands))
* authoring a URL in the browser

A **typical localhost URL** looks like the following:

`https://localhost:8083/myApp`  or  `https://localhost:8083/fullscreen/myApp`

For an app to be **JPro enabled**, it must extend the class called

`javafx.application.Application`.

After declaring an app as runnable in the `jpro.conf`, **it can be embedded into a webpage** by using the `<jpro-app>`
tag
like follows:

```html
<jpro-app href="/app/appname1" />
```

Go to the next chapter _**EMBEDDING JPRO**_ to see how to embed a runnable app into an existing webpage.

## EMBEDDING JPRO

JPro can be **embedded into an existing html-page** by using the tag `<jpro-app>`.
To activate the JPro-tag the following lines need to be introduced to the html-page:

```html
<link rel="stylesheet" type="text/css" href="/jpro/css/jpro.css">
<script src="/jpro/js/jpro.js" type="text/javascript"></script>
```

To embed JPro to your dom, you need to introduce to your html-file:

`<jpro-app href="/app/default">`

### Supported attributes for the jpro-app tag

The jpro-app tag has a set of **attributes**, which can be set to control the jpro-app's behaviour:

| Attribute name         | Default value | Description                                                                                                                                                                            |
|------------------------|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| href                   |               | The URL of the application to be started.  It is either the URL of the App's websocket connection `"wss://yourServer.com/app/myAppName"`, or it's the relative URL `"/app/myAppName"`. |
| loader                 |               | Defines whether or not to activate the loading animation for this JPro-app. Valid values are: `"default"` `"none"`                                                                     |
| loaderURL              |               | Defines a gif file which can be used to replace the standard loader.                                                                                                                   |
| fullscreen             | "false"       | When true, the JPro app is resized to the entire page. It also **sets autofocus** to true.                                                                                             |
| readonly               | "false"       | When true, the user can NOT do any data authoring to the scene.                                                                                                                        |
| disableShadows         | "false"       | Disables all shadows in the JPro-renderer.  This might be useful, for rendering performance reasons.                                                                                   |
| disableEffects         | "false"       | Disables all effects in the JPro-renderer.  This might be useful, for rendering performance reasons.                                                                                   |
| disableClip            | "false"       | Disables all clips in the JPro-renderer. This is useful for debugging.                                                                                                                 |
| disablePointerCapture  | "false"       | Disables the usage of pointer capture to get the mouse events. This is useful for debugging.                                                                                           |
| disableVirtualKeyboard | "false"       | Disables the virtual keyboard on mobile devices.                                                                                                                                       |
| autofocusEnabled       | "false"       | When true, the JPro-tag gets focused when the page is opened. This is useful for text-input, for example to enable the TextInput for a login-mask.                                     |
| nativescrolling        | "false"       | When true, the scroll events are managed by html. Otherwise they are managed by the JPro app.                                                                                          |
| nativezooming          | "false"       | When true, the zoom events are managed by html. Otherwise they are managed by the JPro app.                                                                                            |
| userSelect             | "false"       | When true, the text selection is managed by html. Otherwise it is managed by the JPro app.                                                                                             |
| scale                  | "false"       | When true, the JPro app's scene is scaled to fit the html container. It works similar to `background-size: cover`in html.                                                              |
| stretch                | "false"       | When true, the JPro app's scene is stretched to fit the html container.                                                                                                                |
| fxwidth                | "false"       | When true, the width  of the JPro-tag is managed by the JPro app. Otherwise the width  is managed by html.                                                                             |
| fxheight               | "false"       | When true, the height of the JPro-tag is managed by the JPro app. Otherwise the height is managed by html.                                                                             |
| fxContextMenu          | "true"        | When true, the context menu of the browser is suppressed and NOT shown. Is useful, when the JPro app itself has got a context-menu to show instead.                                    |
| setPrintJSCommands     | "false"       | When true, all js-commands executed through the WebAPI are logged on the browser console.                                                                                              |
| timeUntilReconnect     | "10000"       | It specifies after how much time, the client tries to reconnect, when he didn't hear anything from the server.                                                                         |
| snapshot               | "auto"        | When set to true, the JPro app is rendered as a static image. On "auto" this only happens, when it's indexed and WebSocket is not available.                                           |

### Supported extra attributes for the specified JavaFX node

Extra **attributes** are supported by calling `node.getProperties().put("attributeName", attributeValue)` in the JavaFX
code
in order to control the browser behaviour for a specific node.

| Attribute name | Default value | Description                                                                                                                                                                                                                                                                                 |
|----------------|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| translate      | true          | When false, disables the text translation from the browser. This is useful for example when we want to disable translation on a specified text-input control. The translation rule is inherited from the parent node.                                                                       |
| vkType         | null          | Defines the virtual keyboard, used for a given `TextInputControl`. Check out [mdn web docs](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#input_types) for possible values. Only values that change the virtual keyboard have an effect. Other values should not be used. | 

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
some **simple conventions** defined for the jpro servers. Because of those conventions, you are freed from
the burden of using separate web servers for your resources, be it images, html-files or any
other thinkable resource.

Any resource underneath the package `jpro/html` are publicly available through the jpro-server as a URL.
Another practical convention is that, when a file is named `index.html` the filename itself is redundant and
can therefore simply be skipped for the URL.

The follwing examples should explain well what is meant:

The JPro server can be reached with the url `http://localhost:8080`,

`jpro/html/myImage.jpg` with `http://localhost:8080/myImage.jpg`,

`jpro/html/folder/myImage.jpg` with `http://localhost:8080/folder/myImage.jpg` and

`jpro/html/index.html` with `http://localhost:8080/index.html` or

`jpro/html/index.html` with `http://localhost:8080/`.

### Publishing JPro applications

To make your JPro applications accessible via URL, you should create an “index.html” and place
it into

`/jpro/html/index.html`

or in the project structure under

`src/main/resources/jpro/html/index.html`.  
\
As mentioned in the last chapter, all files to be accessible via URL, be it HTML files, images, documents or others,
should be placed in the classpath on `/jpro/html`.

## THE WEBAPI

The main purpose of the WebAPI is to let you create individual Javascript code for the browser,
which can interoperate with JPro. This means, should you want to bind your browser app to existing Javascript code,
then the WebAPI comes to play. But, in addition, it offers some general methods, which you will find
useful when creating cross-platform solutions.

The following features are currently available:

* Detecting your current running platform, like `com.jpro.web.WebAPI.isBrowser`
* Information about your current **session**, **language** used, **cookies**, the current **URL**, etc.
* Bridges for **bidirectional communication** between client-side Javascript/browser code and server-based java code.
* You can **interchange data**, do **remote calling**, registering remote functions calls, to be used between   
  the client-side Javascript/browser and your server-based java code, and vice versa.

\
There are two ways to get access to the WebAPI:

* let your app `extend JProApplication` and call `getWebAPI()`, or
* call `WebAPI.getWebAPI(javafx.scene.Scene scene)` or
* call `WebAPI.getWebAPI(javafx.stage.Window window)`.

\
For exact details about the API itself, please go to the [WebAPI-documentation](https://www.jpro.one/api/2023.3.1/com/jpro/webapi/WebAPI.html).

### Using the WebAPI without JPro

#### Using Gradle

The WebAPI can be imported as a jar, also when not using JPro. It can be introduced to the `build.gradle` by
the following statement:

```groovy
dependencies {
    implementation "com.sandec.jpro:jpro-webapi:2023.3.1"
}
```

#### Using Maven

The WebAPI can be imported as a jar, also when not using JPro. It can be introduced to the `build.gradle` by
the following statement:

```xml
<dependencies>
    <dependency>
        <groupId>com.sandec.jpro</groupId>
        <artifactId>jpro-webapi</artifactId>
        <version>${jproVersion}</version>
        <scope>compile</scope>
    </dependency>
</dependencies>
```

#### Getting WebAPI as a Jar

You can download the WebAPI from our [repository](https://sandec.jfrog.io/artifactory/repo/com/sandec/jpro/).

This can be useful when you are using neither Maven nor Gradle.

[Here is the download link for the latest version.](https://sandec.jfrog.io/artifactory/repo/com/sandec/jpro/jpro-webapi/2021.1.0/jpro-webapi-2021.1.0.jar)

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
| /info/heapdumps/heapdump.hprof | Downloads the heapdump of the server. Useful for finding memory-leaks with tools like [VisualVM](https://visualvm.github.io/)                                    |
| /jpro/api/instances            | A list of all currently open instances.                                                                                                                          |

Here is an example of a command sent to a running JPro server called **https://www.jpro.one/status** (which is password
protected)

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

Basically, JPro servers can run on any server with a JVM on it. But, fact is, so far all our real world projects
are using Linux for the backend and therefore also for JPro. For development purposes, we are mostly running our
JPro servers on macOS or Windows. Our recommended platform
for the JPro servers at time being is [Ubuntu 20.04](https://releases.ubuntu.com/20.04/).  
Other requirements are:

* JavaFX requires some libraries to run in an headless environment.
  Installing GTK and X11 is usually enough to run JavaFX.

* For production, it is highly recommended to use SSL.
  Why is this important?
  Because, some time proxies manipulate the traffic stream, and this would otherwise break the support of websockets.

## PREPARING LINUX FOR JPRO

### All linux versions

Install Java11 on your linux server. We recommend
using [AdoptOpenJDK 11](https://adoptopenjdk.net/installation.html#x64_linux-jdk):

### Ubuntu 22.04

To use JPro on Ubuntu 22.04, one has to install the following packages:

```shell
sudo apt-get install xorg libasound2 libgtk2.0-0
```

### Ubuntu 18.04 and 20.04:

To use JPro on Ubuntu 18.04/20.04, one has to install the following packages:

```shell
sudo apt-get install xorg gtk2-engines libasound2 libgtk2.0-0
```

### Ubuntu 16.04:

To use JPro on Ubuntu 16.04, one has to install the following packages:

```shell
sudo apt-get update

sudo apt-get install xorg gtk2-engines libasound2
```

### RedHat 7.5:  (OracleLinux CentOS (Tested with Redhat 7.5))

To use JPro on RedHat, one has to download and install the
official [Oracle-Java](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) (not
OpenJDK).
The download must be a rpm-package.

```shell
# You have to download and install Oracle Linux

sudo yum localinstall <filename>.rpm

sudo yum install gtk2 
sudo yum groupinstall "X Window System"
```

### Debian GNU/Linux 9 (Stretch)

To use JPro on Debian, one has to install the following packages:

```
sudo apt-get install software-properties-common
sudo apt-get update
sudo apt-get install gtk2-engines xorg libasound2
```

### Amazon Linux

We don't recommend Amazon Linux, because it does not contain a package for GTK.
GTK is required by JPro for Linux. On Amazon Linux, you would have to compile it for yourself.
This makes it very difficult to run JPro on Amazon Linux.

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

In order to configure nginx for JPro, create the file

`/etc/nginx/sites-enabled/jproconf.nginx.conf`

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
(replace `yourdomain` with the real name):

`/etc/nginx/sites-enabled/yourdomain_com.nginx.conf`

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

## DOCKER WITH JPRO

It's quite easy to use JPro with Docker.
The simplest way to start your application in a docker-container,
is to unzip the JProRelease file,
and run `docker-compse up`

The following Dockerfile can be used to get a container which is compatible with JPro.

```
FROM adoptopenjdk:11-hotspot-focal
RUN apt-get update
RUN apt-get -y install xorg gtk2-engines libasound2 libgtk2.0-0
```

## JPro Close Instance Strategy Configuration

This documentation describes the JPro Close Instance Strategy configuration structure and explains each field in the
configuration.
The configuration can be done in the `jpro.conf` file.

### Configuration Structure

The configuration is structured into three optional strategies: `short`, `medium`, and `long`. Each strategy contains
the following properties:

- `until`: This property defines, until which duration the strategy is used. It must be not set, for the last strategy.
- `closeOnTabCloseAfter`: The second after which the instance will close if the tab is closed. -1 means it will not
  close after tab close.
- `closeOnDisconnectAfter`: The second after which the instance will close if a disconnect is detected. -1 means it will
  not close after disconnect.
- `closeOnAFKAfter`: The second after which the instance will close if a user is detected to be AFK (Away From
  Keyboard). -1 means it will not close after AFK.
- `closeOnBackgroundAfter`: The second after which the instance will close if the application goes to the background. -1
  means it will not close after going to the background.

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

* Your app **must NOT block** the javafx-thread. Wait-, sleep-commands, showAndWaits in the javafx-thread are no-nos.
* Be careful when using **dialog boxes**. Make sure they don't use showAndWait (see above).
  [Here](https://github.com/JPro-one/JPro-Samples/tree/master/popups) you can see how to create a JPro agnostic popup.
  You can also use [this popup](http://www.jfoenix.com/documentation.html#Dialog) from the JFoenix library.
* Be careful with **statics**, because they would be shared between multiple instances
  (interesting enough, there are use cases in which this fact can be utilized as a very useful feature.
  But, it is important not to use them in the wrong way.)
* You can open **Stages** with the method `openStageAsPopup(Stage stage)` and `openStageAsTab(Stage stage)` of
  the [WebAPI](https://www.jpro.one/api/2023.3.1/com/jpro/webapi/WebAPI.html).
  An alternative is, to create new windows or dialogues by using a StackPane at the root of your application.
  We have an example about popups in our [sample-project](https://github.com/JPro-one/JPro-Samples/tree/master/popups).
* The class WebView only works very limited with JPro.
  It should be replaced with `com.jpro.webapi.HTMLView`.
  [This sample](https://github.com/JPro-one/JPro-Samples/tree/master/html-jpro) shows how to use
  the **HTMLView**.
* JPro currently requires at Least Java(FX) 11 or newer.
* JPro requires a JRE without JavaFX. This is the standard since Java11.
  Most JDK Vendors, which bundle JavaFX, also provide a version without JavaFX.

### Not yet supported JavaFX features

(this list refers to version 2023.3.1)

* MediaPlayer is now supported via the [JPro Media](https://github.com/JPro-one/jpro-platform/tree/main/jpro-media)
  module.
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
* FileChooser alternative is provided via the [JPro File](https://github.com/JPro-one/jpro-platform/tree/main/jpro-file)
  module.
* Clipboard
* [Dialog](https://openjfx.io/javadoc/21/javafx.controls/javafx/scene/control/Dialog.html) (check out our checklist above
  for alternatives.)
* WebView (Supported in its basic form, only. We recommend to use the
  [HTMLView](https://www.jpro.one/api/2023.3.1/com/jpro/webapi/HTMLView.html), instead.)

## JPro Loadbalancer

> JPro version 2022.1.2 or newer is required!

### Overview

The JPro Loadbalancer allows you to run multiple JPro Servers in parallel.  
You can configure the **_maximum number of JPro Servers to automatically be started and stopped on demand_** by setting
the property

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`one.jpro.loadbalancer.localServerCount`

inside the file named `application.properties` to your required value. This provides you with a server landscape, which
dynamically up- and down-scales according to current demand, but still respects an overall system size limit.

You can configure the **_maximum number of sessions to be accepted per JPro Server_** by setting the property

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`one.jpro.loadbalancer.sessionsPerServer`

inside the file named `application.properties` to your required value. This sets the rule for when additional JPro
Servers should be available.

#### Single Instance per JVM

With the JPro Loadbalancer you have the choice to set the **_maximum sessions to be accepted per JPro Server_** to 1, in
which case you ensure, that the JPro Server never needs to manage parallel sessions running inside the same JVM. In this
case, you have fewer [rules to take into account](#jpro-checklist) when adapting
existing desktop apps to JPro.
You set this with the property

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`one.jpro.loadbalancer.sessionsPerServer = 1`

inside the file named `application.properties`.

#### Configure external servers

When configuring the `external servers` setup, ensure to set the `one.jpro.loadbalancer.localServerCount` property to 0.
To define additional external servers, utilize the prefix `one.jpro.loadbalancer.externalServer` followed by an index
starting from 1.
This allows you to add as many external servers as required. There is no need to configure other non required
properties,
as the JPro Loadbalancer will automatically load the default values.

Use the following configuration as an example:

```properties
# Set the count of local servers to 0
one.jpro.loadbalancer.localServerCount=0
# Configure external servers
one.jpro.loadbalancer.externalServer1=http://server1.example.com:9101
one.jpro.loadbalancer.externalServer2=http://server2.example.com:9102
one.jpro.loadbalancer.externalServer3=http://server3.example.com:9103
one.jpro.loadbalancer.externalServer4=http://server4.example.com:9104
...
```

### Usage

#### Prerequisites

Make sure you already have a JPro project and a zip file, created with
the [JPro Release command](#jpro-commands) (either `./gradlew jproRelease` or `./mvnw jpro:release`).

#### Steps

1. Create for the JPro Loadbalancer a folder F.
2. Go into the folder F.
3. Download the [JPro Loadbalancer](https://sandec.jfrog.io/artifactory/repo/one/jpro/jpro-loadbalancer/0.10.0/jpro-loadbalancer-0.10.0.jar)
   into the folder F:  
    ```shell
    curl -LO https://sandec.jfrog.io/artifactory/repo/one/jpro/jpro-loadbalancer/0.10.0/jpro-loadbalancer-0.10.0.jar
    ```
4. Either create a new one or use an existing file named `application.properties`, located in the folder F and define
   the properties there. This file can be used, to configure the JPro Loadbalancer.
5. Put the zip file, created by the [JPro Release command](#jpro-commands), into the folder F.
6. Start the JPro Loadbalancer:
    ```shell
    java -jar <jpro-loadbalancer-jar>
    ```

### Configuration

#### An application.properties example

The file `application.properties` might look like the following:

```
server.port = 8080
one.jpro.loadbalancer.startPort = 8100
one.jpro.loadbalancer.localServerCount = 4
one.jpro.loadbalancer.sessionsPerServer = 1
one.jpro.loadbalancer.warmedUpServers = 1
one.jpro.loadbalancer.vmArguments = -Xmx500m
```

#### The application.properties

The following parameters can be set in the `application.properties`:

| Property                                | Default value | Description                                                                                                                                                                                                                  |
|-----------------------------------------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| server.port                             | 8080          | The port used by the JPro Loadbalancer.                                                                                                                                                                                      |
| one.jpro.loadbalancer.zip               | auto          | The zip file containing the JPro Server.                                                                                                                                                                                     |
| one.jpro.loadbalancer.zipFolderName     | auto          | The folder of the zip file.                                                                                                                                                                                                  |
| one.jpro.loadbalancer.vmFolder          | vms           | The folder which will contain the unzipped JPro Servers.                                                                                                                                                                     |
| one.jpro.loadbalancer.startPort         | 8100          | The first port used by the JPro Servers.                                                                                                                                                                                     |
| one.jpro.loadbalancer.localServerCount  | 4             | The maximum amount of JPro Local servers to run in parallel.                                                                                                                                                                 |
| one.jpro.loadbalancer.sessionsPerServer | 1             | The maximum amount of JPro sessions to run in parallel inside of one JPro Server. If `-1` is set, then virtually an unlimited number of sessions per server is allowed, limited only by the server CPU and memory resources. |
| one.jpro.loadbalancer.warmedUpServers   | 1             | The number of JPro Servers to always be kept running, up and ready, before they are demanded.                                                                                                                                |
| one.jpro.loadbalancer.vmArguments       | ""            | A list of arguments provided to the JPro Server. They are split by " " and support exacapping with "\\"                                                                                                                      |
| one.jpro.loadbalancer.serverJavaHome    | ""            | The path to the Java home directory that will be used during the start of each local JPro Server.                                                                                                                            |
| one.jpro.loadbalancer.isolatedUserHome  | true          | When true, an own home directory is created for the process. It's accessible through System.getProperty("user.home")                                                                                                         |
| one.jpro.loadbalancer.printEnvironment  | false         | Prints the environment values available for JPro Loadbalancer during startup.                                                                                                                                                |
| one.jpro.loadbalancer.printConfig       | false         | Prints the configuration of the JPro Loadbalancer during startup.                                                                                                                                                            |
| one.jpro.loadbalancer.logToJsonFormat   | false         | Logs the structured messages in JSON format.                                                                                                                                                                                 |

#### Logging properties

It is also possible to configure different logging properties in the `application.properties`.

##### Example

```
logging.level.one.jpro.loadbalancer=debug`
logging.level.root=debug
```

Because the JPro Loadbalancer is technically a simple [Spring Boot server](https://spring.io/projects/spring-boot), all
the [configurations possible in Spring Boot](https://docs.spring.io/spring-boot/docs/3.2.x/reference/html/features.html#features.logging)
can also be applied.

### Running as a Windows Service

#### Windows Service Wrapper

To use the [Windows service wrapper](https://github.com/winsw/winsw), we have to do 2 things as a preparation.
The steps happen in the same folder, which is used to place the application.conf and the jpro-loadbalancer jar.

First, download the WindowsServiceWrapper exe, and rename it to the name you want your service to have.
You can find the releases on its [GitHub Release page](https://github.com/winsw/winsw/releases).

```
curl -L --output myapp.exe https://github.com/winsw/winsw/releases/download/v2.11.0/WinSW-x64.exe
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
<arguments>-jar "%BASE%\jpro-loadbalancer<version>.jar"</arguments>
</service>
```

After you have created the configuration file and adapted it,
you can install the service:
`myapp.exe install`

Some other available commands are:
`myapp.exe uninstall`, `myapp.exe start`, `myapp.exe stop`, `myapp.exe restart`

For more details, take a look at the [project homepage of winsw](https://github.com/winsw/winsw).

# CHANGELOG

## 2023.3.X

### 2023.3.1 (26. October 2023)

#### Features

* It's now possible access the MimeTypes of a dragged file with the method `FileHandler.getFilesDragOverTypes()`.
  Accessing the filenames/extensions is not possible due to browser limitations.
* Added the attribute `jpro-hidden` to Window. When set to true, then the window is not rendered as part of its owners
  instance.
  It can be set with `window.getProperties().put("jpro-hidden",true)`.

#### Bugfixes

* When a "Snapshot" of a page is created for indexing, then an exception is sometimes thrown since `2023.3.0`.
  In certain configurations, this could trigger a restart with systemd.
  This if fixed now. Also, the close reason in this case is now always `snapshot-finished` for both the Instance and the
  View.
* `WebAPI.runAfterUpdate(f)` no longer blocks other `runAfterUpdate` functions from executing if the provided
  function `f` throws an exception.
* Fixed the native rendering of fonts on macOS. This is only relevant when creating a snapshot.
* The method makeMultiFileUploadNodeStatic(Node) had the wrong return type. It was changed from `FileUploader`
  to `MultiFileUploader`.

### 2023.3.0 (4. October 2023)

#### Features

* JavaFX21 is now supported and used by default.
* Reworked how instances are closed. It can now be configured with more details in the jpro.conf.
  It's now also possible to configure that an instance is closed when the user is afk, or the tab is in the background -
  which is not the default behavior.
  Check out the `JPro Close Instance Strategy Configuration` section for more details.
* Enhanced WebAPI.FileHandler with a new property, FileHandler.selectionMode, to enable configurable multiple file
  selection.
* Added a new version of `WebAPI.executeScriptWithVariable(f)` which returns a JSVariable.
* Added a new configuration parameter `jpro.linkUnownedWindowsToFirstInstance` to the `jpro.conf` file.
  When set to `true`, all unowned windows are linked to the first instance.
  This is useful for applications not designed to run multiple Instances in the same JVM.
* Text translation in the browser for a specific node can now be enabled or disabled by
  setting the attribute **translate** in the Node properties to `true` or `false`.
  The translation rule is inherited from the parent node.

  > As an example, disabling translation on a specific text field can be done by calling:
  textField.getProperties().put("translate", false);
* Added missing Documentation on how to customize the keyboard with the `vkType` property.
* Added new properties to `InstanceInfo`. The properties are **nodesCreated**, **nodesSynchronized** and *
  *nodesCollected** for the instance.
* Reworked the new experimental `InstanceInfo` API in the WebAPI. Added the properties afk, background and
  lastActionTime.
  The original methods are now changed to be properties.
* The JPro Gradle plugin now works with JavaFX Gradle plugin version `0.1.0`.

#### Changes

* Reduced the CPU usage of an idle JPro instance.

#### Bugfixes

* Removed the accidental `throws Exception` from the method `WebAPI.executeScriptWithVariable`
  and `WebAPI.executeScriptWithReturn`.
* Always the correct **WebAPI** version matching the JPro server is now used. This ensures that the server starts
  properly.
* Fixed a bug when setting a custom JavaFX Version in the Gradle/Maven Plugin. The version was not set correctly.
* Fixed the method `InstanceInfo.getInitialHostName`. Before, it always threw an exception.
* Fixed the structured log messages when closing an instance. Some values were set to be "Unknown".
* Fixed `WebAPI.closeInstance()`. It now works as expected.

## 2023.2.X

### 2023.2.2 (16. August 2023)

### Features

* Renamed the newly added method getHTMLElement to getElement.
* Added the new experimental method `WebAPI.getHTMLViewElement`, `WebAPI.wrapNode` and `WebAPI.loadNode` to the WebAPI.
    * WebAPI.wrapNode: Useful for implementing links, copy-to-clipboard functionality, and more
    * WebAPI.getHTMLViewElement: For enhanced integration with external HTML libraries.
    * WebAPI.loadNode: Serialize a node before using it in the browser. This is useful for large nodes, which are not
      used immediately.
* Use `ISO-8601` format based representation for `Time running` information in the JPro stats page.

### Bugfixes

* Resolved an issue where, if two or more Canvas nodes were utilized and the same image was rendered in the same frame,
  only one image would appear. This has now been corrected.
* Previously, when the Canvas attempted to render an unloaded font, it defaulted to a generic font. This behavior has
  been improved to ensure the intended font is loaded and correctly rendered.
* Addressed a rare translation operation error during the Canvas rendering process.
* Implemented canvas filling attribute `FILL_RULE`, an algorithm by which is determined if a point is inside or outside
  the filling region.
* Added support for rendering dashed lines in the Canvas node.
* Disable automatic translation in the browsers for text input controls.
* When using in the Gradle plugin `jproRun` or `jprStart` tasks, or in the Maven plugin `jpro:run` or `jpro:start`
  phases,
  the plugin will first verify if an exising JPro server is already running on the designated port before initiating a
  new server.

### 2023.2.1 (3. July 2023)

### Bugfixes

* Fixed a bug with the new, improved `start.bat` script. After stopping the JPro server, a process was hanging in the
  background.
* Fixed a bug with the improved Gradle plugin. In some cases, not all dependencies were compiled.

### 2023.2.0 (29. June 2023)

### Features

* We now support **JavaFX20** and use it by default!
* We have updated the JPro Maven plugin. We now guarantee with automated tests, that the MavenPlugin
  works for `3.6.x`, `3.8.x`, `3.9.x` and the latest preview `4.0.0-alpha-5`.
  It is now possible to configure the JPro server by passing arguments to a JPro related goal via
  `-Djpro.param=value`, where `param` is the name of the JPro related parameter and `value` is its value.

  *Please note that if the parameter itself has already been configured via the JPro Maven Plugin inside the POM file,
  the given `value` will **NOT** be taken in consideration.*

  > As an example, to configure the `port` parameter before starting the server,
  we can call the following command `mvn jpro:run -Djpro.port=9000`.

* The `WebAPI.getInstanceInfo()` and `WebAPI.getServerInfo()` methods have been introduced to provide access to instance
  and server information, enabling users to retrieve and monitor the current status. These classes are marked
  as `@Experiemntal`
  since they are still subject to change in the future.
* Added a new logging section on the Documentation page.
* It's now possible to override the default `JPro` logging configuration by providing a new `logback.xml` file
  accessed by defining its path via the following options inside `jpro.conf`.
    1. `jpro.logger.resource` - to access the file as a resource in the classpath
    2. `jpro.logger.file` - to access the file as an external file
    3. `jpro.logger.url` - to access the file as a URL
* Added the `jpro.logToJUL` configuration parameter to the `jpro.conf` file. When set to `true`, the logging will be
  redirected to the Java Util Logging (JUL).
* Added the attribute `disableVirtualKeyboard` to the jpro tag. When set to true, the virtual keyboard is disabled.
* Added the configuration option `jpro.onJVMStartup` to the `jpro.conf` file. This option allows to specify a class,
  which
  is executed on JVM startup. This is useful to initialize the JVM with some code, before the JPro server has started.
* Added the configuration option `jpro.onJVMShutdown` to the `jpro.conf
* Added the plugin property `workingDir` for both Maven and Gradle. This option allows to specify the working
  directory of the JPro server before it is started.
* A new type of logging messages called `structured` logging has been introduced and used internally by JPro. Added the
  `jpro.logToJsonFormat` configuration parameter to the `jpro.conf` file. When set to `true`, the structured logging
  messages will be converted in JSON format, making them easier to analyze and work with. Furthermore, the documentation
  section has been updated to include information about this new feature and all the parameters that are currently being
  used.
* Updated the JavaFX17 version to `17.0.7`.

### 2023.1.0 (16. January 2023)

#### UPGRADE INSTRUCTIONS

We have completely rewritten the Gradle plugin and Gradle Kotlin DSL is now supported.
The Gradle plugin was renamed from `com.sandec.jpro` to `jpro-gradle-plugin`. Also,
Gradle and Maven plugins group id were renamed from `com.sandec.jpro` to `one.jpro`.

Examples of configuration changes for both Gradle and Maven from previous versions.

Previous gradle plugin configuration:

```
buildscript {
  ...
  dependencies {
    classpath 'com.sandec.jpro:jpro-plugin-gradle:2022.1.8'
  }
  ...
}

apply plugin: 'com.sandec.jpro'
```

New gradle plugin configuration:

```
buildscript {
  ...
  dependencies {
    classpath 'one.jpro:jpro-gradle-plugin:2023.1.0'
  }
  ...
}

apply plugin: 'jpro-gradle-plugin'
```

Previous Maven plugin configuration:

```
<plugin>
      <groupId>com.sandec.jpro</groupId>
      <artifactId>jpro-maven-plugin</artifactId>
      <version>2022.1.8</version>
      <configuration>
           ...
      </configuration>
</plugin>
```

New Maven plugin configuration:

```
<plugin>
      <groupId>one.jpro</groupId>
      <artifactId>jpro-maven-plugin</artifactId>
      <version>2023.1.0</version>
      <configuration>
           ...
      </configuration>
</plugin>
```

### Features

* Added `JSFile WebAPI.createJSFile(String objectURL, String filename, long size)`.
* Added the method `JSVariable JSFile.getObjectURL()`.
* Added support for Data URLs in Images.
* It's now also possible to check whether JPro is used in a browser or not via `Boolean.getBoolean("jpro.isbrowser")` as
  an alternative to `WebAPI.isBrowser()`.
* We now also publish the JPro CHANGELOG and JPro DOCUMENTATION as an additional artifact of the webapi dependency.
* Add new `releaseName` property on both Gradle and Maven plugins to configure
  the name of the zip file generated during `jproRelease` task.
* Added information about the License/Copyright into the jar of the WebAPI.

### Bug Fixes:

* Fixed a bug, which caused JPro to not work, when the domain ended with `.app`.
  A workaround for older versions is to provide the whole domain in the href of the JPro Tag. (for
  example: <jpro href="https://myapp.app/app/default"/>)
* On Mac platform, when `openURLOnStartup` property is `true`, the duke icon is no longer shown after opening the
  browser.

## 2022.1.X

### 2022.1.8 (22. November 2022)

### Features

* Added support for the property `Node.viewOrder`. Nodes with viewOrder are now rendered in the correct order. This
  property was added in JavaFX 9.
* Added `Instances active` and `Instance afk` to the page `/status`.
* The OS related information in `/status` is now computed in a background thread. This excludes any potential OS/JVM
  related performance issues.
* Introduced a new configuration parameter `verbose` for the Maven and Gradle plugins.
  When set to true, the start-arguments are logged, making it easier to debug when the application isn't starting
  properly.
* It's now possible to change the directory of the logfiles and other temporary files by setting `-Djpro.logdir` as a VM
  argument.

### Bug Fixes

* Fixed a very old bug, that when the Gradle task `jproRun` was stopped, the JPro server was not stopped correctly.
* Fixed a bug, when JPro tried to reconnect to the server, the reconnecting animation was not shown correctly.
* Fixed a regression in 2022.1.6 for `WebAPI.darkModeProperty()` and `WebAPI.devicePixelRatioProperty`.
  The properties wrongly stopped sending updates. This is now fixed.
* Fixed a regression in the file upload in `2022.1.5` until `2022.1.7`. When a file was uploaded, in some cases the
  encoding was changed resulting in changed content.
* When `WebAPI.addInstanceCloseListener(InstanceCloseListener)` was called after the page was closed, the listener was
  not called.
  Now it is called immediately.
  As a negative side effect, a memory leak was created by keeping the reference to the listener.
  This is now fixed.
* Fixed a small leak related to the JSFiles created by the WebAPI.

### 2022.1.7 (6. November 2022)

### Features

* Added experimental support for the module system.
  When setting the property `useModuleSystem` on the Gradle/Maven Plugin, then all dependencies are added as modules
  instead of added to the classpath.
* It's now possible to download all logfiles as a zip by invoking `<server>/info/log/all.zip`

### Changes

* Doubled the default size of the logfiles to 2MB.

### Bug Fixes

* Fixed regressions relating to the reconnect behaviour of the js client.
* Fixed an issue with the MavenPlugin. Sometimes the JavaFX artifacts of the wrong operating system were added to the
  classpath.
  Specifically, the `mac` artifacts were added sometimes to the `mac-aarch64` artifacts.

### 2022.1.6 (2. November 2022)

#### Features

* Added an API to upload multiple files at once. Check out the method `WebAPI.makeMultiFileUploadNode(Node)`
  A sample can be found in the `multifilehandler` sample, in
  our [JPro-Samples GitHub project](https://github.com/JPro-one/JPro-Samples).
* Added a new method `WebAPI.registerWindow(Window)`. It can be used to create a new JPro instance based on an existing
  Window.
  This was used to implement browser native scrolling, which is now used
  in [jfx-central.com](https://www.jfx-central.com/).
  It's also available as a library in [jpro-utils](https://github.com/JPro-one/jpro-utils.git).
* When a touch event is generated, and it was used for scrolling in the browser, then isStillSincePressed is set to
  false for the created MouseEvent.

#### Improvements

* Improved logging. When an instance/view is closed, always the reason is reported, and the instanceID.
* If an instance is created with the WebAPI, but no user connects to it, then the corresponding instance is closed after
  1 minute.
  It was possible to create an instance with the
  methods `WebAPIregisterWindow(Window)`, `WebAPI.openStageAsTab(Stage)` `WebAPI.openStageAsPopup(Stage)`.

#### Bug Fixes

* Instances, which are not opened once, are now closed after 1 minute.
  This could happen with the method `WebAPI.registerWindow(Window)`, `WebAPI.openStageAsPopup(Stage)`,
  or `WebAPI.openStageAsTab)`.
* Fixed a bug with the JPro tag `<jpro-app>`.
  When the HTMLElement was removed and readded to the DOM, then an additional session was started. This is now fixed.
* Various improvements to error handling.

### 2022.1.5 (27. September 2022)

#### Features

* Support For Java19
* Support for JavaFX19
* The cookies in the WebAPI are now automatically updated when they are changed from
  another tab. The update happens also when the cookies are changed from outside JPro.

#### Bugfixes

* Now a simple message is logged when the user closes a tab.
  It used to produce a warning message and sometimes also an exception.
  They both didn't have side effects, but they were superfluous.
* Fixed a rare issue when rendering. In some corner cases, render fragments were visible for 1 frame.

### 2022.1.4 (24. August 2022)

#### Bugfixes

* Fixed a memory leak related to the recently introduced class named "JSVariable" in the WebAPI.
* Fixed an issue, when using the WebAPI for downloading a file.
  Files containing "/1" in its URL were not downloaded properly.
  This was a regression in `2022.1.2`.
* Fixed an important bug related to event handling. Under some conditions, an event was evaluated later than it should,
  which generated an impression of bad performance execution of the event (the handling of the event was deferred until
  a next event arrived).
  This happened mainly on mobile.

### 2022.1.3 (2. August 2022)

Added support for Java18.

#### Changes

* When using Gradle, by default the same java command is now used, as when running with the application plugin.
  This also has the effect, that it's now possible to configure the JVM used in IntelliJ.
* The default value for `jpro.preventSystemExit` is now false. This was done to support Java18.
  It has the consequence, though, that, either you need to explicitly configure `jpro.preventSystemExit` to true, or
  you now have to make sure, your application does NOT call `System.exit`, when the stage is closed.
* Added the properties `objectURLProperty` and `shouldCreateObjectURL` to the FileHandler.
* Added the methods `createUniqueJSName()` and `createUniqueJSName(String prefix)`to the WebAPI.

#### Bugfixes

* Updated internal libraries and removed no longer needed JVM argument.
* Fixed an issue with Maven on Mac Arm.
* Fixed an issue when loading externally hosted images. This bug was introduced in `2ß22.1.2`
* Fixed some rare exceptions, related to Popup and mouse input. It didn't have any side effect.

### 2022.1.2 (30. May 2022)

JPro now also supports **ARM** for Mac and Linux!

#### Improvements

* Fixed a performance issue. This was especially harmful when running the JPro Loadbalancer with multiple JPro servers
  under MS-Windows.

#### Features

* JPro supports **ARM** for Mac and Linux!
* Added the field `jpro.statusUpdateTime` to the jpro.conf.
  When set to -1, no statistics are tracked for the status page.
* Removed the OSDetector plugin from the JPro Gradle Plugin.

#### Bufixes

* Fixed an issue with Apache as a Reverse Proxy. In some cases the URLs generated by JPro were manipulated in a way,
  which broke loading images. this is now fixed.
* Improved the error message, when `WebAPI.openStageAsTab` or `WebAPI.openStageAsPopup` is called with null.

### 2022.1.1 (8. April 2022)

Added support for JavaFX 18!
Jpro now uses JavaFX18 by default.

#### Features

* Added the method `WebAPI.closeInstance()`.
  This closes the current session and triggers a reconnecting in the client.
  This is especially useful with the LoadBalancer, when a fresh session is wanted.
* Added attribute "rememberInstanceIDInCookie" to the JProTag. When set to true, only one instance of the app is created
  per browser.
* Various resources, which are accessed by the browser, now have simplified URLs.
  This makes the link independent of the current folder of the server and makes it easier to create a sitemap and
  supporting indexing for Google.
* Added more detailed information to `/jpro/api/instances` about the opens views, and how long the instances will be
  kept open after closing all views.
* In the JProTag, the attribute `timeUntilReconnect` is removed. We have improved the reconnect behavior of the JPro
  Server.

#### Bugfixes

* Fixed a bug related to TextInput, when switching the focus between different windows.
* Fixed a bug, when the for the case that the `blurType` property of an effect was null. Before this fix, the instance
  wouldn't render properly. Now it uses the correct fallback `BlurType.THREE_PASS_BOX`.
* Fixed the script in the zip generated by JProRelease for MS-Windows. Before this fix, it failed when the path of the
  current folder contained Unicode Characters.
* Fixed a performance issue for the JPro Release when using MW-Windows. The start script `start.bat` now starts much
  faster and opens fewer file handlers.
* `WebAPI.createVirtualImage` can now be called from outside the JavaFX Thread.
* Images created with `WebAPI.createVirtualImage` now return the correct URL, when calling `Image.getUrl()`.
* Fixed an error, which occurred when reconnecting to a JPro instance(“JPro session”) containing non-digit characters.
  This is only relevant for the JPro Loadbalancer.

### 2022.1.0 (1. March 2022)

This version provides a new and efficient way/API for loading and rendering what we call “virtual images” in JPro. When
using this API the virtual images don't require any RAM space in the JPro Server, but instead enables the browser to
access the files directly through pure referencing, either to an HTTP location or to a file located on some server. The
API also provides static methods, which are useful when using the API independent of a specific JPro session.
This release drops the support for the previous JavaFX versions 14, 15, and 16 in favor of the current LTS versions 11
and 17.

#### Features

* Added support for real time updates of changes taking place in WritableImages.
* Added support for virtual images, they can be created with the
  methods `WebAPI.createVirtualImage(String url, int w, int h, boolean jproServerAsProxy)`
  and `WebAPI.createVirtualImage(String url, int w, int h, boolean jproServerAsProxy)`.
* Added static versions of the methods `setLossless` and `makeFileUploaderNode` to the WebAPI.
* Added darkMode property to the WebAPI.
* The user input is now processed in an runLater instead of an animation.
* Added the attribute `setThemeColor` to the JProTag.
  When set to true, a meta element is created which binds a webpage’s theme-color to a scene’s color.
* In the page `jpro/api/instances` users’ addresses were added and are now shown.
* LinearGradient and RadialGradient are now supported in the Canvas.
  RadialGradient has the limitation, that only non-distorted (scale in x or y) gradients are supported.
  Non-distorted scaling usually happens when the proportional property is set to true.

#### Bugfixes

* The Gradle task `jproRun` is now part of the task group `jpro`.
* Fixed a regression, when the `!<appname>` instance was used, to make sure an app is only created once.
* Fixed a regression to the ScreenSize provided by `javafx.stage.Screen`.

## 2021.2.X

### 2021.2.3

#### Summary

this update focuses on features for our new JPro loadbalancer. It also provides many minor improvements and bug fixes.

#### Features

* The new id can now be set as a query parameter when starting a new instance (`?newInstanceID=<newid>`). This is useful
  for load balancing.
* In the jpro.conf it's possible to set the value `jpro.addInstanceID`.
  When set to true, the requests from the client to the server will contain the current instance id.
  This is useful for load balancing.
* It's now possible to define a main method, which gets executed during the JPro Server’s startup.
  This can be used to speed up the handling of the initial session. It can be configured
  with `jpro.onStartup = <mainclass>`.
* Added support for `TextAlignment.JUSTIFY`, for all browsers supporting `text-align-last` which is the case for most
  common browsers, except Safari.
* Reworked the api-key. It is now provided with the key `jpro.apiKey`, as a query parameter `?apiKey=<key>`.
* Added the page `jpro/api/instances` which contains various information about the currently running instances. This is
  primarily used for the new JPro Loadbalancer.

#### Changes

* The websocket connection is now done on the url /app/ws/<appname> instead of /app/<appname>. This is only an internal
  change.
* A small performance improvement when using Text.
* Simplified `stop.bat` in the JProRelease file.
* In the default html page, the hostname is no longer part of the path to the application.
  This is useful when a load balancer is used, to avoid showing the internal address.
* Added "Instances Created" to the `/status` page.
* When a JavaScript exception is thrown, its stack trace is now printed.
* `WebAPI.getInstanceID` now returns a String instead of an Int.

#### Bugfixes

* The white background of Stages with transparent fill and without `StageStyle.TRANSPARENT`, is now rendered correctly.
* Fixed a memory leak in ScrollPane, related to touch events (JDK-8279228)
* Fixed an issue with Popups, being sometimes positioned wrongly.
* Fixed an issue with JPro, sometimes not shutting down properly.
* Added a more detailed error message, instead of an exception when the focus to a window cannot be set.
* Fixed a rare bug, which can cause the start method of the Application to be called twice.
* Fixed a minor memory leak in the js client.
* ScrollEvents now return the correct value for the method `getMultiplierX()` and `getMultiplierY()`.

### 2021.2.2 (1. December 2021)

### Features

* Merged our JavaFX17 fork with the latest JavaFX version 17.0.1
* JPro no longer uses the System font on Linux and Windows with JavaFX17, which is the default.
  This makes the behavior independent of the OS.

### Bugfixes

* Fixed a regression with the JavaFX17 build for Linux. It works again for Ubuntu18.04.
* [#114](https://github.com/JPro-one/JPro-tickets/issues/114) Fixed a bug for atypical fonts.
  Texts with fonts with an unusual baseline were rendered on a wrong y position.
  This happened with icon fonts, and very rarely with normal fonts.
* [#88](https://github.com/JPro-one/JPro-tickets/issues/88) Fixed a bug which caused some Fonts on Mac to render with
  the wrong width.
  This happened with system fonts which were not supported by the browser. Please be aware, this bug will remain fixed
  with JavaFX17+, only. When using lower JavaFX versions, this bug will still remain.
* Fixed a regression in the rendering of TextFlow. In some situations, the text was shifted wrongly by one character.
* Fixed a rare exception related to Mobile and Popups.
* Fixed issues in the SVG fallback for RTL texts.

### 2021.2.1 (15. November 2021)

### Features

* Added support for the property `Node.nodeOrientation`.
  This is usually used for applications using a "right to left" language.
* JPro now correctly renders "right to left" text.
  This is required for languages like Hebrew or Arabic.
* JPro now correctly supports `Text.selectionFill`.
  This fixes the font color of the selected text in TextField and TextArea.
* Updated the logical fonts provided by JPro. As a sans serif font, now Lato is used by default.
  JPro now also provides an italic and bold italic sans serif font.

### Bugfixes

* Fixed the control accelerator memory
  leak [JDK-8274022](https://bugs.openjdk.java.net/browse/JDK-8274022) ([Pullrequest to JavaFX](https://github.com/openjdk/jfx/pull/659))
  in our JavaFX17 fork.
  This leak is a regression in JavaFX17 and happens quite frequently. It will probably be integrated into the next
  official JavaFX17 release.
* Fixed an issue with implicitly created stages, which were created due to an implementation detail.
  The `getWebAPI(Node, WebAPIConsumer)` wrongly executed the listener also for such stages.
  The listener executions for such stages were now eliminated.
  Now the lambda is only executed when its window is managed by JPro.
* When a download was started, the JPro-Session sometimes stopped too early.
  This is now fixed.
* Fixed an issue with the cookies in the WebAPI not being updated correctly.
* Fixed the `PointerCapture` mechanism for Firefox.
  When scrolling by dragging the bar of a scrollbar, no events were created when the mouse was outside the browser.
  This is now fixed.
* Fixed a bug in the scroll events. In rare case the browser scrolled in lines instead of pixels.
  This happened on Firefox running on Ubuntu 18.04.
* Fixed an issue that JPro didn't process `pen` events correctly. Ironically this caused problems with mouse input.

### 2021.2.0 (5. October 2021)

### Features

* JPro now uses **JavaFX17** by default!
* Added support for **Java17**!
* Added support for **Touch Events**! When using JPro on mobile, now touch events are generated.
  Touch events are also generated on the desktop when using a touch device.
* JPro now generates scroll events, when using touch events. When released, the scrolling keeps the scroll inertia for a
  short time. This greatly improves the user experience on mobile.
* It's now possible to add a cleanup method to downloadURL and downloadResource, to clean up the file when it's no
  longer required.
* Added a new function `WebAPI.loadCSSFile` to the WebAPI. It works analogue to loadJSFile. This helps to integrate
  various tools for the browser.
* Added the properties `HTMLView.blockMouseInput` and `HTMLView.blockKeyboardInput` to HTMLView, to notify JPro, whether
  the HTMLView should prevent javafx events when it is the target.

### Bugfixes

* Fixed corner cases for `WebAPI.getWebAPI(Node node, WebAPIConsumer consumer)`.
* Fixed a deadlock related to drag and drop.
* Fixed a rare rendering bug related to clip and HTMLView.

## 2021.1.X

### 2021.1.4 (2. September 2021)

### Bugfixes

* Fixed a memory leak that allocates memory outside the heap.
  Due to this bug, we recommend updating to this version.
* Fixed an exception during the shutdown. It didn't have any further side effects.
* Fixed an issue with the Gradle Plugin.
  When calling `jproRun`, and the JPro process was killed from the outside, the Gradle process wasn't stopped.
  This is now fixed.

### 2021.1.3 (2. August 2021)

### Bugfixes

* When a tab was closed, the closing of the WebSocket connection triggered a reconnect to the server.
  This could result in a small flickering and unnecessary resource usage. This is now fixed.
* Fixed an issue with fonts. Sometimes fonts were loaded multiple times,
  which could cause some flickering during font rendering.
* Fixed a very rare deadlock during startup.

### 2021.1.2 (5. July 2021)

### Features

* JPro now always uses UTF-8 as the default encoding for the JVM.
* Canvas is now rendered for snapshots when no window is set.
  In the `jpro.conf`, `canvasRenderOnServer` now has the default value `null`,
  to automatically detect whether it should be rendered in the server.
* Added `addInstanceID` to the JProTag. If this value is set, all http requests from the browser will add the current
  instanceID. This is useful for load balancers.
* It's now possible to add a file named `defaultpage` to the package `jpro/html`. This file is provided when no file
  extension is provided, or the extension `html` was provided.
  This is useful to develop web pages with a normal URL scheme.
* JPro now shows the path to the JavaFX jar for easier debugging of configuration errors.

### Bugfixes

* Fixed the rendering of the padding for TextFlow. In some situations, the wrong padding was used.
* Fixed a bug for using JAVA_HOME, which was introduced in the previous update.
* Fixed a bug for the Gradle plugin, which is relevant for multi-project setups.
* Fixed an exception, when monocle is not set.
* Minor compatibility improvement for Java.

### 2021.1.1 (19. Mai 2021)

### Features

* Support for Java16.
* JPro now uses the JAVA_HOME variable everywhere when available, otherwise, it falls back to the normal Java command.
  This affects both the Gradle and the Maven Plugin.
  JAVA_HOME is now being used when starting JPro from the build tool and also when starting JPro with the JproRelease
  command.

### Bugfixes

* Fixed an issue with Gradle 7.x. In the zip created by JProRelease.
  The artifact of the current project was missing. Rarely, this also
  happened in older Gradle versions.
* Fixed an issue when installing the JProServer as a Windows service.
  The issue had the effect, that the application wouldn't start properly.

### 2021.1.0 (11. Mai 2021)

### Features

* JPro now uses JavaFX16 by default.
* The JProRelease now contains support for **Windows**!
  It contains scripts to start/restart/stop the process, and to install it as a service.
* When resizing the window, now the Background of the Scene is resized immediately without waiting for the new
  scenegraph. This highly improves the experienced performance.
* JPro now uses high-resolution images with "@2x" at the end of the name, when using high-resolution displays.
  This can be deactivated in the jpro.conf with the statement `jpro.useHighResImages = false`.
* The WebAPI of an application is now set before calling `Application.init`. This can be accessed by the method
  getWebAPI of the class JProApplication.
* The WebAPI now provides the methods `devicePixelRatio` and `getDevicePixelRatio` to access the devicePixelRatio of the
  browser.
* Added support for the property `Shape.strokeLineCap`.
* Added the attributes `disableClip` and `disablePointerCapture` to the JProTag. When set to `true` JPro either ignores
  clip or doesn't use pointerCapture for the mouseinput.
* Added more detailed error messages, when a connection to the JPro Server could not be established.

### Bugfixes

* Fixed the rendering of diacritical letters and other glyphs composed of multiple characters.
* Fixed a browser tab crash for Safari, related to pointerCapture.
* The file upload didn't work, when the Node was part of a Popup or a Stage with an owner. This is now fixed.
* Backport [JDK-8089589](https://github.com/openjdk/jfx/pull/398) for our JavaFX16 fork.
* Fixed an issue with the Focus of Substages and Popups. The Nodes can now get focused.
* Fixed an exception when switching scenes.
* Fixed an exception during mouse-input when visible is set true.
* Fixed the behavior when the font is set to null. Now `Font.defaultFont` is used in this case, just like it is for
  desktop JavaFX - instead of an internal Exception.
* Fixed a race condition happening on Safari, which sometimes caused the file upload to not work.
* Fixed an issue related to screen resizing. Sometimes on fullscreen a small white area was unused for the application.

## 2020.1.X

### 2020.1.6 (20. April 2021)

* Moved to a new repository for hosting the artifacts because of
  the [Bintray shutdown](https://jfrog.com/blog/into-the-sunset-bintray-jcenter-gocenter-and-chartcenter/).
  The old Bintray repository will stop working at the 1. Mai. The new repository
  is `https://sandec.jfrog.io/artifactory/repo`.
  Checkout our commits to our HelloWorld projects, for the required
  changes: ([Maven](https://github.com/JPro-one/HelloJPro-Maven/commit/dfad6b6ace5f5d179dd1ccb26b3ede6fb3c53064), [Gradle](https://github.com/JPro-one/HelloJPro/commit/1c33028c033abf757d97d40ad53f0ed25782f325))

### 2020.1.5 (24. March 2021)

### Features

* Added an error message to be thrown when an unsupported JVM which bundles JavaFX is used. A JVM which bundles JavaFX
  is not supported by JPro, because JPro uses its own JavaFX Fork.
* To avoid confusing behavior the method `WebAPI.openStageAsTab` requires the Owner to be null. When the Owner is not
  null, we throw an exception.

### Bugfixes

* Fixes for MouseEvents. Now, when a Session is closed, a MouseExited-Event with the last mouse position is sent. Before
  this fix, when the Mouse was pressed and released, the MousePressed-Event was suppressed and the MouseReleased-Event
  only was generated. This is now fixed.
* When the JavaFX-Thread was blocked, sometimes the webserver was not responding. This is now fixed.
* Fixed the rendering of the class SubScene.

### 2020.1.4 (16. February 2021)

### Features

* Added **Docker Compose** to the JProRelease.
  If you unzip the generated zip-file, you can run `docker-compose up` to run the application as a Docker service.

### Bugfixes

* Fixed a startup error on Window. The Maven and Gradle Plugin now forwards the classpath for JPro Itself through a file
  instead of through the command line.
  This is very important to avoid the maximum length for the command line on Windows.
* Fixed a memory leak that happened after reconnecting to a running application.
  This could, for example, happen after being offline due to short connection problems.
* Fixed a bug in the Gradle plugin when JPro was used in a subproject.
  The server process is now started in the same folder as the folder of the subproject.
  This sometimes caused issues when starting the server related to the RUNNING.PID file.
* Fixed issue related to mouse input on mobile Firefox. Possible exceptions in the javascript-code are now properly
  logged.

### 2020.1.3 (27. January 2021)

### Bugfixes

* Fixed a regression in 2020.1.1, scrolling inside Popups wasn't working properly.
* Fixed an issue with the Gradle plugin. Sometimes the file RUNNING_PID was checked in the wrong folder.
* Fixed a bug in the zip created by JProRelease. This is a regression from 2020.1.0.
  The scripts `restart.sh`, `restart-background.sh` and `start-background.sh`
  weren't giving their arguments to the JVM, which was the previous behaviour.
* Fixed position of the Popup from the ComboBox. It was sometimes positioned outside the screen.

### 2020.1.2 (5. January 2021)

This release uses a new version of our JavaFX Fork.

* Fixed a rare deadlock during the startup of JPro.
* Fixed a memory leak inside of JavaFX.
* JPro now uses JavaFX 15.0.1 instead of 15.0.0 as it’s default version.
* Added a new experimental feature based on (JMemoryBuddy)[https://github.com/Sandec/JMemoryBuddy].
  We now check every closed application, whether it gets properly collected.
  A list of uncollected applications can be found under `/info/minmemory`.
  All uncollected stages can be found in the HeapDump by searching for the class `AssertCollectableLive`.

### 2020.1.1 (7. December 2020)

#### Features

* JPro now automatically renders Stages with an Owner, as part of the application.
  It works the same way as it previously worked with PopupWindow.
* The class FileHandler in the WebAPI now contains a List of String `filehandler.supportedExtensions`,
  to define the selectable file extension. This is limited to the file chooser and doesn't work with D&D due to
  limitations in the browser.
* Added SystemLoad and JVMLoad to the page `/status`.

### Bugfixes

* Fixed a rare case where the FileHandler wasn't working with Safari.
* PopupWindow and Stages now receive events in the same order as they are rendered.
  Previously sometimes the Window which was rendered in the background got priority over events. This is now fixed.
* Fixed issue with some input events not correctly delivered to the content of the HTMLView.
* Fixed text-align property of the HTMLView. It is now no longer set for the outer div element of the HTMLView.
* Fixed a rare issue with the mouse input for HTMLView. The issue happened when the content of the HTMLView captured the
  mouse event.
* It's no longer possible, in rare situations, to "drag" parts of the application in the browser. This had the effect,
  that mouse events were slightly changed.

### Regression

* With the current version, in some rare cases the mouse-cursor in Safari is wrong.

### 2020.1.0 (19. October 2020)

JPro now supports **JavaFX14** and **JavaFX15**.
JPro now uses JavaFX15 by default.
We no longer support JavaFX8 in the standard versions.

#### Breaking Changes:

* The scripts in the bin folder of the JProReleaseZip now behave differently.
  The `start.sh` and `restart.sh` scripts now start JPro in the foreground.
  The newly added scripts `start-background.sh` and `restart-background.sh start JPro in the background.

#### Feature

* JPro now always renders snapshot properly, without any configuration.
* Added the method `WebAPI.getWebsocketCookies()`. It returns the cookies of the WebSocket connection instead of the
  current browser tab.
  Their contents may differ, for example, due to different domains.
* JPro now properly loads the various logical fonts. In the previous version,
  most italic and bold italic versions were missing.
* The JavaFX version can now be configured in the plugins via the attribute `javafxVersion`in Maven and in Gradle.
  Possible values are `auto`, `latest`, `15`, `14` and `11`. The default value is `auto` which currently uses JavaFX15.

#### Bugfixes

* JPro now supports Gradle 6.6.x
* Fixed deprecations in Gradle to make sure the plugin will work with future releases of Gradle.
* Fixed an exception related to opaque images and mouse events in `QuantumToolkit.imageContains`
* Fixed the cursor in the PasswordField. It's now always positioned correctly.
* Fixed broken optimization for region border.
* Added new scheduling for updating the rendered Scene.
  This fixes some rare rendering of incomplete frames that sometimes felt like stuttering.

## 2019.2.X

### 2019.2.7 (13. August 2020)

#### Feature:

* New Cookie API!
  We've added the methods `setCookie()` and `deleteCookie()` to easily save and delete cookies.
  `getCookies` now behaves differently. It's now an observable map and contains the cookies of the browser page instead
  of the websocket connection.
  The map gets updated after using `setCookie()` or `deleteCookie()`.
* Changed the default for `fxContextMenu` in the JPro Tag.
  By default, instead of the browser Context-Menu, the JavaFX Context-Menu is used.

#### Bugfixes

* The way the `WebAPI.downloadURL()` works was changed. It's now simpler and fixes a bug with the Firefox Version 78.
* We changed the way Cursors were set through Scene or Dragboard.
* We added an info message to the start script in JProRelease to inform the user,
  that the process is starting in the background.

### 2019.2.6 (21. July 2020)

#### Bugfixes:

* Fixed a bug with mouse input. In some situations the special-keys were not set in the MouseEvents.
* Fixed a memory leak in the javascript client.
* When using `loaderURL` in the JProTag the loader was not centered. This is now fixed.
* Firefox: Fixed a regression with the file upload.
  It was only possible to upload files in a domain+port after opening a popup on firefox. This is now fixed.
* Safari: The loading animation of JPro was stuttering in Safari. This is now fixed.
* Safari: Canvas can no now longer be selected with ctrl+a.

### 2019.2.5 (30. June 2020)

#### Features:

* BoxShadows! JPro now uses box-shadows when possible.
  This dramatically improves the performance of shadows.
* Added the
  method [openURL](/api/2022.1.0/com/jpro/webapi/WebAPI.html#openURL(java.lang.String)), [openURLAsTab](/api/2022.1.0/com/jpro/webapi/WebAPI.html#openURLAsTab(java.lang.String))
  and [openURLAsPopup](/api/2019.2.5/com/jpro/webapi/WebAPI.html#openURLAsPopup(java.lang.String)) to the WebAPI.
* It's now possible to define an own loading animation as a gif. Just set the attribute `loaderURL` of the JProTag.

#### Bugfixes:

* Fixed a bug in the Maven plugin.
  When executing the command `mvn jpro:run` followed by the command `mvn package`, the changes done between the two
  calls were not correctly registered.
* Fixed a bug related to cursor selection with Safari. In some situations the `select- `cursor was wrongly overlying
  text-elements.
* Fixed a bug related to a corner case using the clip property.
* Fixed a regression related to mouse-events. It broke the correct sorting of columns in the TableView.
* Fixed a bug in the attribute `disableShadows` for the JProTag.

### 2019.2.4 (2. June 2020)

#### Features

* Added the Method `getHeaders` to the WebAPI.
  It makes all the HTTP-Headers provided to the WebSocket connection accessible.
* Reworked Shadows. The new implementation works reliably in all browsers.

#### Bugfixes:

* The method `WebAPI.executeScript` no longer serializes the result of the provided javascript code.
  Only `WebAPI.executeScriptWithListener` and `WebAPI.executeScriptWithReturn` are now serializing the result.
  This avoids unnecessary exception due to unserializable results.
* Fixed a rendering bug happening with Chrome.
* Fixed a bug related to HTMLView. In some situations it was not possible to focus elements inside an HTMLView.
* In some situations, the HTMLView couldn't get MouseEvents. This is now fixed.
* Fixed an issue with MouseInput when JPro was embedded into another JProApplication using an HTMLView.
* Fixed a bug with Canvas when using Edge.

### 2019.2.3 (20. April 2020)

#### Features

* MouseEvents are now also generated while dragging an element outside the Browser.
  This is especially important when dragging the ScrollBar of a ScrollPane. It no longer hangs when leaving the browser.

#### Minors:

* Improved the support for JPro being embedded into an iframe.

### Bugfixes

* Dotted lines in Regions are now rendered correctly with the new rendering engine.
* Fixed a bug related to uploading files using the WebAPI.
  It only happened when the server was running on Windows and the client was Edge.
* Fixed TextInput for IPads with the latest version of IPadOS.
* ImageView is now rendered correctly when the image is `null`.
* Fixed a rendering regression in Chrome.
* Fixed a rendering bug in Chrome.
* Fixed a rendering bug related to clip in Safari.

### 2019.2.2 (4. February 2020 )

#### Features

* Gradients, Images and Effects now implemented for Canvas, as well.

#### Minors:

* The WebAPI now supports a method (`WebAPI.setLossless(image,false)`) to mark an image which can transferred with a
  lossy compression.

#### Bugfixes

* Fixed a rare rendering bug. In some situations border/background of a region was rendered above its children.
* Fixed a rare rendering bug related to clips. In some situations some browsers didn't render the DOM correctly. These
  situations are now avoided.
* Fixed a rare rendering bug related to clips. In some situations the clip wasn't applied properly.
* Fixed a rendering bug which happened on Chrome when the users zoomed.
* Fixed `fxcontextmenu=true` for the JProTag. It was broken with the new rendering engine.
* Fixed an exception in the browser when rendering a `javafx.scene.text.Text` element with null as the value for the
  text.
* Fixed an exception in the browser when rendering a `javafx.scene.text.Rectangle` with an infinite expansion.
* Fixed the hover property in the FileHandler of the WebAPI.
* Fixed the "image drag problem" on Safari.
* Added a minor performance improvement.

### 2019.2.1 (23. December 2019)

### Minors:

* Canvas now supports the methods `drawImage` and `setGlobalAlpha`.
* We've backported the CSS-performance-improvements done to JavaFX to our JavaFXFork.
* The ByteBuffer of 2D images are now deleted when no longer needed. It can be deactivated, though, by the following
  line in the jpro.conf: `jpro.deleteBufferOfImage=false`

#### BugFixes

* Fixed a bug in the Canvas implementation. In some situations, Canvas elements were rendered allthough not needed.
* Fixed a bug in the gradle plugin.
  When using the command `gradle jproRun`, in some rare situations, two jar files with different javafx-versions were
  added to the classpath.
* Fixed a bug related to the rendering of glyphs with our new rendering engine. The bug occurred when using
  FontAwesomeFX.
* Fixed a behaviour bug which occurred when `userSelect` was set to active. The newline-character is now copied
  correctly with the rest of the text.
* Elements of type ImageView can no longer be selected in the browser. We disabled it because the selection caused an
  unwanted blue effect.

### 2019.2.0 (4. December 2019)

#### Majors:

* **CANVAS SUPPORT**!
  Features not yet implemented for Canvas: Gradients, Images and Effects.

* New generation rendering engine (with Canvas support)! Performance Improvements for new engine will follow soon!

#### Minors:

* Google indexing is now working.
  The problem was, the Google crawler claimed to support WebSocket. But, it took a while until we realized, this was not
  the case. We have now solved it differently.

#### Bug fixes:

* Fixed exception for the case that an application was opened without an initial Scene.
* Fixed exception for the case that a WebAPI.requestLayout(Scene) was called with a Window with no Scene attached to it.
* Fixed a bug in the Maven plugin.
  When using the command `mvn jpro:run`, in some rare situations, wrong jars were added to the classpath.

## 2019.1.X

### 2019.1.3 (24. September 2019)

#### Improvements:

* Major performance-improvement for the javascript-client.

#### Bug fixes:

* Fixed a bug with the SecurityManager in JPro, which prevents `System.exit` to shut down the whole server.
  The bug had the effect, that the new api for Java11 java.net.http` didn't work properly. It probably also affected
  other libraries.
* Fixed a bug with the [FileUploader](https://www.jpro.one/api/2023.3.1/com/jpro/webapi/WebAPI.FileUploader.html).
  There was a problem related to multiple uploads with the same filename. It caused an Exception to be thrown. This is
  now fixed.

### 2019.1.2 (11. September 2019)

#### Features:

* Added the property `selectedFileSize` to the [FileUploader](https://www.jpro.one/api/2023.3.1/com/jpro/webapi/WebAPI.FileUploader.html).
* Added the attribute [timeUntilReconnect](#embedding-jpro) to the JPro tag. It specifies after how much
  time the client tries to reconnect when he didn't hear anything from the server.

#### Bug fixes:

* Fixed a performance regression that was introduced in 2019.1.0. It has a significant impact when many nodes are
  serialized in one and the same frame.
* Eliminated the throwing of a superfluous exception. The text of the exception was like the
  following: `Popup cannot be cast to JavaFX.stage.Stage`
* [#29](https://github.com/JPro-one/JPro-tickets/issues/29) Fixed a bug appearing when using JPro with Firefox. When the
  application was not in fullscreen, a node with effects was not rendered.
* Fixed a bug when using the MavenPlugin.
  Maven was downloading the artifacts which are required for the command `mvn jpro:release`,
  even when this command was not called.

### 2019.1.1 (17. June 2019)

#### Features:

* Added the methods
  [openLocalResource](/api/2022.1.0/com/jpro/webapi/WebAPI.html#openLocalResource-java.lang.String-) and
  [openLocalURL ](/api/2022.1.0/com/jpro/webapi/WebAPI.html#openLocalURL-java.net.URL-) to the
  [WebAPI](/api/2022.1.0/com/jpro/webapi/WebAPI.html).
  They can be used to open files in a new tab, for example pdf-files.

#### Bug fixes

* In the JPro renderer, reduced CPU usage by about 10%. Before this fix JPro could allocate upto 10% of the local CPU at
  time when it should actually be idle.
  Now, no relevant processing power is used when no changes are happening in the scene-graph.
* Fixed a rare bug, when opening two applications at once, sometimes one instance did not start properly.
* Sometimes, after reconnecting, the width or height of the application was wrong. This is now fixed.
* Fixed a bug when changing the Scene of a Stage. Now, the Scene gets properly relay-outed to the size of the
  JProElement.
* Fixed a rare bug for JavaFX8 which in some rare occasions could cause the text input for a running session to stop
  working.
* Gradle: Fixed a bug in the Gradle plugin, the JavaFX-Fork was added to the compile dependencies.
* Maven: Fixed a bug, which prevented JPro from working when using JavaFX11 and Maven.
* Maven: Fixed the command `mvn jpro:release` for Maven. Now the proper files are added, which are required to run JPro
  on Linux.

### 2019.1.0 (28. May 2019)

This release by default uses a forked version of JavaFX11.
JPro will still work with JavaFX8, but we recommend switching to Java(FX)11.
Some new JPro features are restricted to JavaFX11 and higher.

**We highly recommend switching to this new release `2019.1.0`,**
because previous versions were using an experimental version for Web Components,
which will not be supported by Chrome much longer.

#### Features for the forked JavaFX11

* JPro now supports the method **snapshot** from Node.
* Drag-view and Drag events are now supported in JPro.
  For now, they are restricted to work inside the JavaFX application, they can not interface with other applications.
* When calling the method showAndWait, it no longer leads to a freeze of the JavaFX Thread. It does not mean JPro
  supports showAndWait calls, it just constraints their negative side effects. ShowAndWait calls now throw an exception
  when using JPro.

#### Big features:

* For Linux, we now use different default fonts, because the Lucida fonts were removed from the OpenJDK, which resulted
  in various problems during deployment.
  Now they have been replaced by the fonts Roboto, Roboto Mono and Roboto Slab, which are licensed under the Apache
  License 2.0.

* Significant Performance improvements, especially when showing a lot of nodes for the first time. The time needed for
  rendering the initial scene graph was reduced by 30%.

* Updated the API version of the WebComponents.
  We highly recommend updating to this JPro version `2019.1.0`, because the old WebComponents API was experimental and
  will stop working on some browser soon.

* It's now possible to open **new Stages** as new tabs or popups. For this purpose, we've added the
  method `openStageAsPopup(Stage stage)` and `openStageAsTab(Stage stage)` to the WebAPI.

* Added the method `runAfterUpdate` to the WebAPI.
  This method enables for incremental loading of the scene graph, which can be used to improve the user experience.

* Added the method `getWebAPI(Node node, WebAPIConsumer consumer)` to the WebAPI.
  It can be used to access the WebAPI from a node, instead of a stage.

* JPro now supports Java12. New upcoming Java releases will now automatically work when there are no breaking change.

#### Small Features

* The JavaDoc and the source code of the WebAPI are now published as Maven artifacts. This should improve tooling for
  IDEs. The JavaDoc has now got richer content.
* Added the field `JPro build time`, containing a timestamp for the JPro build, to the info block returned by
  the `/status` command.
* Added a new favicon for the internal pages.

#### Bug fixes

* Fixed a rendering issue with Pie Chart. It happened to Regions with (a) width and height property equal zero and (b)
  with a shape.
* `<script>` tags in HTMLView are now being executed.
* Fixed the path for the heap dumps, which were temporarily created when downloading the current heap dump.

## 2018.1.X

### 2018.1.14 (15. May 2019)

**JPro** fixes:

* JPro works now with the latest version of Java8 `1.8.0_212`.

### 2018.1.13 (10. April 2019)

**JPro** features:

* The `/status` page as well as the JPro start and opening now lists the
  JavaFX version used.
* Improved the log information produced at JPro start.

**JPro** fixes:

* Mouse events are now generated while dragging a file from outside the
  browser into the JPro session inside the browser.
* Eliminated some rare-throwing of **NullPointerExceptions**.

**Gradle** and **Maven** Plugin fixes:

* When using `gradle jproRelease` or `mvn jpro:release` on Java11, now by
  default, the JavaFX version 11.0.2 is used.

### 2018.1.12 (17. March 2019)

**JPro** features:

* The processing of user input, mainly relevant for slow event listeners, was performance optimized. The new behavior is
  closer to the behavior of JavaFX on the desktop.
* Changed the naming-pattern for logfiles. The new pattern is "logs/jpro.$level.log" instead of "
  logs/application.$level.log".

**JPro** fixes:

* The blinking behavior of the Caret in TextFields and TextAreas now behaves like on the desktop. It stops blinking for
  a short time, after typing.
* Key events for TextFields and TextAreas are now consumed as on the desktop. They are consumed when the objects are
  focused. Before this fix, when pressing SPACE in a focused TextField in a ScrollPane, a non-expected scroll down was
  executed.
* The `/status` page has gone through a cleanup regarding names and formatting.
* Fixed a bug on mobile chrome. On a touch, when the event target was removed shortly after touching down, then the
  touch release was not fired.
* Fixed a bug on mobile. On a long press, sometimes a release event was fired without actually releasing.
* Fixed a very rare bug, which could cause the text input to stop working.

### 2018.1.11 (11. February 2019)

**JPro** features:

* The page `/status` now uses mB instead of kB to display memory usage.

**JPro** fixes:

* Fixed a bug, which had the effect, that JPro didn't start properly with Java 1.8.0_202.
* Fixed a bug, which could happen on iOS devices. It sometimes caused the screen to darken on touch events.
* Fixed a regression from 2018.1.10, the property `userSelect` of the <jpro-app> tag didn't work properly.
* Fixed a regression from 2018.1.10, the file upload when using the WebAPI didn't work properly.

**Gradle** and **Maven** Plugin fixes:

* Files explicitly added to the jproRelease zip, were added as a root element of the zip.
  They are now added as an element of the folder of the application.

### 2018.1.10 (7. January 2019)

**JPro** features:

* JProRelease: It's now possible to add additional files to the zip-file generated by `gradle jproRelease`
  or `mvn jpro:release`.
  It's documented [here](#configuring-jpro).

* We added a development mode to the JPro server.
  It is activated when the server is started from gradle/maven.
  The production mode is activated when the server is started by a zip, created with `gradle jproRelease`
  or `mvn jpro:release`.
  Pages like `/status` or `/test/appname` are now only accessible **without** username/password, when the development
  mode is active.
* We added a default-page for the JPro-server.
  When the resource `jpro/html/index.html` is unavailable as the path `<servername>/` is opened, the content
  of `test/fullscreen/default` is shown.
  The default `openingPath` for gradle/maven is now `/`.
* A small memory-leak was fixed in the JPro Renderer (the JPro component running inside the browser).

**JPro** fixes:

* The HTMLView was sometimes still rendered when the HTMLView or one of its children was not visible. This is now fixed.
* Chrome: When the HTMLView was rendered outside the visible area, sometimes the scrollable height of the page was
  changed.
  This is now fixed.

**Gradle** and **Maven** Plugin fixes:

* (see above) It's now possible to generate files with `gradle jproRelease` and `mvn jpro:release`.add and then to add
  them to the zip.
* Fixed regression in the script `bin/stop.sh`.
  It was not deleting the file `RUNNING_PID`, when the process didn't exist. This is now fixed.

### 2018.1.9 (26.November 2018)

**JPro** fixes:

* Added some printouts during JPro startup:
  Any errors coming from the javafx initialization process (most
  relevant for running a Linux server in production),
  the JPro-Version,
* Added a warning when a font file with the extension `.ttc` is used.
  The warning is important, because `.ttc`-files are not supported in the
  browsers.

* Fixed a regression in 2018.1.8. In 2018.1.8 uploaded files, after a
  certain amount of time, were no longer accessible.

**Gradle** and **Maven** Plugin fixes:

* When creating a release with `gradle jproRelease` or `mvn jpro:release`,
  the script `start.sh` was not supporting spaces for the
  JVM-Arguments. This has now been fixed.

**Maven** Plugin fixes:

* It's no longer required to explicitly add `compile` when using `mvn jpro:run`
  or `package` when using `mvn jpro:release`.
  The new valid command are:
  `mvn jpro:run` and
  `mvn jpro:release`

  We apologize for an error in our previous DOC-page, which until now
  had the wrong syntax; it should have been `mvn package jpro:release` and
  not `mvn compile jpro:release`. But, in any case, as here stated, since
  2018.1.9 this is no longer relevant.

* There was a wrong leading text in the info/status. It was saying
  `GRADLE-Distribution` instead of `MAVEN-Distribution`. This has now
  been fixed.
* As the start.sh file was generated, it had some wrong classpath in
  it, which were referring to files in the development environment.
  This had no effect, but was confusing and not clean. They are now removed.
* A build created with `mvn jpro:release` for JavaFX11 contained some
  jars, which are not required by JavaFX11. Those have now been eliminated
  for the JavaFX11 build.
* The JVMArgs provided in the `pom.xml` for the JVM were not correctly
  supported. They now are.

### 2018.1.8 (12.November 2018)

**JPro now supports Java/JavaFX 11!**

**JPro** fixes:

* The javascript file for JPro is now 35% smaller than the previous one.
* When Setting the attribute `nativescrolling` for the JProTag, it no longer implicitly sets `fxHeight` to true.
* A bug was fixed, that a HTMLView in a Popup was still rendered although the popup was closed.

Fixed for the **Gradle** and for the **Maven** Plugin:

* Added the property `useFontConfig`. The default value is `false`.
  Until now, JPro implicitly disabled the library with the name fontConfig, but with `useFontConfig` the activation of
  fontConfig was made configurable.
* When creating a release with `gradle jproRelease` or `mvn package jpro:release`, whitespaces in the directories are
  now handled correctly.
* When creating a release with `gradle jproRelease` or `mvn package jpro:release`, the start and restart script now
  passes its arguments to the JVM as JVM-arguments.

Fixes for the **Gradle** Plugin:

* Fixed a bug in the gradle-plugin. The command `gradle jproRelease` now makes sure, that when no longer up to date, a
  new jar is generated.

Fixes for the **Maven** Plugin:

* Added the command `mvn package jpro:release` to the maven plugin. The maven plugin now supports all gradle features.
* Fixed a bug in the command `mvn compile jpro:run`, now it behaves the same way as the corresponding gradle command.
  When the file RUNNING.PID still exists, the corresponding process is killed and the file is deleted.

### 2018.1.7 (22.October 2018)

**JPro** fixes:

* On Edge and IE11, the caret of the hidden input-field is no longer visible.
* Added the attribute `setPrintJSCommands`to the JProTag. When true, all js-commands executed through the WebAPI are
  logged on the browser console.
  Documented in the chapter [EMBEDDING JPRO](#embedding-jpro).
* Small reduction of the js-file by about 15%.
* A regression on mobile/iOS related to the text-input.
* A bug was fixed on the IE11, that sometimes image resources were not loaded correctly.
* A bug was fixed, that a font could not be loaded when it’s path contained a '+'-sign.

### 2018.1.6 (1. October 2018)

**JPro** fixes:

* A memory-leak could happen inside of JavaFX, when a node was removed from the scene-graph while the rendering was
  disabled. The memory is now released when the related node is no longer used, instead of at the end of a session.
* The MouseEvent methods `isAltDown()`, `isControlDown()`, `isMetaDown()` and `isShiftDown()` did not return the correct
  value and were now fixed.
* The field `Views afk` is now added to the URL `<servername>/status`. A view is treated as afk, when there was no
  user-input during a period of one minute.
* A new property was added to the `jpro.conf` to allow for logging all access to any files located under the resource
  path `jpro/html`. It is activated by adding the `jpro.logResourceAccess = true` to the `jpro.conf`.
* A new property was added to the `jpro.conf` to allow for logging user input events. It is activated by adding
  the `jpro.logUserInputEvents = true` to the `jpro.conf`.
* On iOS Safari it could happen, that touch generated unwanted double click events. This bug has now been fixed.
* On iOS Safari it could happen, that touch events got lost. This bug has now been fixed.
* Under special conditions it could happen, that ImageView did not render correctly. It could happen with
  backgroundLoading set to true. This bug has now been fixed.
* When using the WebAPI for downloading files, some file types used to open in the current tab. This has now been
  changed. Now all files are downloaded directly.
* We now use GZip for the download of all javascript files. This greatly increases the performance for initial
  sessions (before the browsers starts caching it).

Fixes for the **Gradle** Plugin:

* The value of `deployment` at `<servername>/status` when using `gradle jproStart` or `gradle jproRestart` was wrong.
  This bug has now been fixed.

Fixes for the **Maven** Plugin:

* A nullpointer-exception could be generated when calling `mvn compile jpro:stop`. This bug has now been fixed.

### 2018.1.5 (23. July 2018)

* Maven : Added an experimental version for a
  MavenPlugin. [Check out the Maven-Helloworld!](https://github.com/JPro-one/HelloJPro-Maven)
* WebAPI: Fixed fil-upload through file-drop in FireFox.
* WebAPI: Fixed the behaviour for fileHover.
* JPro  : Fixed the performance of `Node.setClip`. The implementation is now fast and correct.
* JPro  : Fixed a rare exception in the javascript-client.
* JPro  : Added information about the deployment-method (`gradle jproRun`, `gradle jproRelease`, `mvn compile jpro:run`)
  to `<servername>/status`.
* GRADLE: Fixed a bug in `gradle jproRun`. The server now always terminates after stopping gradle.

### 2018.1.4 (3. July 2018)

* JPro  : Improved rendering when using `Region.setShape`.
* JPro  : Fixed a rendering-issue related to `MediaView` without a `MediaPlayer`.
* JPro  : Fixed some issues when using `Node.setClip`. This fix especially fixes the behaviour of the
  JFoenix-class `JFXButton`.
* JPro  : Fixed wrong rendering, when `Node.setRotate` is used in combination with `Node.setScaleX` or `Node.setScaleY`.
* JPro  : Significant performance-improvements for SVGPath for both the server and the browser.
* JPro  : Significant performance-improvements in the browser.
* JPro  : Fixed regression from the version 2018.1.3, which could crash a session in the Internet Explorer / Edge.
* JPro  : Fixed js-exception in Internet Explorer / Edge. This improves the behaviour on Internet Explorer / Edge.
* JPro  : Fixed DropShadow sometimes being cut-off.
* JPro  : Added workaround for side effects by adding a listener to the layoutBounds of a Group.
* JPro  : Fixed positioning of Popups with Shadows.
* JPro  : Fixed positioning of Popups without autofix.
* JPro  : Fixed rare race-condition in the rendering, which could have the effect of a temporary memory-leak.

### 2018.1.3 (4. June 2018)

* JPro  : Significant performance improvements. The SVG-Dom is now much smaller.
  Region is now painted faster, which especially benefits large business-applications.
* JPro  : Fixed screen-mouse-position for various events.
* JPro  : Added a workaround for a rare bug, related to wrong popup-positions.
  It is activated by default. It can be deactivated in jpro.conf with the following
  statement: `jpro.workaroundWindowPosition = false`.
* JPro  : Fixed bug related to HTMLView, under some conditions the visible-attribute wasn't updated correctly.
* JPro  : Fixed a rare bug related to TextFlow, which breaks the rendering and causes a NullPointerException.
* JPro  : Fixed a bug, which caused too many MouseEnter/MouseLeave events.
* JPro  : Fixed a race-condition, which had the effect, that the JavaFX-Context-Menu isn't shown.
* JPro  : When resizing the jpro-tag in the browser, the stage of the javafx-app is now also resized (previously only
  the scene was resized).
* JPro  : TextFlow with Nodes with `managed = false` are now rendered correctly.
* JPro  : Updated to Play Framework 2.6.13.
* JPro  : Added more information to `/status`.
* JPro  : Fixed a bug, where the logfiles couldn't be accessed in the browser, when the server had an uncommon
  default-encoding.
* JPro  : Added a workaround for a small memory-leak in JavaFX. It can be deactivated in the jpro.conf by the following
  line: `jpro.gcWorkaroundStage = false`.

### 2018.1.2 (19. April 2018)

* ***Added Support for Java10!***
* JPro  : When browser is resized fast and the server cannot catch up, the outdated resizing is now skipped.
* JPro  : fixed wrong clipping, when using the JPro-tag-attribute: scaling
* JPro  : Fixed an exception in the browser related to HTMLView and SVGView. They didn't have any symptoms
* JPro  : added error-message, when initialization of JPro doesn't terminate
* GRADLE: Fixed `jproRelease` on a clean build
* GRADLE: For the tasks `jproStart` and `jproRestart`, The console-output of JPro-process is now printed, until the port
  is opened
* GRADLE: On startup-failure, the exit-code is no longer printed in a loop
* WebAPI: fileDragOver is also updated, when selectFileOnDrop is not true
* WebAPI: added the property `selectFileOnDrop` to `FileHandler`, previously it was implied by `selectFileOnClick

### 2018.1.1 (4. April 2018)

* Improved error-message, when a file couldn't be found in the package jpro/html
* Fixed a bug, which can cause wrong event-positions. This was likely to happen in combination with ScrollPane
* Fixed Double-Clicks on mobile browsers
* Reworked how `WebView` and HTMLView` is working, it's implementation is now much simpler
* WebAPI: Fixed bug in `FileHandler`, uploading the same file twice now works properly
* WebAPI: Improved FileHandler, there is now an `onFileSelected`-event, and a new property `fileDragOver`

### 2018.1.0 (13. March 2018)

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
  But it currently doesn't work with the Charm library, specifically when the
  class [MobileApplication](https://docs.gluonhq.com/charm/javadoc/4.3.3/com/gluonhq/charm/glisten/application/MobileApplication.html)
  is used.

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

* It's most likely related to the use of static variables. In JPro, static variables are shared between multiple
  sessions. Therefore, variables declared as static become global to all sessions. This fact can cause problems. BUT,
  depending on how you use it, it can also be utilized as a welcomed feature.

```
My application slows down over time. After a while it some times even crashes. What could be the reason for such a behaviour?
```

* A common reason for this behaviour is a memory leak in your application.
  You can use tools like [VisualVM](https://visualvm.github.io/) to solve the issue in your application.

```
How can I use a IDE for my JPro-project?
```

The HelloWorld-Project is a simple gradle/java project, which can be imported by intellij or eclipse without any
modifications.

# SUPPORT

## SUPPORT

Feel free to contact us at `info@jpro.one` for commercial support or any other related topic.

## What if I find bugs?

Should you find bugs in jpro, please inform us about any details through our
[jpro bug-tracker](https://github.com/JPro-one/jpro-issues).

# Links

## [JavaFX](https://openjfx.io/)

## [Ticket System](https://github.com/JPro-one/JPro-tickets)

## [JPro Samples](https://github.com/JPro-one/JPro-Samples/)

## [JavaFX Version 21 API](https://openjfx.io/javadoc/21/index.html)

## [JavaFX Version 17 API](https://openjfx.io/javadoc/17/index.html)

## [JavaFX Version 11 API](https://openjfx.io/javadoc/11/index.html)

## Related projects

* [QF-Test](https://www.qfs.de/en/product/qf-test/java-testing/javafx.html) A commercial tool to test your JavaFX/JPro
  Application.
* [ControlsFX](https://github.com/controlsfx/controlsfx), a community library managed by
  [Jonathan Giles](https://jonathangiles.net/) and
  [Gluon](https://gluonhq.com/), with a set of controls. In 2017, it received the
  [Duke Choice Award](https://www.oracle.com/java/2017-dukes-choice-awards.html) for its awesome work.
* [Gluon's](https://gluonhq.com/) useful Java technologies, including
  the [Gluon Mobile](https://gluonhq.com/products/mobile/) library.
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
* [Almas Baimagambetov](https://almasb.github.io/) [on GitHub](https://github.com/AlmasB), with cool games, tutorials
  and examples.
