---
layout: post
title: Configuring a read-only user in Tomcat to add JMX authentification 
---

> The goal is to configure the Tomcat startup script in order to create a readonly user to read data from the JMX interface.
> Then we use that user in Zabbix to connect to the JMX console

## 1. Create or update your setenv.sh to allow for jmx and add authentication
If it does not exist, create a env.sh file in your $CATALINA_HOME/bin. It will contain all info on the jmx remote interface.  
[From the tomcat documentation](https://tomcat.apache.org/tomcat-7.0-doc/monitoring.html)

``` bash
#!/bin/sh
# Allow jmx remote
CATALINA_OPTS="$CATALINA_OPTS
-Dcom.sun.management.jmxremote=true
-Dcom.sun.management.jmxremote.port=8888
-Dcom.sun.management.jmxremote.ssl=false
-Dcom.sun.management.jmxremote.authenticate=true
-Dcom.sun.management.jmxremote.password.file=$CATALINA_HOME/conf/jmxremote.password
-Dcom.sun.management.jmxremote.access.file=$CATALINA_HOME/conf/jmxremote.access
-Djava.rmi.server.hostname=SERVER_IP
"
```

## 2. Create the access and password file
Here we create the jmxremote.access to add a monitorZabbix user with readonly permission. We adjust the rights so only tomcat can read it.

``` bash
cd $CATALINA_HOME/conf
echo "monitorZabbix readonly" > jmxremote.access && chmod 400 jmxremote.access && chown tomcat:tomcat jmxremote.access
``` 

Here we create the jmxremote.password to define the password for the monitorZabbix user declared previously. We adjust the rights so only tomcat can read it.

``` bash
cd $CATALINA_HOME/conf
echo "monitorZabbix PASSWORD" > jmxremote.password && chmod 400 jmxremote.password && chown tomcat:tomcat jmxremote.password
```
## 3. Declaring the user in Zabbix

On the host screen, create the two following macros. If needed/wanted you can declare them on the template level.

``` bash
{$JMX_USER_NAME} = monitorZabbix
{$JMX_PASSWORD} = PASSWORD
```
