# GETTING STARTED

## RUN JPRO LOCALLY

### Using Gradle
The easiest way to get started, is to use **Gradle** as build tool.
JPro provides a plugin for Gradle,
which allows you to easily start JPro from an existing project, 
which is obviously rather practical during the development process.

Currently, JPro supports Gradle in the versions 2.x, 3.x and 4.x. We suggest to use 4.x.

As a simple reference project, you could take a look at the simple [hello-world-gradle](https://github.com/JPro-one/HelloJPro) 
and you can [run it online](https://demos.jpro.one/helloworld.html).

Our public **ticket system** can be found on [github](https://github.com/JPro-one/JPro-tickets). 

[Here](https://github.com/JPro-one/JPro-Samples/) you can find some easy and useful samples.

To get started and run your first app with JPro, you should execute the following **4 steps**:

    * Install Gradle
    * Create the Gradle script
    * Create the JPro configuration file
    * Run the app 


#### Step `1`. Install Gradle
 
Gradle can be downloaded and installed [here](https://gradle.org/install/). 


#### Step `2`. Create the Gradle script 
 
Create the file `build.gradle` and put it into your **project's root directory**.  
You can either download a template file [here](https://raw.githubusercontent.com/JPro-one/HelloJPro/master/build.gradle) or just use the following:

```groovy
buildscript {
  repositories {
    jcenter()
    maven {
      url "http://sandec.bintray.com/repo"
    }
  }

  dependencies {
    classpath 'com.sandec.jpro:jpro-plugin-gradle:2019.1.0'
  }
}

repositories {
  jcenter()
}

apply plugin: 'com.sandec.jpro'

mainClassName = 'your.class.Name'

jpro {
  port = 8080
}
```

#### Step `3`. Create the JPro configuration file 

This file is configured in [HOCON (Human-Optimized Config Object Notation)](https://github.com/lightbend/config/blob/master/HOCON.md), 
which is a superset of JSON, and is optimized for writing configurations.


The `jpro.conf` must be placed into the directory `<project-dir>/src/main/resources`.

You can either download a **template file** 
[here](https://raw.githubusercontent.com/JPro-one/HelloJPro/master/src/main/resources/jpro.conf) or just use the following:

```groovy
jpro.applications {
  "myApp" = com.jpro.somepackage.SomeMain
}
```

Make sure you use the same name specification for the `<jpro-app>` tag in the `index.html`, like 

```groovy 
<jpro-app href="/app/myApp" fullscreen="true"></jpro-app>
```

***TODO***

#### Step `4`. Run the app 

Start a **Terminal session**, move to the **main project directory** and enter the command:

```groovy
./gradlew jproRun
```

Now you should see your app running inside of your standard browser.



### Using Maven
JPro provides a plugin for Maven,
which allows you to easily start JPro from an existing project, 
which is obviously rather practical during the development process.

Currently, JPro supports Maven in the versions 3.5. We suggest to use 3.5.x.

As a simple reference project, you could take a look at the simple [hello-world-maven](https://github.com/JPro-one/HelloJPro-Maven/) 
and you can [run it online](https://demos.jpro.one/helloworld.html).

Our public **ticket system** can be found on [github](https://github.com/JPro-one/JPro-tickets). 

To get started and run your first app with JPro, you should execute the following **4 steps**:

    * Install Maven
    * Create the Maven script
    * Create the JPro configuration file
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

    <groupId>com.sandec.jpro</groupId>
    <artifactId>hellojpro-maven</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <properties>
        <jproVersion>2019.1.0</jproVersion>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <name>Hello JPro!</name>
    <url>https://www.jpro.one/</url>

    <build>

    <plugins>

      <plugin>
          <groupId>com.sandec.jpro</groupId>
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
          </configuration>
      </plugin>

    </plugins>
    </build>

    <pluginRepositories>
        <pluginRepository>
            <id>jpro - sandec repository</id>
            <url>http://sandec.bintray.com/repo</url>
        </pluginRepository>
    </pluginRepositories>

    <repositories>
        <repository>
            <id>jpro - sandec repository</id>
            <url>http://sandec.bintray.com/repo</url>
        </repository>
    </repositories>



    <dependencies>
        <dependency>
            <groupId>com.sandec.jpro</groupId>
            <artifactId>jpro-webapi</artifactId>
            <version>${jproVersion}</version>
            <scope>compile</scope>
        </dependency>
    </dependencies>



</project>
```

#### Step `3`. Create the JPro configuration file 

This file is configured in [HOCON (Human-Optimized Config Object Notation)](https://github.com/lightbend/config/blob/master/HOCON.md), 
which is a superset of JSON, and is optimized for writing configurations.


The `jpro.conf` must be placed into the directory `<project-dir>/src/main/resources`.

You can either download a **template file** 
[here](https://raw.githubusercontent.com/JPro-one/HelloJPro/master/src/main/resources/jpro.conf) or just use the following:

```groovy
jpro.applications {
  "myApp" = com.jpro.somepackage.SomeMain
}
```

Make sure you use the same name specification for the `<jpro-app>` tag in the `index.html`, like 

```groovy 
<jpro-app href="/app/myApp" fullscreen="true"></jpro-app>
```

*** TODO ***

#### Step `4`. Run the app 

Start a **Terminal session**, move to the **main project directory** and enter the command:

```groovy
mvn jpro:run
```

Now you should see your app running inside of your standard browser.



## RUN JPRO REMOTELY


### Using Gradle

#### Step `1`. Prepare your server

To run JPro on linux, the server must be configured correctly.

Checkout the following chapters to configure your server correctly for JPro:

[DEPLOYING JPRO](/?page=docs/current/2.6/DEPLOYING_JPRO)
 
[PREPARING LINUX FOR JPRO](/?page=docs/current/2.7/PREPARING_LINUX_FOR_JPRO)

#### Step `2`. Create the binary

Create a zip which contains the application with the following command:
```groovy
./gradlew jproRelease
```

The path of the zip-file is the following: `build/distributions/<app-name>-jpro.zip`

Now copy this file to your Server and unzip it.

#### Step `3`. Run JPro

In the unzipped folder you can find a start-script: `bin/start.sh`

By running `./bin/start.sh` you start the JPro Server on your server. 

The JPro Server is now ready to serve your URLs entered in your browser.

```bash
./bin/start.sh
```


### Using Maven

#### Step `1`. Prepare your server

To run JPro on linux, the server must be configured correctly.

Checkout the following chapters to configure your server correctly for JPro:

[DEPLOYING JPRO](/?page=docs/current/2.6/DEPLOYING_JPRO)
 
[PREPARING LINUX FOR JPRO](/?page=docs/current/2.7/PREPARING_LINUX_FOR_JPRO)

#### Step `2`. Create the binary

Create a zip which contains the application with the following command:
```bash
mvn jpro:release
```

The path of the zip-file is the following: `target/<app-name>-jpro.zip`

Now copy this file to your Server and unzip it.

#### Step `3`. Run JPro

In the unzipped folder you can find a start-script: `bin/start.sh`

By running `./bin/start.sh` you start the JPro Server on your server. 

The JPro Server is now ready to serve your URLs entered in your browser.

```bash
./bin/start.sh
```



## CREATE A PROJECT 

The easiest way to setup a new JPro project for your apps is to use the **HelloJPro** project as your base,
for then to make some small adaptions to it.  This chapter will show you what you need to do if you 
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
As a JPro session gets startet, it will look for this app name inside of the resource file called `jpro.conf`.

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

Now you are done and can run your `myApp`, by simply providing the command

, if you use Gradle:
```groovy
./gradlew jproRun
```
or

```groovy
gradle jproRun
```

, and if you use Maven:
```bash
mvn jpro:run
```

from the **main project directory** in your terminal window.  

See Step 4 of the 
[RUN JPRO LOCALLY](/?page=docs/current/1.1/RUN_JPRO_LOCALLY/Using_Gradle/) and 
[JPRO GRADLE COMMANDS](/?page=docs/current/2.1/JPRO_COMMANDS/Using_Gradle/) 
for more details about how to run an app with `Gradle`.  
See Step 4 of the 
[RUN JPRO LOCALLY](/?page=docs/current/1.1/RUN_JPRO_LOCALLY/Using_Maven/) and 
[JPRO MAVEN COMMANDS](/?page=docs/current/2.1/JPRO_COMMANDS/Using_Maven/) 
for more details about how to run an app with `Maven`.  See
[CONFIGURING JPRO](/?page=docs/current/2.2/CONFIGURING_JPRO) 
for more detailed information about `jpro.conf`.


### Starting an app from build.gradle 

The `build.gradle` file of the HelloJPro project can be downloaded
[here](https://github.com/JPro-one/HelloJPro/blob/master/build.gradle).  It looks like the following:

```
/**
 ******************  Script Configuration ******************
 */
buildscript {
  repositories {
    jcenter()

    maven {
      url "http://sandec.bintray.com/repo"
    }
  }

  dependencies {
    classpath 'com.sandec.jpro:jpro-plugin-gradle:2019.1.0'
  }
}


/**
 ******************  Java Configuration ******************
 */
apply plugin: 'java'
apply plugin: 'application'

compileJava {
  sourceCompatibility = 1.8
  targetCompatibility = 1.8
}

repositories {
  jcenter()
}

dependencies {
// Add your dependencies here, for example:
// compile group: 'org.controlsfx', name: 'controlsfx', version: '8.40.14'
}

/**
 ******************  jpro Configuration ******************
 */
apply plugin: 'com.sandec.jpro'


/**
 * App Main Class
 */
//mainClassName = 'com.jpro.hellojpro.HelloJPro'
mainClassName = 'com.jpro.hellojpro.HelloJProFXML'

/**
 * jpro settings
 */
jpro {
  // for debugging
  // JVMArgs << '-agentlib:jdwp=transport=dt_socket,server=n,address=5006,suspend=y'

  JVMArgs << '-Xmx1000m'

  //jpro server port
  port = 8080

  //jpro version (optional)
  jproVersion = "2019.1.0"

  openingPath = ""
}
```

If the JPro starter does not find any maching name in the `jpro.conf`, then it will look 
for a specified `mainClassName` in the `build.gradle` to be started instead.


### Starting an app from pm.xml(Maven) 
The `pom.xml` file of the HelloJPro project can be downloaded
[here](https://github.com/JPro-one/HelloJPro-Maven/blob/master/pom.xml).  It looks like the following:

```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.sandec.jpro</groupId>
    <artifactId>hellojpro-maven</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

    <properties>
        <jproVersion>2019.1.0</jproVersion>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>

    <name>Hello JPro!</name>
    <url>https://www.jpro.one/</url>

    <build>

    <plugins>

      <plugin>
          <groupId>com.sandec.jpro</groupId>
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
          </configuration>
      </plugin>

    </plugins>
    </build>

    <pluginRepositories>
        <pluginRepository>
            <id>jpro - sandec repository</id>
            <url>http://sandec.bintray.com/repo</url>
        </pluginRepository>
    </pluginRepositories>

    <repositories>
        <repository>
            <id>jpro - sandec repository</id>
            <url>http://sandec.bintray.com/repo</url>
        </repository>
    </repositories>



    <dependencies>
        <dependency>
            <groupId>com.sandec.jpro</groupId>
            <artifactId>jpro-webapi</artifactId>
            <version>${jproVersion}</version>
            <scope>compile</scope>
        </dependency>
    </dependencies>



</project>
```

If the JPro starter does not find any maching name in the `jpro.conf`, then it will look 
for a specified `<mainClassName>` in the `pom.xml` to be started instead.


## PC AS JPRO SERVER

After testing your app through localhost, a next practical step could be to make your PC host a JPro server
for external access.  This way you can make your current state of the app available for insight by people 
located externally.  You can also see how the app behaves when it really uses a WLAN or the internet as 
communication platform for your JPro server. To achieve this, follow these steps:

### Step `1`. Start JPro in localhost

Make sure the `index.html`, the `jpro.conf` and your tool specific file (either `gradle.build` or `pom.xml`) 
are correctly setup to start your app. Check this by starting your JPro app as a normal app in your browser.  See 
[RUN JPRO LOCALLY](/?page=docs/current/1.1/RUN_JPRO_LOCALLY/) for more details.


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

Setup your in-house communication structure to support external access through one or more selected port numbers.


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

Setup your app to be shared among external users.



### Step `1`. Setup your PC as a JPro server

Make sure everything is prepared for your PC to host a JPro server, as explained 
[here](/?page=docs/current/1.1/RUN_JPRO_LOCALLY). 



### Step `2`. Setup for starting through the index.html

Modify the `index.html` to start your app with Screensharing, simply by 
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
There are two ways of making Gradle accessable for your project:

 * the files `gradlew` and `gradlew.bat` are parts of your project 
 (see the [helloJPro example](https://github.com/JPro-one/HelloJPro))  
 * you have downloaded and installed gradle

The following ***JPro commands*** are supported by the jpro-gradle-plugin, to be started either from your IDE or 
directly from your terminal(***):
 * `gradle jproRun` **starts the currently specified application**(*) inside of the browser.
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

During development, when you iteratively check your last program changes etc, you basically do fine with 
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
 * `mvn jpro:run` **starts the currently specified application**(*) inside of the browser.
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


During development, when you iteratively check your last program changes etc, you basically do fine with 
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

 Property         | Default value   | Description 
 -----------------| --------------- | -----------
 visible          | false           | If true, an additional window, beside the browser window, hosts the original javafx-application. This is for debuggig, only. It impacts the performance negatively. 
 port             | 8080            | The port to which the server should listen. 
 openURLOnStartup | true            | Tells JPro, whether the Browser should be opened after calling `jproRun`
 openingPath      | "/"             | On `jproRun` the Browser is automatically opened. This variable defines the path of the opened URL.
 useFontConfig    | false           | Tells the Server, whether the library fontconfig should be used to resolve fonts. It's deactivated by default to make sure, the font is always the same.
 jproVersion      | The version of the jpro-gradle-plugin | The JPro-version to be used.
 JVMArgs          | [] | A list of arguments, which are used to run JPro. 
 jproReleaseFiles | [:] | A map of paths and files, which should be added to the zip, generated by `jproRelease`


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

  jproVersion = "2019.1.0"            // The JPro version to use.  

  openURLOnStartup = false            // This prevents the browser from opening 
                                      // when jproRun is called.    
                                              
  openingPath = "/fullscreen/"        // A prefix to use for the path in  
                                      // the Url for the browser.
                                      
  JVMArgs << '-Xmx3500m'              // Lets set the memory for the JPro-Server
  
  // These two lines will add the file1.dat and file2.dat to the folder data in the zipfile.
  // The names of the files are changed to newname1.dat and newname2.dat.
  jproReleaseFiles << new JProReleaseFile("target/file1.dat", "/data/newname1.dat")
  jproReleaseFiles << new JProReleaseFile("target/file2.dat", "/data/newname2.dat")
  
  // The file is added to the folder named data, with the filename file3.dat.
  jproReleaseFiles << new JProReleaseFile("target/file3.dat", "/data/")
}
```

#### A pom.xml example

See the previous chapter for more comments associated with the properties.

**NOTE**: Please note, that `mainClassName` is here set under the `<configuration>` tag, allthough, 
for the gradle plugin it is not set where those other properties are set(under the `jpro` tag).

Here an **example**:

```xml
<plugin>
  <groupId>com.sandec.jpro</groupId>
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
}
```

### jpro.conf

The following properties can be set in the `jpro.conf`: 

 Property               | Default value | Description
 -----------------------|---------------|------------
 jpro.preventSystemExit | true          | Tells the JVM, to prevent calls to `java.lan.System.exit`.
 jpro.adminUsername     | ""            | The username, to access logs, passwords etc.
 jpro.adminPassword     | ""            | The password, to access logs, passwords etc.
 jpro.gcWorkaroundStage | true          | Activated a workaround for a memory leak in JavaFX when closing a stage.
 jpro.logResourceAccess | false         | Log all access to resources under the path `jpro/html`.
 jpro.logUserInputEvents| true          | Log all input events.
 
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

* using the `jproRun` or the `jpro:run` command (See [JPRO COMMANDS](/?page=docs/current/2.1/JPRO_COMMANDS/))
* authoring a URL in the browser


A **typical localhost URL** looks like the following:

`https://localhost:8083/myApp`  or  `https://localhost:8083/fullscreen/myApp`


  
  
For an app to be **JPro enabled**, it must extend the class called 

`javafx.application.Application`.

After declaring an app as runnable in the `jpro.conf`, **it can be embedded into a webpage** by using the `<jpro-app>` tag 
like follows:
```
<jpro-app href="/app/appname1" />
```

Go to the next chapter _**EMBEDDING JPRO**_ to see how to embed a runnable app into an existing webpage.





## EMBEDDING JPRO

JPro can be **embedded into an existing html-page** by using the tag `<jpro-app>`.
To activate the JPro-tag the following lines need to be introduced to the html-page:
```
<link rel="stylesheet" type="text/css" href="/jpro/css/jpro.css">
<script src="/jpro/js/jpro.js" type="text/javascript"></script>
```

To embed JPro to your dom, you need to introduce to your html-file:

`<jpro-app href="/app/default">`

  
  
### Supported attributes for the jpro-app tag

The jpro-app tag has a set of **attributes**, which can be set to control the jpro-app's behaviour: 

  Attribute name     | Default value | Description
  -------------------|---------------|----------------------
  href               |               |The URL of the application to be started.  It is either the URL of the App's websocket connection `"wss://yourServer.com/app/myAppName"`, or it's the relative URL `"/app/myAppName"`.
  loader             |               |Defines whether or not to activate the loading animation for this JPro-app. Valid values are: `"default"` `"none"`
  fullscreen         | "false"       |When true, the JPro app is resized to the entire page. It also **sets autofocus** to true.
  readonly           | "false"       |When true, the user can NOT do any data authoring to the scene.
  disableShadows     | "false"       |Disables all shadows in the JPro-renderer.  This might be useful, for rendering performance reasons.
  disableEffects     | "false"       |Disables all effects in the JPro-renderer.  This might be useful, for rendering performance reasons.
  autofocusEnabled   | "false"       |When true, the JPro-tag gets focused when the page is opened. This is useful for text-input, for example to enable the TextInput for a login-mask. 
  nativescrolling    | "false"       |When true, the scroll events are managed by html. Otherwise they are managed by the JPro app.
  nativezooming      | "false"       |When true, the zoom events are managed by html. Otherwise they are managed by the JPro app.
  userSelect         | "false"       |When true, the text selection is managed by html. Otherwise it is managed by the JPro app.
  scale              | "false"       |When true, the JPro app's scene is scaled to fit the html container. It works similar to `background-size: cover`in html.
  stretch            | "false"       |When true, the JPro app's scene is stretched to fit the html container.
  fxwidth            | "false"       |When true, the width  of the JPro-tag is managed by the JPro app. Otherwise the width  is managed by html.
  fxheight           | "false"       |When true, the height of the JPro-tag is managed by the JPro app. Otherwise the height is managed by html.
  fxContextMenu      | "false"       |When true, the context menu of the browser is surpressed and NOT shown. Is useful, when the JPro app itself has got a context-menu to show instead.
  setPrintJSCommands | "false"       |When true, all js-commands executed through the WebAPI are logged on the browser console.
  timeUntilReconnect | "10000"       |It specifies after how much time, the client tries to reconnect, when he didn't hear anything from the server.
 
### A web-page template

Here, **an example** (of course, to see an example, you could also just inspect the source of **this web-page**):


```
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


### Make Resources accessable as URLs

In order to **make resources publicly available as URLs**, you just need to understand and follow 
some **simple conventions** defined for the jpro servers.  Because of those conventions, you are freed from 
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
which can interoperate with JPro.  This means, should you want to bind your browser app to existing Javascript code, 
then the WebAPI comes to play.  But, in addition, it offers some general methods, which you will find 
useful when creating cross platform solutions.

The following features are currently available:

* Detecting your current running platform, like `com.jpro.web.WebAPI.isBrowser`
* Information about your current **session**, **language** used, **cookies**, the current **URL**, etc.
* Bridges for **bi-directional communication** between client-side Javascript/browser code and server-based java code.
* You can **interchange data**, do **remote calling**, registering remote functions calls, to be used between   
the client-side Javascript/browser and your server-based java code, and vice versa.


\
There are two ways to get access to the WebAPI:

* let your app `extend JProApplication` and call `getWebAPI()`, or
* call `WebAPI.getWebAPI(javafx.scene.Scene scene)` or 
* call `WebAPI.getWebAPI(javafx.stage.Window window)`.

        
\
For exact details about the API itself, please go to the [WebAPI-documentation](./?page=docs/current/api).

   
### Using the WebAPI without JPro
#### Using Gradle
The WebAPI can be imported as a jar, also when not using JPro. It can be introduced to the `build.gradle` by 
the following statement:

```
dependencies {
    ...
    compile "com.sandec.jpro:jpro-webapi:2019.1.0"
    ...
}
```

#### Using Maven
The WebAPI can be imported as a jar, also when not using JPro. It can be introduced to the `build.gradle` by 
the following statement:

```
    <dependencies>
        ...
        <dependency>
            <groupId>com.sandec.jpro</groupId>
            <artifactId>jpro-webapi</artifactId>
            <version>${jproVersion}</version>
            <scope>compile</scope>
        </dependency>
    </dependencies>
}
```

#### Getting WebAPI as a Jar
You can download the WebAPI from our [repository](http://sandec.bintray.com/repo/com/sandec/jpro/). 

This can be useful when you are using neither Maven nor Gradle.

[Here is the download link for the latest version.](http://sandec.bintray.com/repo/com/sandec/jpro/jpro-webapi/2019.1.0/jpro-webapi-2019.1.0.jar)



## DEBUGGING AND TESTING
The following tags can be added to the original URL of your JPro server.  
The JPro server responds to those tags in different ways, and thereby allows for system administrators and 
developers to aquire useful information during runtime. 

A `username` and `passwort` for the URLs (or pages) can be configured in the `jpro.conf`.
In production, the URLs (or pages) are only accessible, when a password is configured.

url | content
----| -------
/status                     | Returns a page with some statistics about the running server.
/status/alive               | Asks the running server whether it's alive and ok., When the javafx-thread is not being blocked and running normally, the server responds with the word "alive".
/info/log/console.log       | Returns a log-file with all the console-output of the application. The logging of the console-output can be deactivated in the `jpro.conf`.
/info/log/info.log          | Returns a log-file with all the info-logs in the jpro-server.
/info/log/warning.log       | Returns a log-file with all the warning-logs in the jpro-server.
/info/log/error.log         | Returns a log-file with all the error-logs in the jpro-server.
/info/log/activity.log      | Returns a log-file with all the activity-logs in the jpro-server.
/info/fxstack               | Returns the whole stack-trace of the javafx-thread. Useful for debugging blocked javafx-threads.
/info/minmemory             | Returns the memory-usage of the jvm, after running the garbage-collector.
/test/<appname>            | Creates a simple test-page, which opens the provided application.
/test/fullscreen/<appname> | Creates a simple test-page, which opens the provided application in fullscreen.
/test/scrolling/<appname>  | Creates a simple test-page, which opens the provided application as natively scrollable.
/info/heapdumps/heapdump.hprof | Downloads the heapdump of the server. Useful for finding memory-leaks with tools liks [VisualVM](https://visualvm.github.io/)
 
Here is an example of a command sent to a running JPro server called **https://www.jpro.one/status** (which is password protected)

which returns the following information about the JPro server:

```
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




## DEPLOYING JPRO

### Deployment Requirements
Basically, JPro servers can run on any server with a JVM on it.  But, fact is, so far all our real world projects 
are using Linux for the backend and therefore also for jpro.  For development purposes, we are mostly running our 
JPro servers on MacOS or Windows, but not for the live systems.  For those who cannot wait, but really need Windows 
or MacOS as deployment platforms for the backends right now, please contact us directly.  Our recommended platform 
for the JPro servers at time being is [Ubuntu 16.04](http://releases.ubuntu.com/16.04/).  
Other requirements are:

 * JPro requires the Oracle-JRE. JPro requires javaFX, which is not always contained in OpenJDK.
 
 * JavaFX requires some libraries to run in an headless environment. 
   Installing GTK and X11 is usually enough to run JavaFX.
 
 * For production it is highly recommended to use SSL.
   Why is this important?
   Because, some time proxies manipulate the traffic stream, and this would otherwise break the support of websockets.
   
## PREPARING LINUX FOR JPRO

### All linux versions
Install Java8 from the Oracle page. You have to create an oracle account to download it.


### Ubuntu 18.04:

To use JPro on Ubuntu 18.04, one has to install the following packages:

```
sudo apt-get install xorg gtk2-engines libasound2 libgtk2.0-0
```

### Ubuntu 16.04:

To use JPro on Ubuntu 16.04, one has to install the following packages:

```
sudo apt-get update

sudo apt-get install xorg gtk2-engines libasound2
```


### RedHat 7.5:  (OracleLinux CentOS (Tested with Redhat 7.5))

To use JPro on RedHat, one has to download and install the official [Oracle-Java](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) (not OpenJDK).
The download must be an rpm-package.

```
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

### SSL by using NGINX

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


## JPRO CHECKLIST
When using JPro, please be aware of the following important aspects:
* Your app **must NOT block** the javafx-thread.  Wait-, sleep-commands, showAndWaits in the javafx-thread are no-nos.
* Be careful when using **dialog boxes**. Make sure they dont use showAndWait (see above).
[Here](https://github.com/JPro-one/JPro-Samples/tree/master/popups) you can see how to create a JPro agnostic popup.
You can also use [this popup](http://www.jfoenix.com/documentation.html#Dialog) from the Jphoenix library.
* Be careful with **statics**, because they would be shared between multiple instances 
(interesting enough, there are use cases in which this fact can be utilized as a very useful feature. 
But, it is important not to use them in the wrong way.) 
* You can open **Stages** with the method `openStageAsPopup(Stage stage)` and `openStageAsTab(Stage stage)` of the [WebAPI](/api/2019.1.1/com/jpro/webapi/WebAPI.html).
  An alternative is, to create new windows or dialogues by using a StackPane at the root of your application.
  We have an example about popups in our [sample-project](https://github.com/JPro-one/JPro-Samples/tree/master/popups).
* The class WebView only works very limited with JPro. 
It should be replaced with `com.jpro.webapi.HTMLView`. 
[This sample ](https://github.com/JPro-one/JPro-Samples/tree/master/html-jpro) shows how to use 
the **HTMLView**.
* Snapshots only work with JavaFX11 or newer


### Not yet supported JavaFX features 
(this list refers to version 2019.1.1)
* Canvas (It will be supprted in the next major release)
* MediaPlayer
* The following Effect classes
    * Bloom
    * BoxBlur
    * ColorInput
    * DisplacementMap
    * DropShadow (Supported, but slow)
    * Glow
    * ImageInput
    * InnerShadow (Supported, but slow)
    * Lighting
    * MotionBlur 
    * PerspectiveTransform
    * Reflection
    * Shadow 
* 3D
* SwingNode
* javafx.stage.FileChooser, please take a look at our [WebAPI](/api/2019.1.1/com/jpro/webapi/WebAPI.html#makeFileUploadNode-javafx.scene.Node-) and our [sample project](https://github.com/JPro-one/JPro-Samples) for an alternative. 
* Clipboard
* WebView (Supported in it's basic form, only. We recommend to use the 
[HTMLView](/?page=docs/current/api), instead.)


# CHANGELOG

## 2019.1.X

### 2019.1.2 (11. September 2019)

#### Features:
 * Added the property `selectedFileSize` to the [FileHandler](/api/2019.1.2/com/jpro/webapi/WebAPI.FileUploader.html).  DOKU “FileHandler”, Wo???
 * Added the attribute [timeUntilReconnect](/?page=docs/current/2.3/EMBEDDING_JPRO) to the JProTag. It specifies after how much time, the client tries to reconnect, when he didn't hear anything from the server.

#### Bug fixes:
 * Fixed a performance regression that was introduced in 2019.1.0. It has a significant impact when many nodes are serialized in one and the same frame.
 * Eliminated the throwing of a superfluous exception. The text of the exception was like the following: `Popup cannot be cast to JavaFX.stage.Stage`
 * [#29](https://github.com/JPro-one/JPro-tickets/issues/29) Fixed a bug appearing when using JPro with Firefox. When the application was not in fullscreen, a node with effects was not rendered.


 * Fixed a bug when using the MavenPlugin. 
 Maven was downloading the artifacts which are required for the command `mvn jpro:release`, 
 even when this command was not called.

### 2019.1.1 (17. June 2019)

#### Features:
 * Added the methods 
[openLocalResource](/api/2019.1.1/com/jpro/webapi/WebAPI.html#openLocalResource-java.lang.String-) and 
[openLocalURL ](/api/2019.1.1/com/jpro/webapi/WebAPI.html#openLocalURL-java.net.URL-) to the 
[WebAPI](/api/2019.1.1/com/jpro/webapi/WebAPI.html). 
They can be used to open files in a new tab, for example pdf-files.

#### Bug fixes 
 * In the JPro renderer, reduced CPU usage by about 10%. Before this fix JPro could allocate upto 10% of the local CPU at time when it should actually be idle.
   Now, no relevant processing power is used when no changes are happening in the scene-graph.
 * Fixed a rare bug, when opening two applications at once, sometimes one instance did not start properly.
 * Sometimes, after reconnecting, the width or height of the application was wrong. This is now fixed.
 * Fixed a bug when changing the Scene of a Stage. Now, the Scene gets properly relayouted to the size of the JProElement.
 * Fixed a rare bug for JavaFX8 which in some rare occasions could cause the text input for a running session to stop working.
 * Gradle: Fixed a bug in the Gradle plugin, the JavaFX-Fork was added to the compile dependencies.
 * Maven: Fixed a bug, which prevented JPro from working when using JavaFX11 and Maven.
 * Maven: Fixed the command `mvn jpro:release` for Maven. Now the proper files are added, which are required to run JPro on Linux.



### 2019.1.0 (28. May 2019)

This release by default uses a forked version of JavaFX11.
JPro will still work with JavaFX8, but we recommend switching to Java(FX)11.
Some new JPro features are restricted to JavaFX11 and higher.

**We highly recommend switching to this new release `2019.1.0`,** 
because previous versions were using an experimental version for Web Components,
which will not be supported by Chrome much longer.

#### Features for the forked JavaFX11
* JPro now supports the method **snapshot** from Node.
* Dragview and Drag events are now supported in JPro. 
For now, they are restricted to work inside of the JavaFX application, they can not interface with other applications. 
* When calling the method showAndWait, it no longer leads to a freeze of the JavaFX Thread. It does not mean JPro supports showAndWait calls, it just contraints their negative side effects. ShowAndWait calls now throw an exception when using JPro.

#### Big features:
* For Linux, we now use different default fonts, because the Lucida fonts were removed from the OpenJDK, which resulted in various problems during deployment.
 Now they have been replaced by the fonts Roboto, Roboto Mono and Roboto Slab, which are licensed under the Apache License 2.0.

* Significant Performance improvements, especially when showing a lot of nodes for the first time. The time needed for rendering the initial scene graph was reduced by 30%.

* Updated the API version of the WebComponents.
We highly recommend updating to this JPro version `2019.1.0`, because the old WebComponents API was experimental and will stop working on some browser soon. 

* It's now possible to open **new Stages** as new tabs or popups. For this purpose, we've added the method `openStageAsPopup(Stage stage)` and `openStageAsTab(Stage stage)` to the WebAPI.

* Added the method `runAfterUpdate` to the WebAPI. 
This method enables for incremental loading of the scene graph, which can be used to improve the user experience.

* Added the method `getWebAPI(Node node, WebAPIConsumer consumer)` to the WebAPI.
It can be used to access the WebAPI from a node, instead of a stage.

* JPro now supports Java12. New upcoming Java releases will now automatically work when there are no breaking change.


#### Small Features
* The JavaDoc and the source code of the WebAPI are now published as Maven artifacts. This should improve tooling for IDEs. The JavaDoc has now got richer content.
* Added the field `JPro build time`, containing a timestamp for the JPro build, to the info block returned by the `/status` command.
* Added a new favicon for the internal pages.

#### Bug fixes
* Fixed a rendering issue with Pie Chart. It happened to Regions with (a) width and height property equal zero and (b) with a shape.
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
* Eliminated some rarethrowing of NullPointerExceptions.

**Gradle** and **Maven** Plugin fixes:
* When using `gradle jproRelease` or `mvn jpro:release` on Java11, now by 
default, the JavaFX version 11.0.2 is used.

### 2018.1.12 (17. March 2019)
**JPro** features:
* The processing of user input, mainly relevant for slow event listeners, was performance optimized.   The new behavior is closer to the behavior of JavaFX on the desktop.
* Changed the naming-pattern for logfiles. The new pattern is "logs/jpro.$level.log" instead of "logs/application.$level.log".

**JPro** fixes:
* The blinking behavior of the Caret in TextFields and TextAreas now behaves like on the desktop. It stops blinking for a short time, after typing.
* Key events for TextFields and TextAreas are now consumed as on the desktop.  They are consumed when the objects are focused.  Before this fix, when pressing SPACE in a focused TextField in a ScrollPane, a non-expected scroll down was executed.
* The `/status` page has gone through a cleanup regarding names and formatting.
* Fixed a bug on mobile chrome. On a touch, when the event target was removed shortly after touching down, then the touch release was not fired.
* Fixed a bug on mobile. On a long press, sometimes a release event was fired without actually releasing.
* Fixed a very rare bug, which could cause the text input to stop working.

### 2018.1.11 (11. February 2019)

**JPro** features:
* The page `/status` now uses mB instead of kB to display memory usage.

**JPro** fixes:
* Fixed a bug, which had the effect, that JPro didn't start properly with Java 1.8.0_202.
* Fixed a bug, which could happen on iOS devices.  It sometimes caused the screen to darken on touch events.
* Fixed a regression from 2018.1.10, the property `userSelect` of the <jpro-app> tag didn't work properly.
* Fixed a regression from 2018.1.10, the file upload when using the WebAPI didn't work properly.

**Gradle** and **Maven** Plugin fixes:
* Files explicitly added to the jproRelease zip, were added as a root element of the zip. 
  They are now added as an element of the folder of the application.

### 2018.1.10 (7. January 2019)
**JPro** features:
* JProRelease: It's now possible to add additional files to the zip-file generated by `gradle jproRelease` or `mvn jpro:release`.
  It's documented [here](https://www.jpro.one/?page=docs/current/2.2/CONFIGURING_JPRO).
  
* We added a development mode to the JPro server. 
  It is activated when the server is started from gradle/maven.
  The production mode is activated when the server is started by a zip, created with `gradle jproRelease` or `mvn jpro:release`.
  Pages like `/status` or `/test/appname` are now only accessible **without** username/password, when the development mode is active.
* We added a default-page for the JPro-server. 
  When the resource `jpro/html/index.html` is unavailable as the path `<servername>/` is opened, the content of `test/fullscreen/default` is shown.
  The default `openingPath` for gradle/maven is now `/`.
* A small memory-leak was fixed in the JPro Renderer (the JPro component running inside of the browser).

**JPro** fixes:
* The HTMLView was sometimes still rendered when the HTMLView or one of it's children was not visible. This is now fixed.
* Chrome: When the HTMLView was rendered outside of the visible area, sometimes the scrollable height of the page was changed. 
  This is now fixed.

**Gradle** and **Maven** Plugin fixes:
* (see above) It's now possible to generate files with `gradle jproRelease` and `mvn jpro:release`.add and then to add them to the zip.
* Fixed regression in the script `bin/stop.sh`. 
  It was not deleting the file `RUNNING_PID`, when the process didn't exist. This is now fixed.

### 2018.1.9 (26.November 2018)

**JPro** fixes:
* Added some printouts during JPro startup:
     Any errors coming from the javafx initialization process (most 
relevant for running a Linux server in production),
     the JPro-Version,
* Added a warning when a fontfile with the extension `.ttc` is used. 
The warning is important, because `.ttc`-files are not supported in the 
browsers.

* Fixed a regression in 2018.1.8.  In 2018.1.8 uploaded files, after a 
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

* There was a wrong leading text in the info/status.  It was saying 
`GRADLE-Distribution` instead of `MAVEN-Distribution`.  This has now 
been fixed.
* As the start.sh file was generated, it had some wrong classpaths in 
it, which were refering to files in the development environment.  
This had no effect, but was confusing and not clean. They are now removed.
* A build created with `mvn jpro:release` for JavaFX11 contained some 
jars, which are not required by JavaFX11. Those have now been eliminated 
for the JavaFX11 build.
* The JVMArgs provided in the `pom.xml` for the JVM were not correctly 
supported.  They now are.


### 2018.1.8 (12.November 2018)

**JPro now supports Java/JavaFX 11!**

**JPro** fixes:
* The javascript file for JPro is now 35% smaller than the previous one.
* When Setting the attribute `nativescrolling` for the JProTag, it no longer implicitly sets `fxHeight` to true.
* A bug was fixed, that a HTMLView in a Popup was still rendered although the popup was closed. 

Fixed for the **Gradle** and for the **Maven** Plugin:
* Added the property `useFontConfig`. The default value is `false`. 
Until now, JPro implicitly disabled the library with the name fontConfig, but with `useFontConfig` the activation of fontConfig was made configurable.
* When creating a release with `gradle jproRelease` or `mvn package jpro:release`, whitespaces in the directories are now handled correctly.
* When creating a release with `gradle jproRelease` or `mvn package jpro:release`, the start and restart script now passes it's arguments to the JVM as JVM-arguments.

Fixes for the **Gradle** Plugin:
* Fixed a bug in the gradle-plugin. The command `gradle jproRelease` now makes sure, that when no longer up to date, a new jar is generated.

Fixes for the **Maven** Plugin:
* Added the command `mvn package jpro:release` to the maven plugin. The maven plugin now supports all gradle features.
* Fixed a bug in the command `mvn compile jpro:run`, now it behaves the same way as the corresponding gradle command. When the file RUNNING.PID still exists, the corresponding process is killed and the file is deleted.



### 2018.1.7 (22.October 2018)

**JPro** fixes:

* On Edge and IE11, the caret of the hidden input-field is no longer visible.
* Added the attribute `setPrintJSCommands`to the JProTag. When true, all js-commands executed through the WebAPI are logged on the browser console.
  Documented in the chapter [EMBEDDING_JPRO](https://www.jpro.one/?page=docs/current/2.3/EMBEDDING_JPRO).
* Small reduction of the js-file by about 15%.
* A regression on mobile/iOS related to the text-input.
* A bug was fixed on the IE11, that sometimes image resources were not loaded correctly.
* A bug was fixed, that a font could not be loaded when it’s path contained a '+'-sign.

 


### 2018.1.6 (1. October 2018)

**JPro** fixes:
* A memory-leak could happen inside of JavaFX, when a node was removed from the scene-graph while the rendering was disabled. The memory is now released when the related node is no longer used, instead of at the end of a session.
* The MouseEvent methods `isAltDown()`, `isControlDown()`, `isMetaDown()` and `isShiftDown()` did not return the correct value and were now fixed.
* The field `Views afk` is now added to the URL `<servername>/status`. A view is treated as afk, when there was no user-input during a period of one minute.
* A new property was added to the `jpro.conf` to allow for logging all access to any files located under the resource path `jpro/html`.  It is activated by adding the `jpro.logResourceAccess = true` to the `jpro.conf`.
* A new property was added to the `jpro.conf` to allow for logging user input events.  It is activated by adding the `jpro.logUserInputEvents = true` to the `jpro.conf`.
* On iOS Safari it could happen, that touch generated unwanted double click events.  This bug has now been fixed.
* On iOS Safari it could happen, that touch events got lost.  This bug has now been fixed.
* Under special conditions it could happen, that ImageView did not render correctly.  It could happen with backgroundLoading set to true.  This bug has now been fixed.
* When using the WebAPI for downloading files, some file types used to open in the current tab.  This has now been changed.  Now all files are downloaded directly.
* We now use GZip for the download of all javascript files. This greatly increases the performance for initial sessions (before the browsers starts caching it).

Fixes for the **Gradle** Plugin:
* The value of `deployment` at `<servername>/status` when using `gradle jproStart` or `gradle jproRestart` was wrong. This bug has now been fixed.

Fixes for the **Maven** Plugin:
* A nullpointer-exception could be generated when calling `mvn compile jpro:stop`.   This bug has now been fixed.

### 2018.1.5 (23. July 2018)

* Maven : Added an experimental version for a MavenPlugin. [Check out the Maven-Helloworld!](https://github.com/JPro-one/HelloJPro-Maven)
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
* JPro  : Fixed some issues when using `Node.setClip`. This fix especially fixes the behaviour of the JFoenix-class `JFXButton`.
* JPro  : Fixed wrong rendering, when `Node.setRotate` is used in combination with `Node.setScaleX` or `Node.setScaleY`.
* JPro  : Significant performance-improvements for SVGPath for both the server and the browser.
* JPro  : Significant performance-improvements in the browser.
* JPro  : Fixed regression from the version 2018.1.3, which could crash a session in the Internet Explorer / Edge. 
* JPro  : Fixed js-exception in Internet Explorer / Edge. This improves the behaviour on Internet Explorer / Edge.
* JPro  : Fixed DropShadow sometimes being cut-off.
* JPro  : Added workaround for side-effects by adding a listener to the layoutBounds of a Group.
* JPro  : Fixed positioning of Popups with Shadows.
* JPro  : Fixed positioning of Popups without autofix.
* JPro  : Fixed rare race-condition in the rendering, which could have the effect of a temporary memory-leak.

### 2018.1.3 (4. June 2018)

* JPro  : Significant performance improvements. The SVG-Dom is now much smaller.
          Region is now painted faster, which especially benefits large business-applications. 
* JPro  : Fixed screen-mouse-position for various events.
* JPro  : Added a workaround for a rare bug, related to wrong popup-positions.
 It is activated by default. It can be deactived in jpro.conf with the following statement: `jpro.workaroundWindowPosition = false`.
* JPro  : Fixed bug related to HTMLView, under some conditions the visible-attribute wasn't updated correctly.
* JPro  : Fixed a rare bug related to TextFlow, which breaks the rendering and causes a NullPointerException.
* JPro  : Fixed a bug, which caused too many MouseEnter/MouseLeave events.
* JPro  : Fixed a race-condition, which had the effect, that the JavaFX-Context-Menu isn't shown.
* JPro  : When resizing the jpro-tag in the browser, the stage of the javafx-app is now also resized (previously only the scene was resized).
* JPro  : TextFlow with Nodes with `managed = false` are now rendered correctly.
* JPro  : Updated to Play Framework 2.6.13.
* JPro  : Added more information to `/status`.
* JPro  : Fixed a bug, where the logfiles couldn't be accessed in the browser, when the server had an uncommon default-encoding.
* JPro  : Added a workaround for a small memoryleak in JavaFX. It can be deactivated in the jpro.conf by the following line: `jpro.gcWorkaroundStage = false`.


### 2018.1.2 (19. April 2018)

* ***Added Support for Java10!***
* JPro  : When browser is resized fast and the server cannot catch up, the outdated resizing is now skipped.
* JPro  : fixed wrong clipping, when using the JPro-tag-attribute: scaling
* JPro  : Fixed an exception in the browser related to HTMLView and SVGView. They didn't had any symptoms
* JPro  : added error-message, when initialization of JPro doesn't terminate
* GRADLE: Fixed `jproRelease` on a clean build
* GRADLE: For the tasks `jproStart` and `jproRestart`, The console-output of JPro-process is now printed, until the port is opened
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
I'm using a lot of java libraries in my app, like controlsfx. Do they work in combination with jpro?
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
But it's currently doesn't work with the Charm library, specifically when the class [MobileApplication](http://docs.gluonhq.com/charm/javadoc/4.3.3/com/gluonhq/charm/glisten/application/MobileApplication.html) is used.

```
Does the ScenicView work in combination with JPro?
```
* Yes, the [ScenicView](http://fxexperience.com/scenic-view/) works without any problems.

```
How do I handle browser specific differences?
```
* JPro handles most of the browser specifics internally and relieves the developer from those topics.
NOTE: the code you write in javascript, obviously does not benefit from this.

```
The first Instance of my application starts fine, but as soon as the second instance is started, strange things happen. What can be the cause?
```
* It's most likely related to the use of static variables. In JPro, static variables are shared between multiple sessions. Therefore, variables declared as static become global to all sessions.  This fact can cause problems.  BUT, depending on how you use it, it can also be utilized as a welcomed feature.

```
My application slows down over time. After a while it some times even crashes. What could be the reason for such a behaviour?
```
* A common reason for this behaviour is a memory leak in your application.
You can use tools like [VisualVM](https://visualvm.github.io/) to solve the issue in your application.

```
How can i use a IDE for my JPro-project?
```
The HelloWorld-Project is a simple gradle/java project, which can be imported by intellij or eclipse without any modifications.

# SUPPORT

## SUPPORT

Feel free to contact us at `info@jpro.one` for commercial support or any other related topic.

## What if I find bugs?

Should you find bugs in jpro, please inform us about any details through our 
[jpro bug-tracker](https://github.com/JPro-one/jpro-issues).


# Links

## [OpenJFX](https://openjfx.io/)

## [Ticket System](https://github.com/JPro-one/JPro-tickets)

## [JPro Samples](https://github.com/JPro-one/JPro-Samples/) 

## [JavaFX Version 11 API](https://openjfx.io/javadoc/11/index.html)

## [JavaFX Version 10 API](https://docs.oracle.com/javase/10/docs/api/overview-summary.html)

## [JavaFX Version 9 API](https://docs.oracle.com/javase/9/docs/api/overview-summary.html#JavaFX)

## [JavaFX Version 8 API](https://docs.oracle.com/javase/8/javafx/api/toc.htm)

## Related projects

* [Gluon](http://gluonhq.com/)'s useful Java technologies, including the [Gluon Mobile](http://gluonhq.com/products/mobile/) library. 
* [ControlsFX](http://fxexperience.com/controlsfx/), a community library managed by 
[Jonathan Giles](https://jonathangiles.net/) and 
[Gluon](https://gluonhq.com/), with a set of controls.  In 2017 it received the 
[Duke Choice Award](https://www.oracle.com/java/2017-dukes-choice-awards.html) for it's awesome work.
* [Dirk Lemmermann's](https://dlsc.com/) powerful projects:
    * [CalendarFX](http://dlsc.com/products/calendarfx/).
    * [PreferencesFX](https://github.com/dlemmermann/PreferencesFX).
    * [FormsFX](https://github.com/dlemmermann/FormsFX).
    * [FlexGanttFX](https://dlsc.com/products/flexganttfx/) (Using Canvas, therefore not fully supported by JPro, yet).
* [Harmonic Code](https://harmoniccode.blogspot.de/2018/02/friday-fun-lix-parallel-coordinates.html) is 
an impressive and dynamic blog from the Java Champion [Gerrit Grunwald](https://twitter.com/hansolo_?lang=de), 
which describes his cool components libraries.
* [Dr. Michael Hoffer's](https://twitter.com/mihosoft?lang=de)  
with lots of [interesting projects](https://mihosoft.eu). 

A JPro helloworld project can be found [here](https://github.com/JPro-one/HelloJPro).


## Blogs

[fxexperience.com](http://fxexperience.com/) is a very interesting blog from Jonathan Giles, previously Oracle, now Microsoft.

[ScenicView](http://fxexperience.com/scenic-view/) represents a very useful debugging tool for UI development.


The JavaFX Champion und JavaOne Rockstar [Dirk Lemmermann](http://dlsc.com/blog/)'s interesting blog.
