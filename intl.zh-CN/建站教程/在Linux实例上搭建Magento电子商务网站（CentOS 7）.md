# 在Linux实例上搭建Magento电子商务网站（CentOS 7） {#concept_jny_5rl_2fb .concept}

Magento是一款开源电商网站框架，其丰富的模块化架构体系及拓展功能可为大中型站点提供解决方案。它使用PHP开发，支持版本范围从PHP 5.6到PHP 7.1，并使用MySQL存储数据。本文主要说明如何在阿里云ECS实例上搭建Magento电子商务网站，使用的操作系统为Linux CentOS 7.2 64位。

## 适用对象 {#section_its_wrl_2fb .section}

适用于熟悉ECS，熟悉Linux系统，刚开始使用阿里云进行建站的用户。

## 资源 {#section_gxm_xrl_2fb .section}

本文描述的操作涉及的Linux ECS实例配置包括：2 vCPU、4 GiB内存、Cent OS 7.2 64位操作系统、VPC网络、分配的公网IP地址。

**说明：** 用于搭建Magento 2的服务器，内存不能小于2 GiB。

根据本文搭建的Magento电子商务网站，使用的软件版本信息如下：

-   MySQL 5.7
-   PHP 7.0
-   Magento 2.1

## 前提条件 {#section_nln_zrl_2fb .section}

