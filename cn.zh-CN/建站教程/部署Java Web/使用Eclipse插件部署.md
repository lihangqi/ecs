# 使用Eclipse插件部署 {#concept_ak3_zpd_sfb .concept}

Alibaba Cloud Toolkit for Eclipse，简称Cloud Toolkit，是一款免费的IDE插件。当您在本地完成应用程序的开发、调试及测试后，通过该插件即可轻松将应用程序部署到ECS实例。本篇教程介绍了如何在ECS实例上使用Eclipse插件部署一个Java应用。

本篇教程将向您介绍如何在Windows系统下的Eclipse中安装Cloud Toolkit，并使用Cloud Toolkit快速部署一个应用。

## 安装Cloud Toolkit {#section_hw2_ksd_sfb .section}

**准备工作**

1.  下载并安装[JDK 1.8 或更高版本](http://java.com/zh_CN/download/)。
2.  下载并安装适用于Java EE开发人员的[Eclipse IDE 4.5.0或更高版本](http://www.eclipse.org/downloads/)。

**安装步骤**

1.  启动Eclipse。
2.  在菜单栏中选中**Help** \> **Install New Software...**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321121799_zh-CN.png)

3.  单击**Add...**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321130980_zh-CN.png)

4.  输入名称（例如Cloud Toolkit for Eclipse）以及下载地址http://toolkit.aliyun.com/eclipse，并单击**Add**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321131037_zh-CN.png)

5.  勾选需要的组件**Alibaba Cloud Toolkit Core**和**Alibaba Cloud Toolkit Deployment Tools**，并在下方**Details** 区域中取消勾选**Contact all update sites during install to find required software**，然后单击**Next**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321131038_zh-CN.png)

6.  单击**Next**。
7.  选择**I accept the terms of the license agreement**， 然后单击**Finish**。
8.  单击**Install anyway**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321130612_zh-CN.png)

9.  单击**Restart Now**重启Eclipse。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321121860_zh-CN.png)


工具栏中出现Alibaba Cloud Toolkit for Eclipse的图标，表示Cloud Toolkit插件安装完成。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321221861_zh-CN.png)

## 设置 AccessKey {#section_ox1_mq2_sfb .section}

AccessKeyID和AccessKeySecret 由阿里云官方颁发给访问者。AccessKeyID用于标识访问者的身份，AccessKeySecret用于加密签名字符串和服务器端验证签名字符串的密钥，必须严格保密。

设置AccessKeyID和AccessKeySecret步骤如下：

1.  在Eclipse工具栏单击Alibaba Cloud Toolkit图标，在下拉菜单中单击**Alibaba Cloud Preference...**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321230995_zh-CN.png)

