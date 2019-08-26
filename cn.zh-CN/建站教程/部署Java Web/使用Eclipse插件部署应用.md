# 使用Eclipse插件部署应用 {#concept_ak3_zpd_sfb .task}

Alibaba Cloud Toolkit for Eclipse，简称Cloud Toolkit，是一款免费的IDE插件。当您在本地完成应用程序的开发、调试及测试后，通过该插件即可轻松将应用程序部署到ECS实例。本教程介绍如何在Windows系统下的Eclipse中安装Cloud Toolkit，并使用Cloud Toolkit快速部署一个Java应用。

-   使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。
-   下载并安装[JDK 1.8 或更高版本](http://java.com/zh_CN/download/)。
-   下载并安装适用于Java EE开发人员的[Eclipse IDE 4.5.0或更高版本](http://www.eclipse.org/downloads/)。

## 操作步骤 {#section_bi1_x2j_v96 .section}

在ECS实例上使用Eclipse插件部署一个Java应用的操作步骤如下：

1.  [步骤一：安装Cloud Toolkit](#section_swe_tkc_2ir)
2.  [步骤二：设置AccessKey](#section_qb9_4j0_0r9)
3.  [步骤三：下载并上传JDK安装压缩包](#section_aux_qrq_9ny)
4.  [步骤四：完成准备工作](#section_942_mtv_3nn)
5.  [步骤五：安装JDK](#section_crs_eb3_tkq)
6.  [步骤六：安装Apache Tomcat](#section_u3u_gdp_kuc)
7.  [步骤七：部署Java应用程序到ECS实例](#section_pwr_rqr_y6f)

## 步骤一：安装Cloud Toolkit {#section_swe_tkc_2ir .section}

完成以下操作，安装Cloud Toolkit：

1.  启动Eclipse。
2.  在菜单栏中单击**Help** \> **Install New Software...**。 

    ![安装新软件](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967121799_zh-CN.png)

3.  单击**Add...**。 

    ![Add](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967130980_zh-CN.png)

4.  输入名称（例如Cloud Toolkit for Eclipse）以及下载地址http://toolkit.aliyun.com/eclipse，并单击**Add**。 

    ![编辑站点信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967231037_zh-CN.png)

5.  选择需要的组件：选中**Alibaba Cloud Toolkit Core**和**Alibaba Cloud Toolkit Deployment Tools**复选框，并在下方**Details**区域中清除**Contact all update sites during install to find required software**复选框，然后单击**Next**。 

    ![选择组件](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967231038_zh-CN.png)

6.  单击**Next**。
7.  选择**I accept the terms of the license agreement**， 然后单击**Finish**。
8.  单击**Install anyway**。 

    ![强制安装](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967230612_zh-CN.png)

9.  单击**Restart Now**重启Eclipse。 

    ![重启Eclipse](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967221860_zh-CN.png)


## 步骤二：设置AccessKey {#section_qb9_4j0_0r9 .section}

AccessKeyID和AccessKeySecret由阿里云官方颁发给访问者。AccessKeyID用于标识访问者的身份，AccessKeySecret用于加密签名字符串和服务器端验证签名字符串的密钥，必须严格保密。

完成以下操作，设置AccessKeyID和AccessKeySecret：

1.  在Eclipse工具栏，单击**Window** \> **Preferences**。 

    ![选择菜单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967230995_zh-CN.png)

2.  在左侧导航栏中，单击**Alibaba Cloud Toolkit** \> **Accounts**。
3.  输入**Access Key ID**和**Access Key Secret**，然后单击**Apply and Close**完成设置。 

    **说明：** 

    -   如果您已有账号，但未创建AccessKey，单击**Get existing AK/SK**，然后登录阿里云控制台创建AccessKey。详情请参见[创建AccessKey](../../../../../cn.zh-CN/通用参考/创建AccessKey.md#)。
    -   如果您还没有注册账号，单击**Sign up**。
    ![设置账号](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967230215_zh-CN.png)


## 步骤三：下载并上传JDK安装压缩包 {#section_aux_qrq_9ny .section}

完成以下操作，下载并上传JDK安装压缩包：

1.  下载[Apache Tomcat](https://mirrors.aliyun.com/apache/tomcat/tomcat-8/v8.5.34/bin/apache-tomcat-8.5.34.tar.gz)。 

    **说明：** 源代码版本会不断升级。您可以在[此处](https://mirrors.aliyun.com/apache/tomcat/tomcat-8/)获取合适的安装包地址。

2.  下载[JDK安装压缩包](https://www.oracle.com/technetwork/java/javase/downloads/index.html)。 

    **说明：** 如果在ECS实例中下载JDK安装压缩包，解压缩时会出错。您可以下载JDK安装压缩包到本地，再上传到实例上。

3.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。
4.  在左侧导航栏，单击**实例与镜像** \> **镜像**。
5.  在顶部状态栏处，选择地域。
6.  找到ECS实例，并在**IP 地址**列获取该实例的公网IP地址。
7.  在Winscp工具里用公网IP地址连接Linux实例，然后将JDK安装压缩包上传到Linux实例的根目录下。

## 步骤四：完成准备工作 {#section_942_mtv_3nn .section}

完成以下操作，做安装前的准备工作：

1.  [使用管理终端连接Linux实例](../cn.zh-CN/实例/连接实例/连接Linux实例/使用管理终端连接Linux实例.md#)。
2.  在安全组入方向添加规则并放行所需端口。具体操作，请参见[添加安全组规则](../cn.zh-CN/安全/安全组/添加安全组规则.md#)。
3.  关闭防火墙。 
    1.  运行systemctl status firewalld命令查看当前防火墙的状态。 

        ![查看防火墙状态](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64105/156617967332172_zh-CN.png)

        -   如果防火墙的状态参数是inactive，则防火墙为关闭状态。
        -   如果防火墙的状态参数是active，则防火墙为开启状态。本示例中防火墙为开启状态，因此需要关闭防火墙。
    2.  关闭防火墙。如果防火墙为关闭状态可以忽略此步骤。 
        -   如果您想临时关闭防火墙，运行命令systemctl stop firewalld。

            **说明：** 这只是暂时关闭防火墙，下次重启Linux后，防火墙还会开启。

        -   如果您想永久关闭防火墙，运行命令systemctl disable firewalld。

            **说明：** 如果您想重新开启防火墙，具体操作，请参见[firewalld官网信息](https://firewalld.org/)。

4.  关闭SELinux。 
    1.  运行命令getenforce查看SELinux的当前状态。 

        ![查看SELinux状态](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9763/156617967321065_zh-CN.png)

        -   如果SELinux状态参数是Disabled， 则SELinux为关闭状态。
        -   如果SELinux状态参数是Enforcing，则SELinux为开启状态。本示例中SELinux为开启状态，因此需要关闭SELinux。
    2.  关闭SELinux。如果SELinux为关闭状态可以忽略此步骤。 
        -   如果您想临时关闭SELinux，运行命令setenforce 0。

            **说明：** 这只是暂时关闭SELinux，下次重启Linux后，SELinux还会开启。

        -   如果您想永久关闭SELinux，运行命令vi /etc/selinux/config编辑SELinux配置文件。回车后，把光标移动到`SELINUX=enforcing`这一行，按`i`键进入编辑模式，修改为`SELINUX=disabled`， 按`Esc`键，然后输入`:wq`并回车来保存并关闭SELinux配置文件。

            **说明：** 如果您想重新开启SELinux，具体操作，请参见[SELinux的官方文档](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/5/html/deployment_guide/ch-selinux#s1-SELinux-resources)。

    3.  重启系统使设置生效。
5.  创建用户www来运行Tomcat。 

    ``` {#codeblock_jz5_np6_ehx}
    useradd www
    ```

6.  创建网站根目录。 

    ``` {#codeblock_ok7_o0f_arv}
    mkdir -p /data/wwwroot/default
    ```

7.  将网站根目录下文件权限改为www。 

    ``` {#codeblock_jfu_ub4_abe}
    chown -R www.www /data/wwwroot
    ```


## 步骤五：安装JDK {#section_crs_eb3_tkq .section}

完成以下操作，安装JDK：

1.  新建一个目录。 

    ``` {#codeblock_wvp_0v9_z1e}
    mkdir /usr/java
    ```

2.  解压JDK安装压缩包（本示例中为jdk-8u191-linux-x64.tar.gz）到/usr/java。 

    ``` {#codeblock_47o_ywc_jw3}
    chmod +x jdk-8u191-linux-x64.tar.gz
    tar xzf jdk-8u191-linux-x64.tar.gz -C /usr/java
    ```

3.  设置环境变量。 
    1.  运行vi /etc/profile命令打开/etc/profile。
    2.  按下`i`键进入编辑模式。
    3.  在/etc/profile文件中添加以下信息。 

        ``` {#codeblock_hg1_omf_i94}
        # set java environment
        export JAVA_HOME=/usr/java/jdk1.8.0_191
        export CLASSPATH=$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib
        export PATH=$JAVA_HOME/bin:$PATH
        ```

    4.  按下`Esc` 键退出编辑模式，输入`:wq` 保存并关闭文件。
4.  运行命令source /etc/profile加载环境变量。
5.  运行命令java -version，查看JDK版本信息。 

    当显示JDK版本信息时，表示JDK已经安装成功。

    ![安装成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9766/156617967330641_zh-CN.png)


## 步骤六：安装Apache Tomcat {#section_u3u_gdp_kuc .section}

完成以下操作，安装Apache Tomcat：

1.  依次运行以下命令解压apache-tomcat-8.5.34.tar.gz，重命名Tomcat目录，并设置用户权限。 

    ``` {#codeblock_p1m_hd2_6xt}
    tar xzf apache-tomcat-8.5.34.tar.gz
    mv apache-tomcat-8.5.34 /usr/local/tomcat/
    chown -R www.www /usr/local/tomcat/
    ```

    在/usr/local/tomcat/目录中：

    -   bin：存放Tomcat的一些脚本文件，包含启动和关闭Tomcat服务脚本。
    -   conf：存放Tomcat服务器的各种全局配置文件，其中最重要的是server.xml和web.xml。
    -   webapps：Tomcat的主要Web发布目录，默认情况下把Web应用文件放于此目录。
    -   logs：存放Tomcat执行时的日志文件。
2.  配置server.xml文件。 
    1.  运行命令cd /usr/local/tomcat/conf/切换到/usr/local/tomcat/conf/目录。
    2.  运行命令mv server.xml server.xml\_bk重命名server.xml文件。
    3.  运行命令vi server.xml打开文件。
    4.  按下`i`键进入编辑模式。
    5.  添加以下内容。 

        ``` {#codeblock_0ee_tc5_2mn}
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

    6.  按下`Esc`键退出编辑模式，输入`:wq`并回车来保存并关闭文件。
3.  设置JVM内存参数。 
    1.  运行命令vi /usr/local/tomcat/bin/setenv.sh， 创建/usr/local/tomcat/bin/setenv.sh。
    2.  按下`i`键进入编辑模式。
    3.  添加以下内容。 

        ``` {#codeblock_wjo_fbk_fig}
        JAVA_OPTS='-Djava.security.egd=file:/dev/./urandom -server -Xms256m -Xmx496m -Dfile.encoding=UTF-8'
        ```

    4.  按下`Esc`键退出编辑模式，输入`:wq`并回车来保存并关闭文件。
4.  设置Tomcat自启动脚本。 
    1.  运行命令wget https://github.com/lj2007331/oneinstack/raw/master/init.d/Tomcat-init下载脚本。
    2.  运行命令mv Tomcat-init /etc/init.d/tomcat重命名Tomcat-init。
    3.  运行命令chmod +x /etc/init.d/tomcat添加可执行权限。
    4.  运行以下命令，设置启动脚本`JAVA_HOME`。 

        ``` {#codeblock_680_9j0_apu}
        sed -i 's@^export JAVA_HOME=.*@export JAVA_HOME=/usr/java/jdk1.8.0_191@' /etc/init.d/tomcat                      
        ```

5.  设置开机自启动。 

    ``` {#codeblock_5dn_xpw_o6r}
    chkconfig --add tomcat
    chkconfig tomcat on
    ```

6.  启动Tomcat。 

    ``` {#codeblock_9br_91d_hod}
    service tomcat start
    ```


## 步骤七：部署Java应用程序到ECS实例 {#section_pwr_rqr_y6f .section}

您可参见以下步骤用Cloud Toolkit将Java应用程序部署到ECS实例，部署完成后，您访问http://公网IP:8080时，会显示`Tomcat test`。

1.  在Eclipse中右键单击要部署的应用工程名，选择**Alibaba Cloud** \> **Deploy to ECS...**。 

    ![选择菜单](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967330615_zh-CN.png)

2.  在Deploy to Alibaba Cloud对话框中，您可以做如下设置。 

    -   **Deploy File**：选择部署方式。本示例中，选择**Upload File**。如果您的应用工程是采用Maven构建的，请您选择**Maven Build**。
    -   **Choose File**：选择要部署的文件。
    -   **Target Deploy ECS**：选择您的实例所在的地域，并选择实例。
    -   **Deploy Location**：填入部署在ECS实例上的目录，本示例中，目录为/data/wwwroot/default。
    -   **Command**：单击**Select...**，在弹出的对话框中单击**Add...**。在文本框里输入一个命令，这个命令会在Cloud Toolkit插件把Java应用程序部署到ECS的文件夹后自动执行。本示例中，输入service tomcat restart命令来重启Tomcat。您可根据您的需求输入要执行的命令。
    ![输入命令](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967330623_zh-CN.png)

3.  单击**Deploy**开始部署Java应用程序到ECS实例。
4.  在Eclipse的**Console**区域，您可以查看部署的进展信息。 

    ![查看进展](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41804/156617967430632_zh-CN.png)

5.  在浏览器地址栏中输入`http://公网IP:8080`进行访问。 

    出现如下图所示页面，表示已成功用Alibaba Cloud Toolkit for Eclipse插件部署Java应用程序到ECS实例。

    ![部署成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9766/156617967412137_zh-CN.png)


如果您要修改Java应用程序，可在Eclipse中直接修改，然后保存代码，再次用Cloud Toolkit插件将改动过的文件部署到ECS实例上。

