---
layout: post
title: Application Performance Management
date: 2020-07-30
category: category
---

# Application Performance Management (APM)

## Heap Peep with the jcmd utility
Referred from - [Oracle Documentation](https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr006.html)

Find all Java PIDs
````sh
jcmd
````

Create a heap dump
````sh
jcmd <PID> Thread.print | head -n100 >> MyHeapDump.txt
````

Furthermore, configured the JCMD in the crontab to capture the dumps at intervals to see the application performance.
````sh
0 0 * * * sh /path/to/heap_peep.sh
````

The exported heap dump file could be analyzed online with several online portals - [FastThread](https://fastthread.io/)


## Glowroot
Referred from - [Glowroot](https://glowroot.org/) - [Glowroot github](https://github.com/glowroot/glowroot)

1. Common steps
	1. Download the glowroot jar, extract the jar.

2. Configuring Glowroot for single application
	1. Add ````-javaagent:path/to/glowroot.jar```` to JVM args. (For web application, the JAVA_OPTS are usually in the setenv.sh file. For standalone application, the argument is passed along with the other args.)
	2. ````java -jar -javaagent:path/to/glowroot.jar MyApp.jar````

3. Configuring Glowroot for multiple applications running in the same box
	1. Referred from [here](https://github.com/glowroot/glowroot/wiki/Agent-Installation-(with-Embedded-Collector))
	2. Create a new file glowroot.properties under the Glowroot Agent folder add the below line multi.dir=true in the properties file
	3. Add this to the JVM args for each app where the glowroot has to be configured ````-Dglowroot.agent.id=MyAppName```` along with ````-javaagent:path/to/glowroot.jar````
	4. Once the above steps are complete and the app is restarted, there will be a new folder with name **agent-MyAppName**
	5. In the **admin.json** under the new folder (MyAppName in this example), change the port and the context path(if required). Now glowroot is accessible by 127.0.0.1:4000/MyAppName-glowroot
````JSON
"port": 4001,
"bindAddress": "127.0.0.1",
"contextPath": "/MyAppName-glowroot",
"sessionTimeoutMinutes": 30,
"sessionCookieName": "GLOWROOT_SESSION_ID"
````
	6. Repeat step 3 to 5 to configure for another application.


Note : Configure ProxyPass on apache or nginx to allow request forwarding if a particular port is not open.
