# JPRO DOCs

## GETTING STARTED

The easiest way to get started, is to use **Gradle** as build tool.
jpro provides a plugin for gradle,
which allows you to easily start jpro from an existing project, 
which is obviously rather practical during the development process.

Currently, jpro supports Gradle in the versions 2.x and 3.x.  We suggest to use 3.x.

As a simple reference project, you could take a look at the simple **hello-world project** found 
[here](https://github.com/jpro-one/HelloJPro) and you can **run it** 
[here](https://demos.jpro.one/helloworld.html).

To get started and run your first app with jpro, you should execute the following **4 steps**:

    * Install Gradle
    * Create the Gradle script
    * Create the jpro configuration file
    * Run the app 


### Step `1`. Install Gradle
 
Gradle can be downloaded and installed [here](https://gradle.org/install/). 


### Step `2`. Create the Gradle script 
 
Create the file `build.gradle` and put it into your **project's root directory**.  
You can either download a template file [here](https://raw.githubusercontent.com/jpro-one/HelloJPro/master/build.gradle) or just use the following:

```groovy
buildscript {
  repositories {
    jcenter()
    maven {
      url "http://sandec.bintray.com/repo"
    }
  }

  dependencies {
    classpath 'com.jprotechnologies.jpro:jpro-plugin-gradle:2018.1.0'
  }
}

repositories {
  jcenter()
}

apply plugin: 'com.jprotechnologies.jpro'

mainClassName = 'your.class.Name'

jpro {
  port = 8080
}
```

### Step `3`. Create the jpro configuration file 

This file is configured in [HOCON (Human-Optimized Config Object Notation)](https://github.com/lightbend/config/blob/master/HOCON.md), 
which is a superset of JSON, and is optimized for writing configurations.


The `jpro.conf` must be placed into the directory `<project-dir>/src/main/resources`.

You can either download a **template file** 
[here](https://raw.githubusercontent.com/jpro-one/HelloJPro/master/src/main/resources/jpro.conf) or just use the following:

```groovy
jpro.applications {
  "myApp" = com.jpro.somepackage.SomeMain
}
```

### Step `4`. Run the app 

Start a **Terminal session**, move to the **main project directory** and enter the command:

```groovy
gradle jproRun
```

Now you should see your app running inside of your standard browser.




## JPRO COMMANDS

There are two ways of making Gradle accessable for your project:

 * the files `gradlew` and `gradlew.bat` are parts of your project 
 (see the [helloJPro example](https://github.com/jpro-one/HelloJPro))  
 * you have downloaded and installed gradle


### Using gradlew

The following ***jpro commands*** are supported by the jpro-gradle-plugin, to be started either from your IDE or 
directly from your terminal:
 * `./gradlew jproRun` **starts the currently specified application**(*) inside of the browser.
    Before it starts the application it automatically **starts the jpro server**. 
    The console output is visible in the console until the jpro server is closed (you can close the running app 
    by typing `ctrl+c` in the terminal window).
    
 * `./gradlew jproStart` **starts the jpro server** in the background(**).
 
 * `./gradlew jproStop` **stops the jpro server** in the background.
 
 * `./gradlew jproRestart` **restarts the jpro server**.  Should the jpro server already be running, 
    it automatically gets stopped before restarted.
    
 * `./gradlew jproRelease` **creates a zip-file**, which contains a build of the **current project**, 
   including the dependencies for jpro and for the current project.
   It contains scripts for `start/stop/restart` of the ***deployed jpro servers***. 
   The scripts are located in the *bin-folder*.

(*) the "currently specified application" is the `mainClassName` defined in the `build.gradle`.

(**) in this process we are dealing with a single jpro server, which is why no jpro server needs to be addressed 
specifically.


### Using gradle

The table above shows what the commands are like when the two files are members of your project.  When you have 
installed gradle, the equivalent commands are:

 * `gradle jproRun` **starts the currently specified application**
 * `gradle jproStart` **starts the jpro server** in the background.
 * `gradle jproStop` **stops the jpro server** in the background.
 * `gradle jproRestart` **restarts the jpro server**.    
 * `gradle jproRelease` **creates a zip-file**.


During development, when you iteratively check your last program changes etc, you basically do fine with 
just using the `jproRun` command from your terminal window.  If required, it automatically starts your browser, 
and opens a new tab with your app in it.  Which app to start is defined in the `mainClassName` of your `build.gradle`. 

The browser's URL shows the `localhost` URL with whatever properties you have specified either 
in your app or in your `build.gradle`.  You don't need to worry about starting a jpro server 
etc., it is all handled by the `jproRun` command for you.

In a real world scenario, though, when your jpro server runs **remotely**, you will require the other commands, 
like the `jproStart` etc. 



## CONFIGURING JPRO
 
### build.gradle

In the file `build.gradle` the gradle-plugin for jpro is configured.  

The following configuration properties are available:

 Property         | Default value   | Description 
 -----------------| --------------- | -----------
 visible          | false           | If true, an additional window, beside the browser window, hosts the original javafx-version. This is for debuggig, only. It impacts the performance negatively. 
 port             | 8080            | The port to which the server should listen. 
 openURLOnStartup | true            | tells jpro, whether the Browser should be opened after calling jproRun
 openingPath      | "/test/default" | On jproRun the Browser is automatically opened. This variable defines the path of the opened URL. 
 jproVersion      | The version of the jpro-gradle-plugin | The jpro-version to be used. 


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

  jproVersion = "2018.1.0"            // The jpro version to use.  

  openURLOnStartup = false            // This prevents the browser from opening 
                                      // when the app starts.
                                      // This might be useful when ... ??    
                                              
  openingPath = /fullscreen/          // A prefix to use for the path in  
                                      // the Url for the browser.
}
```


### jpro.conf

The following properties can be set in the `jpro.conf`: 

 Property          | Default value | Description
 ------------------|---------------|------------
 preventSystemExit | true          | Tells the JVM, to prevent calls to `java.lan.System.exit`.
 adminUsername     | ""            | The username, to access logs, passwords etc.
 adminPassword     | ""            | The password, to access logs, passwords etc.

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

* using the `jproRun` command
* authoring a URL in the browser
* ??


A **typical localhost URL** looks like the following:

`https://localhost:8083/myApp`  or  `https://localhost:8083/fullscreen/myApp`


  
  
For an app to be **jpro enabled**, it must extend the class called 

`javafx.application.Application`.

After declaring an app as runnable in the `jpro.conf`, **it can be embedded into a webpage** by using the `<jpro-app>` tag 
like follows:
```
<jpro-app href="/app/appname1" />
```

Go to the next chapter _**EMBEDDING JPRO**_ to see how to embed a runnable app into an existing webpage.





## EMBEDDING JPRO

jpro can be **embedded into an existing html-page** by using the tag `<jpro-app>`.
To activate the jpro-tag the following lines need to be introduced to the html-page:
```
<link rel="stylesheet" type="text/css" href="/jpro/css/jpro.css">
<script src="/jpro/js/jpro.js" type="text/javascript"></script>
```

To embed jpro to your dom, you need to introduce to your html-file:

`<jpro-app href="/app/default">`

  
  
### Supported attributes for the jpro-app tag

The jpro-app tag has a set of **attributes**, which can be set to control the jpro-app's behaviour: 

  Attribute name   | Default value | Description
  -----------------|---------------|----------------------
  href             |               |The URL of the application to be started.  It is either the URL of the App's websocket connection `"wss://yourServer.com/app/myAppName"`, or it's the relative URL `"/app/myAppName"`.
  loader           |               |Defines whether or not to activate the loading animation for this jpro-app. Valid values are: `"default"` `"none"`
  fullscreen       | "false"       |When true, the jpro app is resized to the entire page. It also **sets autofocus** to true.
  readonly         | "false"       |When true, the user can NOT do any data authering to the scene.
  disableShadows   | "false"       |Disables all shadows in the jpro-renderer.  This might be useful, for rendering performance reasons.
  disableEffects   | "false"       |Disables all effects in the jpro-renderer.  This might be useful, for rendering performance reasons.
  autofocusEnabled | "false"       |When true, the jpro-tag gets focused when the page is opened. This is useful for text-input, for example to enable the TextInput for a login-mask. 
  nativescrolling  | "false"       |When true, the scroll events are managed by html. Otherwise they are managed by the jpro app.
  nativezooming    | "false"       |When true, the zoom events are managed by html. Otherwise they are managed by the jpro app.
  userSelect       | "false"       |When true, the text selection is managed by html. Otherwise it is managed by the jpro app.
  scale            | "false"       |When true, the jpro app's scene is scaled to fit the html container. It works similar to `background-size: cover`in html.
  stretch          | "false"       |When true, the jpro app's scene is stretched to fit the html container.
  fxwidth          | "false"       |When true, the width  of the jpro-tag is managed by the jpro app. Otherwise the width  is managed by html.
  fxheight         | "false"       |When true, the height of the jpro-tag is managed by the jpro app. Otherwise the height is managed by html.
  fxContextMenu    | "false"       |When true, the context menu of the browser is surpressed and NOT shown. Is useful, when the jpro app itself has got a context-menu to show instead.
 
 
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
the burden of using a separate web servers for your resources, be it images, html-files or any 
other thinkable resource.

Any resource underneath the package `jpro/html` are publicly available through the jpro-server as a URL.
Another practical convention is that, when a file is named `index.html` the filename itself is redundant and 
can therefore simply be skipped for the URL.

The follwing examples should explain well what is meant:

The jpro server can be reached with the url `http://localhost:8080`, 

`jpro/html/myImage.jpg` with `http://localhost:8080/myImage.jpg`,

`jpro/html/folder/myImage.jpg` with `http://localhost:8080/folder/myImage.jpg` and   

`jpro/html/index.html` with `http://localhost:8080/index.html` or 

`jpro/html/index.html` with `http://localhost:8080/`.

 

### Publishing jpro applications

To make your jpro applications accesible via URL, you should create an “index.html” and place
it into `/jpro/html/index.html` (or in the project structure under `src/main/resources/jpro/html/index.html`.  
\
As mentioned in the last chapter, all files to be accessible via URL, be it HTML files, images, documents or others, 
should be placed in the classpath on `/jpro/html`.



## THE WEB-API
The main purpose of the WEB-API is to let you create individual Javascript code for the browser, 
which can interoperate with jpro.  This means, should you want to bind your browser app to existing Javascript code, 
then the WEB-API comes to play.  But, in addition to that, it offers some general methods, which you will find 
useful when creating cross platform solutions. 

The following features are currently available:

* Detecting your current running platform, like `com.jpro.web.WebAPI.isBrowser`
* Information about your current **session*, **language* used, **cookies**, the current **URL**, etc.
* Bridges for **bi-directional communication** between client-side Javascript/browser code and server-based java code.
* You can **interchange data**, do **remote calling**, registering remote functions calls, to be used between   
the client-side Javascript/browser and your server-based java code, and vice versa.


\
There are two ways to get access to the WEB-API:

* let your app `extend JProApplication` and call `getWebAPI()`, or
* call `WebAPI.getWebAPI(javafx.scene.Scene scene)` or 
* call `WebAPI.getWebAPI(javafx.stage.Window window)`.

        
\
For exact details about the API itself, please go to the [WEB-API-documentation](./?page=docs/current/api).

   
### Using the WEB-API without jpro
The WEB-API can be imported as a jar, also when not using jpro. It can be introduced to the `build.gradle` by 
the following statement:

```
dependencies {
    ...
    compile "com.sandec.jpro:jpro-webapi:2018.1.0"
    ...
}
```



## DEBUGGING AND TESTING
The following tags can be added to the original URL of your jpro server.  
The jpro server responds to those tags in different ways, and therebye allows for system administrators and 
developers to aquire useful information during runtime. 

A `username` and `passwort` for these pages can be configured in the `jpro.conf`, which is mandatory for production.

url | content
----| -------
/status                     | Returns a page with some statistics about the running server.
/status/alive               | Asks the running server whether it's alive and ok., When the javafx-thread is not being blocked and running normally the server responds with the word "alive".
/info/log/console.log       | Returns a log-file with all the console-output of the application. The logging of the console-output can be deactivated in the `jpro.conf`.
/info/log/info.log          | Returns a log-file with all the info-logs in the jpro-server.
/info/log/warning.log       | Returns a log-file with all the warning-logs in the jpro-server.
/info/log/error.log         | Returns a log-file with all the error-logs in the jpro-server.
/info/log/activity.log      | Returns a log-file with all the activity-logs in the jpro-server.
/info/fxstack               | Returns the whole stack-trace of the javafx-thread. Useful for debugging an blocked javafx-threads.
/info/minmemory             | Returns the memory-usage of the jvm, after running the garbage-collector.
/test/\<appname>            | Creates a simple test-page, which opens the provided application.
/test/fullscreen/\<appname> | Creates a simple test-page, which opens the provided application in fullscreen.
/test/scrolling/\<appname>  | Creates a simple test-page, which opens the provided application as natively scrollable.
/info/heapdumps/heapdump.hprof | Downloads the heapdump of the server. Useful for finding memory-leaks with tools liks [VisualVM](https://visualvm.github.io/)
 
Here an examples of a command to a running jpro server called **live.ff-drohnenquiz.de**:

```
    live.ff-drohnenquiz.de/status
```

which returns the following information about the jpro server:

```
    servletInfo: jetty/9.4.3.v20170317
    quizmaxVersion: 2.5.3
    startTime: Thu Feb 15 12:16:50 CET 2018
    maxMem: 3055m
    usedMem(heap): 76.7652138505149%
    fx-cpu-usage: 0.21030353982300884% 
```




## DEPLOYING JPRO

### Deployment Requirements
Basically, jpro servers can run on any server with a JVM on it.  But, fact is, so far all our real world projects 
are using Linux for the backend and therefore also for jpro.  FOr development purposes, we are mostly running our 
jpro servers on MacOS or Windows, but not for the live systems.  For those who cannot wait, but really need Windows 
or MacOS as deployment platforms for the backends right now, please contact us directly.  Our recommended platform 
for the jpro servers at time being is [Ubuntu 16.04](http://releases.ubuntu.com/16.04/).  
Other requirements are:

 * jpro requires the Oracle-JRE.  jpro requires javaFX, which is not always contained in OpenJDK.
 
 * For production it is highly recommended to use SSL.
   Why is this important?
   Because, some time proxies manipulate the traffic stream, and this would otherwise break the support of websockets.

### SSL by using NGINX

 The setup defined below is tested with the nginx package contained in ubuntu 16.04.

 In order to configure nginx for jpro, create the file 
 `/etc/nginx/sites-enabled/jproconf.nginx.conf` with the following content:
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

 The following procedure can be used to heko creating the file: 

 In order to configure the domain the way a jpro server needs it, please create the following file 
 (replace `yourdomain` with the real name):

 `/etc/nginx/sites-enabled/yourdomain_com.nginx.conf`
 ```
 upstream jpro {
   server 127.0.0.1:8080;
 }
 server {
   listen 80;
   server_name yourdomain.com;  # Here a list of all domain names to be used for this jpro server #
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
When using jpro, please be aware of the following important aspects:
* Your app **must NOT block** the javafx-thread.  Wait-, sleep-commands, showAndWaits in the javafx-thread are no-nos.
* Be careful when using dialog boxes. Make sure they dont use showAndWait (see above).
* Be careful with statics, because they would be shared between multiple instances 
(interesting enough, there are use cases in which this fact can be utilized as a very useful feature. 
But, it is important not to use them in the wrong way.) 
* Creating additional Stages is not supported.
  The only Stage which can be opended by a Session, is the Stage associated with the `javafx.scene.Application.show` method.
  One alternative is, to create new windows or dialogues by using a StackPane at the root of your application.


### Not yet supported JavaFX features 
(this list refers to version 2018.1.0)
* Canvas
* MediaPlayer
* Some effects
* Snapshots
* 3D


# FAQ
## FAQ
```
I'm using a lot of java libraries in my app, like controlsfx. Do they work in combination with jpro?
```
* jpro works well with any java library.

```
Does jpro work on mobile browser?
```
* jpro works very well on mobile browsers.

```
Does jpro work in combination with Gluon?
```
* jpro works without any problem with the [javafxmobile-plugin](https://bitbucket.org/javafxports/javafxmobile-plugin).

```
Does the ScenicView work in combination with jpro?
```
* Yes, the [ScenicView](http://fxexperience.com/scenic-view/) works without any problems.

```
How do I handle browser specific differences?
```
* jpro handles most of the browser specifics internally and relieves the developer from those topics.
NOTE: the code you write in javascript, obviously does not benefit from this, though.

```
The first Instance of my application starts fine, but as soon as the second instance is started, strange things happen. What can be the cause?
```
* It's most likely related to the use of static variables. In jpro, static variables are shared between multiple sessions. Therefore, variables declared as static become global to all sessions.  This fact can cause problems.  BUT, depending on how you use it, it can also be utilized as a welcomed feature.

```
My Application get's slower over time. After a while it some times even crashes. What can be reason for such a behaviour?
```
* A common reason for this behaviour is a memory leak in your application.
You can use tools like [VisualVM](https://visualvm.github.io/) to solve the issue in your application.


# SUPPORT

Feel free to contact us at `info@jpro.one` for commercial support or any other related topic.

## What if I find bugs?

Should you find bugs in jpro, please inform us about any details through our 
[jpro bug-tracker](https://github.com/jpro-one/jpro-issues).


# Links

## [JavaFX Version 9 API](https://docs.oracle.com/javase/9/docs/api/overview-summary.html)

## [JavaFX Version 8 API](https://docs.oracle.com/javase/8/javafx/api/toc.htm)



## Related projects

* A useful community library - [ControlsFX](http://fxexperience.com/controlsfx/) - with a set of interesting controls.
* [Harmonic Code](https://harmoniccode.blogspot.de/2018/02/friday-fun-lix-parallel-coordinates.html) is 
an impressive blog from the Java Champion Gerrit Grünwald, which describes his cool components library. 
* [Gluon](http://gluonhq.com/)'s useful technology for Cross Platform development with Java, including 
the [Gluon Mobile](http://gluonhq.com/products/mobile/) library, which supports you in writing Java code 
for the mobile platforms.
* Dr. Michael Hoffer's [page](https://mihosoft.eu) with lots of interesting projects. 

\
The jpro helloworld project can be found [here] (https://github.com/jpro-one/HelloJPro).


## Blogs

[fxexperience.com](http://fxexperience.com/) is a very interesting blog from Jonathan Giles, previous Oracle, now Microsoft.

[ScenicView](http://fxexperience.com/scenic-view/) represents a very handy debugging tool for UI development.


