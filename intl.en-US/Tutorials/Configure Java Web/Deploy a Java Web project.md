# Deploy a Java Web project {#concept_51376_zh .concept}

This article describes how to deploy a Java Web project on a Linux instance with the basic configuration. This method is applicable to individual users who are new to website construction by using ECS.

## Configuration requirements { .section}

The following programs are used as examples to deploy the Java Web project:

-   OS: CentOS 7.4
-   Tomcat: Tomcat 8.5.23
-   JDK: JDK 1.8.0\_141

## Preparations { .section}

-   The firewall is enabled by default for CentOS 7.4. You can disable the firewall, or add rules on the firewall by referring to official documents to open Ports 80, 443, or 8080 for inbound access.

    -   Disable the firewall.

        ```language-bash
        systemctl stop firewalld.service
        
        ```

    -   Set the firewall not to be enabled automatically at startup.
    ```language-bash
    systemctl disable firewalld.service
    
    ```

-   Create a user www to run Tomcat.

    ```language-bash
    useradd www
    
    ```

-   Add a security group rule to open Port 8080 for HTTP access. For more information, see [add a security group rule](../../../../reseller.en-US/User Guide/Security groups/Add security group rules.md#).
-   Creates a root directory for the Java Web project.

    ```language-bash
    mkdir -p /data/wwwroot/default
    
    ```

-   Create a Tomcat test page.

    ```language-bash
    echo Tomcat test > /data/wwwroot/default/index.jsp
    chown -R www.www /data/wwwroot
    ```


## Download source code { .section}

```language-bash
wget https://mirrors.aliyun.com/apache/tomcat/tomcat-8/v8.5.23/bin/apache-tomcat-8.5.23.tar.gz
```

The source code is constantly upgraded. You can find the installation package at https://mirrors.aliyun.com/apache/tomcat/tomcat-8/.

```language-bash
wget http://mirrors.linuxeye.com/jdk/jdk-8u141-linux-x64.tar.gz

```

The source code is constantly upgraded. You can find the installation package at http://mirrors.linuxeye.com/jdk/.

## Install JDK { .section}

To install JDK, follow these steps:

1.  Run mkdir /usr/java to create a directory.

    ```language-bash
    mkdir /usr/java
    
    ```

2.  Run the following command to decompress jdk-8u141-linux-x64.tar.gz to the /usr/java directory.

    ```language-bash
    tar xzf jdk-8u141-linux-x64.tar.gz -C /usr/java
    
    ```

3.  Follow these steps to set environment variables:
    1.  Run vi /etc/profile: `vi /etc/profile`
    2.  Press the `i` key to enter the Edit mode.
    3.  Add the following lines into the /etc/profile file:

        ```language-bash
        #set java environment
        export JAVA_HOME=/usr/java/jdk1.8.0_141
        export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
        export PATH=$JAVA_HOME/bin:$PATH
        ```

    4.  Press the `Esc` key, and then type `:wq` to save and close the file.
4.  Run `source /etc/profile` to load the new environment variable.
5.  Check the version of JDK. When the JDK version is displayed, it indicates that JDK has been installed successfully.

    ```language-bash
    java -version
    
    ```

    ```language-bash
    java -version
    java version "1.8.0_141"
    Java(TM) SE Runtime Environment (build 1.8.0_141-b15)
    Java HotSpot(TM) 64-Bit Server VM (build 25.141-b15, mixed mode)
    ```


## Install Tomcat { .section}

To install Tomcat, follow these steps:

1.  Run the following commands one by one to decompress apache-tomcat-8.5.23.tar.gz, rename the Tomcat directory, and set user permissions.

    ```language-bash
    tar xzf apache-tomcat-8.5.23.tar.gz
    mv apache-tomcat-8.5.23 /usr/local/tomcat/
    chown -R www.www /usr/local/tomcat/
    ```

    **Note:** In the /usr/local/tomcat/ directory:

    -   The bin directory stores some Tomcat script files, including scripts for enabling and disabling Tomcat service.
    -   The conf directory stores various global configuration files for Tomcat server, the most important of which are server.xml and web.xml.
    -   The webapps directory is the main Web publishing directory of Tomcat, which stores Web application files by default.
    -   The logs directory stores Tomcat log files.
2.  Follow these steps to configure the server.xml file:
    1.  Switch to the /usr/local/tomcat/conf/ directory: `cd /usr/local/tomcat/conf/`.
    2.  Rename the server.xml file: `mv server.xml server.xml_bk`.
    3.  Create a new server.xml file:

        1.  Run `vi server.xml`.
        2.  Press the `i` key to enter the Edit mode.
        3.  Add the following content.
        ```
        <? xml version="1.0" encoding="UTF-8"? > <Server port="8006" shutdown="SHUTDOWN"> <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener"/> <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener"/> <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener"/> <Listener className="org.apache.catalina.core.AprLifecycleListener"/> <GlobalNamingResources> <Resource name="UserDatabase" auth="Container" type="org.apache.catalina.UserDatabase" description="User database that can be updated and saved" factory="org.apache.catalina.users.MemoryUserDatabaseFactory" pathname="conf/tomcat-users.xml"/> </GlobalNamingResources> <Service name="Catalina"> <Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" maxThreads="1000" minSpareThreads="20" acceptCount="1000" maxHttpHeaderSize="65536" debug="0" disableUploadTimeout="true" useBodyEncodingForURI="true" enableLookups="false" URIEncoding="UTF-8"/> <Engine name="Catalina" defaultHost="localhost"> <Realm className="org.apache.catalina.realm.LockOutRealm"> <Realm className="org.apache.catalina.realm.UserDatabaseRealm" resourceName="UserDatabase"/> </Realm> <Host name="localhost" appBase="/data/wwwroot/default" unpackWARs="true" autoDeploy="true"> <Context path="" docBase="/data/wwwroot/default" debug="0" reloadable="false" crossContext="true"/> <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs" prefix="localhost_access_log." suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" /> </Host> </Engine> </Service> </Server>
        ```

3.  Follow these steps to set JVM memory parameters:
    1.  Run `vi /usr/local/tomcat/bin/setenv.sh`.
    2.  Press the `i` key to enter the Edit mode.
    3.  Add the following content.

        ```language-bash
        	JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
        
        ```

    4.  Press the `Esc` key, and then type `:wq` to save and close the file.
4.  Follow these steps to set Tomcat automatic startup script:
    1.  Run the command to download the script: `wget https://github.com/lj2007331/oneinstack/raw/master/init.d/Tomcat-init` 
    2.  Run the command to rename Tomcat-init: `mv Tomcat-init /etc/init.d/tomcat` 
    3.  Add the permission: `chmod +x /etc/init.d/tomcat` 
    4.  Set the startup script JAVA\_HOME.

        ```
        sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_141@' /etc/init.d/tomcat
        
        ```

5.  Set automatic startup.

    ```language-bash
    chkconfig --add tomcat
    chkconfig tomcat on
    ```

6.  Start Tomcat.

    ```language-bash
    service tomcat start
    
    ```

7.  Access the instance by using http://Public IP address:8080. If the following page appears, Tomcat is installed successfully.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9766/153949587412983_en-US.png)


