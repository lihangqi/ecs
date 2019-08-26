# 手工部署Java Web项目 {#concept_51376_zh .concept}

本文档介绍如何使用一台基本配置的云服务器 ECS 实例部署 Java web 项目。适用于刚开始使用阿里云进行建站的个人用户。

## 项目配置 { .section}

此处列出验证本文档操作时使用的软件版本。操作时，请您以实际软件版本为准。

-   操作系统：CentOS 7.4
-   Tomcat 版本：Tomcat 8.5.23
-   JDK 版本：JDK 1.8.0\_141

## 安装前准备 { .section}

-   CentOS 7.4 系统默认开启了防火墙。您可以关闭防火墙，也可以参考官网文档在防火墙里添加规则，放行 80、443 或 8080 端口入方向规则。
    -   关闭防火墙：

        ```language-bash
        systemctl stop firewalld.service
        
        ```

    -   关闭防火墙开机自启动功能：

        ```language-bash
        systemctl disable firewalld.service
        
        ```

-   创建一般用户 www，运行 tomcat：

    ```language-bash
    useradd www
    
    ```

-   在安全组中放行 8080 端口。具体操作，请参考 [添加安全组规则](../../../../intl.zh-CN/用户指南/安全组/添加安全组规则.md#)。
-   创建网站根目录：

    ```language-bash
    mkdir -p /data/wwwroot/default
    
    ```

-   新建 Tomcat 测试页面：

    ```language-bash
    echo Tomcat test > /data/wwwroot/default/index.jsp
    chown -R www.www /data/wwwroot
    ```


## 下载源代码 { .section}

**下载 Apache**

```language-bash
wget https://mirrors.aliyun.com/apache/tomcat/tomcat-8/v8.5.23/bin/apache-tomcat-8.5.23.tar.gz

```

源代码版本会不断升级。您可以在 https://mirrors.aliyun.com/apache/tomcat/tomcat-8/ 目录下获取合适的安装包地址。

**下载 JDK**

```language-bash
wget http://mirrors.linuxeye.com/jdk/jdk-8u141-linux-x64.tar.gz

```

源代码版本会不断升级。您可以在 http://mirrors.linuxeye.com/jdk/ 目录下获取合适的安装包地址。

## 安装 JDK { .section}

按以下步骤安装 JDK。

1.  新建一个目录：

    ```language-bash
    mkdir /usr/java
    
    ```

2.  解压 jdk-8u141-linux-x64.tar.gz 到 /usr/java。

    ```language-bash
    tar xzf jdk-8u141-linux-x64.tar.gz -C /usr/java
    
    ```

3.  设置环境变量：
    1.  打开 /etc/profile：`vi /etc/profile`。
    2.  按 `i` 键进入编辑模式。
    3.  在 /etc/profile 文件中添加以下信息：

        ```language-bash
        #set java environment
        export JAVA_HOME=/usr/java/jdk1.8.0_141
        export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
        export PATH=$JAVA_HOME/bin:$PATH
        ```

    4.  按 `Esc` 键退出编辑模式，输入 `:wq` 保存并关闭文件。
4.  加载环境变量： `source /etc/profile`。
5.  查看 jdk 版本。当出现 jdk 版本信息时，表示 JDK 已经安装成功。

    ```language-bash
    java -version
    
    ```

    ```language-bash
    java -version
    java version "1.8.0_141"
    Java(TM) SE Runtime Environment (build 1.8.0_141-b15)
    Java HotSpot(TM) 64-Bit Server VM (build 25.141-b15, mixed mode)
    ```


## 安装 Tomcat { .section}

按以下步骤安装 Tomcat。

1.  依次运行以下命令解压 apache-tomcat-8.5.23.tar.gz，重命名 Tomcat 目录，并设置用户权限。

    ```language-bash
    tar xzf apache-tomcat-8.5.23.tar.gz
    mv apache-tomcat-8.5.23 /usr/local/tomcat/
    chown -R www.www /usr/local/tomcat/
    ```

    **说明：** 在 /usr/local/tomcat/ 目录里：

    -   bin：存放 Tomcat 的一些脚本文件，包含启动和关闭 Tomcat 服务脚本。
    -   conf：存放 Tomcat 服务器的各种全局配置文件，其中最重要的是 server.xml 和 web.xml。
    -   webapps：Tomcat 的主要 Web 发布目录，默认情况下把 Web 应用文件放于此目录。
    -   logs：存放 Tomcat 执行时的日志文件。
2.  配置 server.xml 文件：
    1.  切换到 /usr/local/tomcat/conf/ 目录：`cd /usr/local/tomcat/conf/`。
    2.  重命名 server.xml 文件：`mv server.xml server.xml_bk`。
    3.  创建一个新的 server.xml 文件：

        1.  运行命令 `vi server.xml`。
        2.  单击 `i` 键进入编辑模式。
        3.  添加以下内容：
        ```
        <?xml version="1.0" encoding="UTF-8"?>
        <Server port="8006" shutdown="SHUTDOWN">
        <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener"/>
        <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener"/>
        <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener"/>
        <Listener className="org.apache.catalina.core.AprLifecycleListener"/>
        <GlobalNamingResources>
        <Resource name="UserDatabase" auth="Container"
         type="org.apache.catalina.UserDatabase"
         description="User database that can be updated and saved"
         factory="org.apache.catalina.users.MemoryUserDatabaseFactory"
         pathname="conf/tomcat-users.xml"/>
        </GlobalNamingResources>
        <Service name="Catalina">
        <Connector port="8080"
         protocol="HTTP/1.1"
         connectionTimeout="20000"
         redirectPort="8443"
         maxThreads="1000"
         minSpareThreads="20"
         acceptCount="1000"
         maxHttpHeaderSize="65536"
         debug="0"
         disableUploadTimeout="true"
         useBodyEncodingForURI="true"
         enableLookups="false"
         URIEncoding="UTF-8"/>
        <Engine name="Catalina" defaultHost="localhost">
        <Realm className="org.apache.catalina.realm.LockOutRealm">
        <Realm className="org.apache.catalina.realm.UserDatabaseRealm"
          resourceName="UserDatabase"/>
        </Realm>
        <Host name="localhost" appBase="/data/wwwroot/default" unpackWARs="true" autoDeploy="true">
        <Context path="" docBase="/data/wwwroot/default" debug="0" reloadable="false" crossContext="true"/>
        <Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
        prefix="localhost_access_log." suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
        </Host>
        </Engine>
        </Service>
        </Server>
        ```

3.  设置 JVM 内存参数：
    1.  运行命令 `vi /usr/local/tomcat/bin/setenv.sh`， 创建 /usr/local/tomcat/bin/setenv.sh。
    2.  按 `i` 键进入编辑模式。
    3.  添加以下内容：

        ```language-bash
        JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
        
        ```

    4.  按 `Esc` 键退出编辑模式，输入 `:wq` 保存并退出文件。
4.  设置 Tomcat 自启动脚本。
    1.  下载脚本：`wget https://github.com/lj2007331/oneinstack/raw/master/init.d/Tomcat-init` 
    2.  重命名 Tomcat-init：`mv Tomcat-init /etc/init.d/tomcat` 
    3.  添加执行权限：`chmod +x /etc/init.d/tomcat` 
    4.  运行以下命令，设置启动脚本 JAVA\_HOME。

        ```
        sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_141@' /etc/init.d/tomcat
        
        ```

5.  设置自启动。

    ```language-bash
    chkconfig --add tomcat
    chkconfig tomcat on
    ```

6.  启动 Tomcat。

    ```language-bash
    service tomcat start
    
    ```

7.  在浏览器地址栏中输入 http://ip:8080 进行访问。出现如图所示页面时表示安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9766/154106581412137_zh-CN.png)