您已经创建了一台VPC网络类型的Linux ECS实例，详细操作，请参见 [使用向导创建实例](../../../../intl.zh-CN/用户指南/实例/创建实例/使用向导创建实例.md#)。配置包括：2 vCPU、4 GiB内存、Cent OS 7.2 64位操作系统、VPC网络、分配公网IP地址。

ECS实例所在安全组中已经添加了如下表所示的安全组规则。详细操作，请参见 [使用向导创建实例](../../../../intl.zh-CN/用户指南/实例/创建实例/使用向导创建实例.md#) 和 [添加安全组规则](../../../../intl.zh-CN/用户指南/安全组/添加安全组规则.md#)。

|服务|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
|HTTP|入方向|允许|自定义TCP|80/80|地址段访问|0.0.0.0/0|1|
|MySQL|入方向|允许|自定义TCP|3306/3306|地址段访问|0.0.0.0/0|1|

## 步骤1：安装配置LAMP平台 { .section}

本部分内容说明如何手动安装LAMP平台。您也可以在 [云市场](https://marketplace.alibabacloud.com/) 购买LAMP镜像直接启动ECS实例，以便快速建站。

1.  依次运行以下命令更新包和存储库，并安装Apache Web服务器和MySQL服务器。

    ```
    [ECS]$ yum update -y
    [ECS]$ yum install httpd –y
    [ECS]$ rpm -Uvh http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
    [ECS]$ yum -y install mysql-community-server
    ```

2.  启动HTTP和MySQL服务并设置开机自启动。

    ```
    [ECS]$ systemctl start httpd
    [ECS]$ systemctl enable httpd
    [ECS]$ systemctl start mysqld
    [ECS]$ systemctl enable mysqld
    ```

3.  编辑Apache配置文件：
    1.  运行命令 `vim /etc/httpd/conf/httpd.conf`。
    2.  按 `i` 键进入编辑模式。
    3.  做以下修改：
        -   在 `Include conf.modules.d/*.conf` 之后添加 `LoadModule rewrite_module modules/mod_rewrite.so`。
        -   将以下内容的 `AllowOverride None` 改为 `AllowOverride all`。

            ```
            Options Indexes FollowSymLinks
            #
            # AllowOverride controls what directives may be placed in .htaccess files.
            # It can be "All", "None", or any combination of the keywords:
            # Options FileInfo AuthConfig Limit
            #
            AllowOverride None
            ```

    4.  按 `Esc` 键退出编辑，并输入 `:wq` 保存并退出。
4.  查看/var/log/mysqld.log文件，获取安装MySQL时自动设置的root用户密码。

    ```
    # grep 'temporary password' /var/log/mysqld.log
    2016-12-13T14:57:47.535748Z 1 [Note] A temporary password is generated for root@localhost: p0/G28g>lsHD
    ```

5.  运行下面的命令可以从如下4个方面提高MySQL的安全性：

    -   设置root账号密码
    -   禁止root账号远程登录
    -   删除匿名用户账号
    -   删除test库以及对test库的访问权限

        详细说明可参见 [官方文档](http://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html)。

    ```
    # mysql_secure_installation
    Securing the MySQL server deployment.
    Enter password for user root: #输入第4步中获取的root用户密码
    The 'validate_password' plugin is installed on the server.
    The subsequent steps will run with the existing configuration of the plugin.
    Using existing password for root.
    Estimated strength of the password: 100 
    Change the password for root ? ((Press y|Y for Yes, any other key for No) : Y #是否更改root用户密码，输入Y
    New password: #输入密码，长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号。特殊符号可以是()` ~!@#$%^&*-+=|{}[]:;‘<>,.?/
    Re-enter new password: #再次输入密码
    Estimated strength of the password: 100 
    Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y
    By default, a MySQL installation has an anonymous user, allowing anyone to log into MySQL without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother. You should remove them before moving into a production environment.
    Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y #是否删除匿名用户，输入Y
    Success.
    Normally, root should only be allowed to connect from 'localhost'. 
    This ensures that someone cannot guess at the root password from the network.
    Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y #禁止root远程登录，输入Y
    Success.
    By default, MySQL comes with a database named 'test' that anyone can access. 
    This is also intended only for testing, and should be removed before moving into a production
    environment.
    Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y #是否删除test库和对它的访问权限，输入Y
    - Dropping test database...
    Success.
    - Removing privileges on test database...
    Success.
    Reloading the privilege tables will ensure that all changes
    made so far will take effect immediately.
    Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y #是否重新加载授权表，输入Y
    Success.
    All done!
    ```

6.  依次运行以下命令，安装PHP 7和一些所需的额外PHP扩展。

    ```
    # yum install -y http://dl.iuscommunity.org/pub/ius/stable/CentOS/7/x86_64/ius-release-1.0-14.ius.centos7.noarch.rpm
    # yum -y update
    # yum -y install php70u php70u-pdo php70u-mysqlnd php70u-opcache php70u-xml php70u-gd php70u-mcrypt php70u-devel php70u-intl php70u-mbstring php70u-bcmath php70u-json php70u-iconv
    ```

7.  查看PHP版本，以验证PHP是否已经成功安装。

    ```
    # php -v
    PHP 7.0.13 (cli) (built: Nov 10 2016 08:44:18) ( NTS )
    Copyright (c) 1997-2016 The PHP Group
    Zend Engine v3.0.0, Copyright (c) 1998-2016 Zend Technologies
     with Zend OPcache v7.0.13, Copyright (c) 1999-2016, by Zend Technologies
    ```

8.  编辑配置文件/etc/php.ini：
    1.  运行命令 `vim /etc/php.ini`。
    2.  按 `i` 进入编辑模式。
    3.  在文件最后添加以下配置：

        ```
        memory_limit = 128M #根据实际情况增加内存限制
        date.timezone = Asia/Shanghai #设置时区为上海。
        ```

9.  重启Web服务进程。

    ```
    # systemctl restart httpd
    ```


## 步骤2：创建数据库 { .section}

按以下步骤创建数据库。

1.  创建数据库及用户：为Magento数据创建一个数据库和一个数据库用户，数据库和用户名可根据实际情况修改。

    ```
    # mysql -u root -p
    Enter password: 
    mysql> CREATE DATABASE magento; #根据实例情况替换magento
    Query OK, 1 row affected (0.00 sec)
    mysql> GRANT ALL ON magento.* TO YourUser@localhost IDENTIFIED BY 'YourPass'; #根据实际情况替换YourUser和YourPass
    Query OK, 0 rows affected, 1 warning (0.00 sec)
    mysql> FLUSH PRIVILEGES;
    Query OK, 0 rows affected (0.00 sec)
    ```

2.  运行 `exit` 退出MySQL。
3.  （可选）验证新建的Magento数据库和用户是否可用。

    ```
    # mysql -u YourUser -p
    mysql> show databases;
    +--------------------+
    | Database           |
    +--------------------+
    | information_schema |
    | magento            |
    +--------------------+
    2 rows in set (0.00 sec)
    mysql> exit
    ```


## 步骤3：安装配置Composer { .section}

Composer是PHP一个包管理和包依赖管理的工具。按以下步骤安装配置Composer。

1.  安装Composer。

    ```
    # curl -sS https://getcomposer.org/installer | php
    All settings correct for using Composer
    Downloading 1.2.4...
    Composer successfully installed to: /root/composer.phar
    Use it: php composer.phar
    ```

2.  配置Composer全局使用。

    ```
    # mv /root/composer.phar /usr/bin/composer
    ```

3.  测试命令是否可用。

    ```
    # composer -v
    ______
    / ____/___  ____ ___  ____  ____  ________  _____
    / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
    / /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
    \____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                     /_/
    Composer version 1.2.4 2016-12-06 22:00:51
    ```


## 步骤4：安装配置Magento { .section}

您可以使用不同的方法安装Magento，也可以选择是否安装示例数据。如果安装Magento仅用于测试，您可以选择安装示例数据。如果是在生产环境中安装Magento，建议您安装全新的Magento，从头开始配置。

本部分介绍如何使用git下载Magento，然后使用Composer安装Magento。

1.  依次运行以下命令，通过 `git clone` 下载Magento。

    ```
    # yum -y install git
    # cd /var/www/html/
    # git clone https://github.com/magento/magento2.git
    ```

2.  （可选）将Magento切换到稳定版本。

    默认情况git下载安装Magento是一个最新的开发版本。如果您在生产环境中使用，建议切换到稳定版本，否则未来将无法升级安装。

    ```
    # cd magento2 &&  git checkout tags/2.1.0 -b 2.1.0
    Switched to a new branch '2.1.0'
    ```

3.  将安装文件移到Web服务器根目录下。否则，您只能通过 `http://[ECS实例公网IP地址]/magento2` 访问您的Magento站点。

    ```
    # shopt -s dotglob nullglob && mv /var/www/html/magento2/* /var/www/html/ && cd ..
    ```

4.  设置Magento文件适当的权限。

    ```
    # chown -R :apache /var/www/html
    # find /var/www/html -type f -print0 | xargs -r0 chmod 640
    # find /var/www/html -type d -print0 | xargs -r0 chmod 750
    # chmod -R g+w /var/www/html/{pub,var}
    # chmod -R g+w /var/www/html/{app/etc,vendor}
    # chmod 750 /var/www/html/bin/magento
    ```

5.  运行 `composer install` 安装Magento。
6.  测试：在浏览器中访问 `http://[ECS实例公网IP地址]`，如果出现以下页面，说明Magento安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/154113585012145_zh-CN.png)

7.  单击 **Agree and Setup Magento** 开始配置Magento：按实际情况填写连接数据库信息、Web访问设置、定制商店、创建管理员账号。出现如下图所示的界面时，说明Magento配置完成。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/154113585012146_zh-CN.png)


## 步骤5：添加cron作业 { .section}

1.  运行 `crontab -u apache -e` 设置cron运行调度工作。
2.  添加以下内容。

    ```
    */10 * * * * php -c /etc /var/www/html/bin/magento cron:run
    */10 * * * * php -c /etc /var/www/html/update/cron.php
    */10 * * * * php -c /etc /var/www/html/bin/magento setup:cron:run
    ```


关于Magento上使用cron作业，请参见 [Magento官方文档](http://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cron.html)。

## 后续操作 {#section_jh3_l5l_2fb .section}

访问 `http://[ECS实例公网IP]` 可以看到如下图所示的默认主页。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/154113585012147_zh-CN.png)

访问 `http://[ECS实例公网IP]/admin`，使用您在安装过程中设置的用户名和密码，成功登录管理面板后可看到如下界面。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/154113585012148_zh-CN.png)

更多Magento配置信息，请参见 [Magento官方文档](http://devdocs.magento.com/guides/v2.1/)。