2.  在左侧导航栏中，单击**Accounts**。
3.  输入AccessKeyID和AccessKeySecret，然后单击**Apply and Close**完成设置。。

    **说明：** 如果您已有账号，但未创建AccessKey，单击**Get existing AK/SK**，然后登录阿里云控制台[创建AccessKey](../../../../../cn.zh-CN/通用参考/创建AccessKey.md#)。如果您还没有注册账号，单击**Sign up**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321230215_zh-CN.png)


## ECS环境配置 {#section_n5f_bwl_sfb .section}

本次环境配置示例步骤中使用了以下版本的软件。操作时，请您以实际软件版本为准。

-   操作系统：CentOS 7.4
-   Tomcat 版本：Tomcat 8.5.34
-   JDK 版本：JDK 1.8.0\_191

**下载源代码**

1.  下载[Apache Tomcat](https://mirrors.aliyun.com/apache/tomcat/tomcat-8/v8.5.34/bin/apache-tomcat-8.5.34.tar.gz)。

    **说明：** 源代码版本会不断升级。您可以在[https://mirrors.aliyun.com/apache/tomcat/tomcat-8/](https://mirrors.aliyun.com/apache/tomcat/tomcat-8/)获取合适的安装包地址。

2.  下载[JDK安装压缩包](https://www.oracle.com/technetwork/java/javase/downloads/index.html)。

    **说明：** 如果在ECS实例中下载JDK安装压缩包，解压缩时会出错。您可以下载JDK安装压缩包到本地，再上传到实例上。

3.  登录[ECS管理控制台](https://ecs.console.aliyun.com/)。
4.  在左边导航栏中，单击**实例**，进入ECS实例列表页。
5.  选择地域，找到ECS实例，并在**IP 地址**列获取该实例的公网 IP 地址。
6.  在Winscp工具里用公网IP地址连接Linux实例，然后将JDK安装压缩包上传到Linux实例的根目录下。

**安装前准备**

1.  [使用管理终端连接ECS实例](../cn.zh-CN/用户指南/连接实例/使用管理终端连接ECS实例.md#)。
2.  参考[添加安全组规则](../cn.zh-CN/用户指南/安全组/添加安全组规则.md#)，放行所需端口入方向规则。
3.  关闭防火墙。

    输入`systemctl status firewalld`命令查看当前防火墙的状态。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64105/154478321232172_zh-CN.png)

    如果防火墙的状态参数是active，则防火墙为开启状态。如果防火墙的状态参数是inactive，则防火墙为关闭状态。如上图所示，此处防火墙为开启状态，需要运行如下命令关闭防火墙：

    -   如果您想临时关闭防火墙，输入命令`systemctl stop firewalld`。

        **说明：** 这只是暂时关闭防火墙，下次重启Linux后，防火墙还会开启。

    -   如果您想永久关闭防火墙，输入命令`systemctl disable firewalld`。

        **说明：** 您可参考[firewalld官网](https://firewalld.org/)信息来决定何时开启防火墙。

4.  关闭SELinux。
    1.  运行`getenforce`命令查看当前SELinux的状态。如果显示`Disabled`，则SELinux为关闭状态。如果显示`Enforcing`，则SELinux为开启状态，运行如下命令关闭SELinux：
        -   如果您想临时关闭SELinux，输入命令`setenforce 0`。

            **说明：** 这只是暂时关闭SELinux，下次重启Linux后，SELinux依旧会开启。

        -   如果您想永久关闭SELinux，输入命令`vi /etc/selinux/config`编辑SELinux配置文件。回车后，把光标移动到`SELINUX=enforcing`这一行，按下i进入编辑模式，修改为`SELINUX=disabled`，按`Esc`键，然后输入`:wq`并回车以保存并关闭SELinux配置文件。

            **说明：** 您可参考redhat关于[SELinux的官方文档](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/5/html/deployment_guide/ch-selinux#s1-SELinux-resources)来决定何时开启SELinux。

    2.  重启系统使设置生效。
5.  创建用户www来运行Tomcat。

    ```
    useradd www
    ```

6.  创建网站根目录。

    ```
    mkdir -p /data/wwwroot/default
    ```

7.  将网站根目录下文件权限改为 www：

    ```
    chown -R www.www /data/wwwroot
    ```


**安装 JDK**

1.  新建一个目录。

    ```
    mkdir /usr/java
    ```

2.  解压JDK安装压缩包（本例中为jdk-8u191-linux-x64.tar.gz）到/usr/java。

    ```
    chmod +x jdk-8u191-linux-x64.tar.gz
    tar xzf jdk-8u191-linux-x64.tar.gz -C /usr/java
    ```

3.  设置环境变量。
    1.  打开/etc/profile：`vi /etc/profile`。
    2.  按下`i`键进入编辑模式。
    3.  在/etc/profile 文件中添加以下信息。

        ```
        # set java environment
        export JAVA_HOME=/usr/java/jdk1.8.0_191
        export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
        export PATH=$JAVA_HOME/bin:$PATH
        ```

    4.  按下`Esc` 键退出编辑模式，输入`:wq` 保存并退出编辑。
4.  加载环境变量： `source /etc/profile`。
5.  运行`java -version`命令，显示JDK版本信息时，表示 JDK 已经安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9766/154478321230641_zh-CN.png)


**安装 Apache Tomcat**

1.  依次运行以下命令解压apache-tomcat-8.5.34.tar.gz，重命名Tomcat目录，并设置用户权限。

    ```
    tar xzf apache-tomcat-8.5.34.tar.gz
    mv apache-tomcat-8.5.34 /usr/local/tomcat/
    chown -R www.www /usr/local/tomcat/
    ```

    在/usr/local/tomcat/目录中：

    -   bin：存放Tomcat的一些脚本文件，包含启动和关闭Tomcat服务脚本。
    -   conf：存放Tomcat服务器的各种全局配置文件，其中最重要的是server.xml和web.xml。
    -   webapps：Tomcat 的主要 Web 发布目录，默认情况下把 Web 应用文件放于此目录。
    -   logs：存放 Tomcat 执行时的日志文件。
2.  配置server.xml文件。
    1.  切换到/usr/local/tomcat/conf/目录：`cd /usr/local/tomcat/conf/`。
    2.  重命名server.xml文件：`mv server.xml server.xml_bk`。
    3.  创建一个新的server.xml文件：

        1.  运行命令`vi server.xml`。
        2.  按下`i`键进入编辑模式。
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

    4.  按下`Esc`键退出编辑模式，输入`:wq`保存并退出编辑。
3.  设置JVM 内存参数。
    1.  运行命令`vi /usr/local/tomcat/bin/setenv.sh`， 创建/usr/local/tomcat/bin/setenv.sh。
    2.  按下`i`键进入编辑模式。
    3.  添加以下内容：

        ```
        JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
        ```

    4.  按下`Esc`键退出编辑模式，输入`:wq`保存并退出编辑。
4.  设置Tomcat自启动脚本。
    1.  下载脚本：`wget https://github.com/lj2007331/oneinstack/raw/master/init.d/Tomcat-init` 
    2.  重命名 Tomcat-init：`mv Tomcat-init /etc/init.d/tomcat` 
    3.  添加执行权限：`chmod +x /etc/init.d/tomcat` 
    4.  运行以下命令，设置启动脚本JAVA\_HOME。

        ```
        sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_191@' /etc/init.d/tomcat
        
        ```

5.  设置自启动。

    ```
    chkconfig --add tomcat
    chkconfig tomcat on
    ```

6.  启动Tomcat。

    ```
    service tomcat start
    ```


## 部署Java应用程序到ECS实例 {#section_itb_pr1_tfb .section}

您可参照以下步骤用Cloud Toolkit将Java应用程序部署到ECS实例，部署完成后，您访问`http://公网IP:8080`时，会显示`Tomcat test`。

1.  在Eclipse中右键单击要部署的应用工程名，在右键菜单中单击**Alibaba Cloud** \> **Deploy to ECS...**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321230615_zh-CN.png)

2.  在Deploy to Alibaba Cloud对话框中，您可以做如下设置：

    -   **Deploy File**：选择部署方式。本示例中，选择**Upload File**。如果您的应用工程是采用Maven构建的，请您选择**Maven Build**。
    -   **Choose File**：选择要部署的文件。
    -   **Target Deploy ECS**：选择您的实例所在的地域，并选择实例。
    -   **Deploy Location**：填入部署在ECS实例上的目录，本示例中，目录为/data/wwwroot/default。
    -   **Command**：单击**Select...**，在弹出的对话框中单击**Add...**。在文本框里输入一个命令，这个命令会在Cloud Toolkit插件把Java应用程序部署到ECS的文件夹后自动执行。本示例中，输入`service tomcat restart`命令来重启Tomcat。您可根据您的需求输入要执行的命令。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321230623_zh-CN.png)

3.  单击**Deploy**开始部署Java应用程序到ECS实例。
4.  在Eclipse的**Console**区域，你可以查看部署的进展信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/154478321230632_zh-CN.png)

5.  在浏览器地址栏中输入`http://公网IP:8080`进行访问。

出现如下图所示页面，表示成功用Alibaba Cloud Toolkit for Eclipse插件部署Java应用程序到ECS实例。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9766/154478321212137_zh-CN.png)

如果您要修改Java应用程序，可在Eclipse中直接修改，然后保存代码，再次用Cloud Toolkit插件将改动过的文件部署到ECS实例上。

