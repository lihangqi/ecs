# 手工部署Java Web项目 {#concept_51376_zh .concept}

本文档介绍如何使用一台基本配置的云服务器 ECS 实例部署 Java web 项目。适用于刚开始使用阿里云进行建站的个人用户。

## 项目配置 { .section}

本篇教程在示例步骤中使用了以下版本的软件。操作时，请您以实际软件版本为准。

-   操作系统：CentOS 7.4
-   Tomcat 版本：Tomcat 8.5.34
-   JDK 版本：JDK 1.8.0\_191

## 安装前准备 { .section}

-   CentOS 7.4 系统默认开启了防火墙。您可以关闭防火墙，也可以参考官网文档在防火墙里添加规则，放行 80、443 或 8080 端口入方向规则。
    -   关闭防火墙：

        ```language-bash
        # systemctl stop firewalld.service
        
        ```

    -   关闭防火墙开机自启动功能：

        ```language-bash
        # systemctl disable firewalld.service
        
        ```

-   创建一般用户 www来运行Tomcat：

    ```language-bash
    # useradd www
    
    ```

-   在安全组中放行 8080 端口。具体操作，请参考 [添加安全组规则](../cn.zh-CN/用户指南/安全组/添加安全组规则.md#)。
-   创建网站根目录：

    ```language-bash
    # mkdir -p /data/wwwroot/default
    
    ```

-   在网站根目录下新建 Tomcat 测试页面，然后将网站根目录下文件权限改为 www：

    ```language-bash
    # echo Tomcat test > /data/wwwroot/default/index.jsp
    chown -R www.www /data/wwwroot
    ```


## 下载源代码 { .section}

1.  下载 Apache

    ```language-bash
    # wget https://mirrors.aliyun.com/apache/tomcat/tomcat-8/v8.5.34/bin/apache-tomcat-8.5.34.tar.gz
    
    ```

    源代码版本会不断升级。您可以在 https://mirrors.aliyun.com/apache/tomcat/tomcat-8/ 目录下获取合适的安装包地址。

2.  下载 JDK
    1.  下载JDK安装压缩包[jdk-8u191-linux-x64 .tar.gz](https://www.oracle.com/technetwork/cn/java/javase/downloads/index-jsp-138363-zhs.html):

        **说明：** 直接用`# wget`命令在实例中下载JDK安装压缩包，在解压缩时会出错。您可以下载JDK安装压缩包,再上传到实例上。

    2.  登录 [[ECS管理控制台](https://ecs.console.aliyun.com/)ECS 管理控制台](https://ecs.console.aliyun.com/#/home)。
    3.  在左边导航栏中，单击 **实例**，进入 ECS 实例列表页。
    4.  选择所购 ECS 实例所在的地域，找到已购的 ECS 实例，在 **IP 地址** 列获取该实例的公网 IP 地址。
    5.  在Winscp工具里用公网 IP 地址连接Linux实例，然后将下载好的JDK安装压缩包上传到Linux实例的根目录下。

## 安装 JDK { .section}

按以下步骤安装 JDK。

1.  新建一个目录：

    ```language-bash
    # mkdir /usr/java
    
    ```

2.  解压 jdk-8u191-linux-x64.tar.gz 到 /usr/java。

    ```language-bash
    # tar xzf jdk-8u191-linux-x64.tar.gz -C /usr/java
    
    ```

3.  设置环境变量：
    1.  打开 /etc/profile：`# vi /etc/profile`。
    2.  按 `i` 键进入编辑模式。
    3.  在 /etc/profile 文件中添加以下信息：

        ```language-bash
        #set java environment
        export JAVA_HOME=/usr/java/jdk1.8.0_191
        export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
        export PATH=$JAVA_HOME/bin:$PATH
        ```

    4.  按 `Esc` 键退出编辑模式，输入 `:wq` 保存并关闭文件。
4.  加载环境变量： `# source /etc/profile`。
5.  查看 jdk 版本。当出现 jdk 版本信息时，表示 JDK 已经安装成功。

    ```language-bash
    # java -version
    
    ```

    ```language-bash
    java -version
    java version "1.8.0_191"
    Java(TM) SE Runtime Environment (build 1.8.0_191-b12)
    Java HotSpot(TM) 64-Bit Server VM (build 25.191-b12, mixed mode)
    ```


## 安装 Tomcat { .section}

按以下步骤安装 Tomcat。

1.  依次运行以下命令解压 apache-tomcat-8.5.34.tar.gz，重命名 Tomcat 目录，并设置用户权限。

    ```language-bash
    # tar xzf apache-tomcat-8.5.34.tar.gz
    # mv apache-tomcat-8.5.34 /usr/local/tomcat/
    # chown -R www.www /usr/local/tomcat/
    ```

    在 /usr/local/tomcat/ 目录中：

    -   bin：存放 Tomcat 的一些脚本文件，包含启动和关闭 Tomcat 服务脚本。
    -   conf：存放 Tomcat 服务器的各种全局配置文件，其中最重要的是 server.xml 和 web.xml。
    -   webapps：Tomcat 的主要 Web 发布目录，默认情况下把 Web 应用文件放于此目录。
    -   logs：存放 Tomcat 执行时的日志文件。
2.  配置 server.xml文件：
    1.  切换到 /usr/local/tomcat/conf/ 目录：`# cd /usr/local/tomcat/conf/`。
    2.  重命名 server.xml文件：`# mv server.xml server.xml_bk`。
    3.  创建一个新的 server.xml文件：

        1.  运行命令 `# vi server.xml`。
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
    1.  运行命令 `# vi /usr/local/tomcat/bin/setenv.sh`， 创建 /usr/local/tomcat/bin/setenv.sh。
    2.  按 `i` 键进入编辑模式。
    3.  添加以下内容：

        ```language-bash
        JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
        
        ```

    4.  按 `Esc` 键退出编辑模式，输入 `:wq` 保存并退出文件。
4.  设置 Tomcat 自启动脚本。
    1.  下载脚本：`# wget https://github.com/lj2007331/oneinstack/raw/master/init.d/Tomcat-init` 
    2.  重命名 Tomcat-init：`# mv Tomcat-init /etc/init.d/tomcat` 
    3.  添加执行权限：`# chmod +x /etc/init.d/tomcat` 
    4.  运行以下命令，设置启动脚本 JAVA\_HOME。

        ```
        # sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_191@' /etc/init.d/tomcat
        
        ```

5.  设置自启动。

    ```language-bash
    # chkconfig --add tomcat
    # chkconfig tomcat on
    ```

6.  启动 Tomcat。

    ```language-bash
    # service tomcat start
    
    ```

7.  在浏览器地址栏中输入 http://公网IP:8080 进行访问。出现如图所示页面时表示安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9766/154149765312137_zh-CN.png)


