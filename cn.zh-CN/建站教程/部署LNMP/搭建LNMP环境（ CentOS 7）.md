# 搭建LNMP环境（ CentOS 7） {#concept_fnh_v3x_5fb .concept}

Nginx是一个小巧而高效的Linux下的Web服务器软件,可以帮助您在Linux系统下快速方便地搭建出LNMP Web服务环境。本教程介绍如何手动在ECS实例上搭建LNMP环境，其中LNMP分别代表Linux、 Nginx、MySQL和PHP。

## 项目配置 {#section_mrn_4dv_vfb .section}

本篇教程在示例步骤中使用了以下版本的软件：

-   操作系统：公共镜像 CentOS 7.2 64位
-   Nginx版本：Nginx 1.12.2
-   MySQL版本：MySQL 5.7.25
-   PHP版本：PHP 7.0.33

本篇教程在示例步骤中使用了以下配置的ECS实例：

-   CPU：2 vCPU
-   内存：4 GiB
-   网络类型：专有网络
-   IP地址：公网IP

## 适用对象 {#section_pmz_2x2_2fb .section}

适用于熟悉Linux操作系统，刚开始使用阿里云进行建站的个人用户。

## 前提条件 {#section_3do_4h1_tfn .section}

您已在ECS实例所使用的安全组入方向添加规则放行端口80和3306。具体操作步骤，请参见[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

## 基本流程 {#section_ghz_hx2_2fb .section}

使用云服务器ECS手动搭建LNMP平台的操作步骤如下：

1.  准备编译环境。
2.  安装Nginx。
3.  安装MySQL。
4.  安装PHP。
5.  配置Nginx。
6.  配置MySQL。
7.  配置PHP。
8.  测试访问。

您也可以在[云市场](https://market.aliyun.com/software)购买LNMP镜像直接启动ECS，以便快速建站。

## 步骤一：准备编译环境 {#section_ucf_8l3_pul .section}

1.  [使用SSH密钥对连接Linux实例](../../../../cn.zh-CN/实例/连接实例/连接Linux实例/使用SSH密钥对连接Linux实例.md#)或[使用用户名密码验证连接Linux实例](../../../../cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)。
2.  关闭防火墙。
    1.  输入`systemctl status firewalld`命令查看当前防火墙的状态。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64105/155869165032172_zh-CN.png)

    2.  如果防火墙的状态参数是inactive，则防火墙为关闭状态， 可跳过此步骤。如果防火墙的状态参数是active，则防火墙为开启状态。如上图所示，此处防火墙为开启状态，需要运行如下命令关闭防火墙：
        -   如果您想临时关闭防火墙，输入命令`systemctl stop firewalld`。

            **说明：** 这只是暂时关闭防火墙，下次重启Linux后，防火墙还会开启。

        -   如果您想永久关闭防火墙，输入命令`systemctl disable firewalld`。

            **说明：** 您可参考[firewalld官网](https://firewalld.org/)信息来决定何时开启防火墙。

3.  关闭SELinux。
    1.  运行`getenforce`命令查看SELinux的当前状态。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9763/155869165021065_zh-CN.png)

    2.  如果SELinux状态参数是Disabled， 则SELinux为关闭状态，可跳过此步骤。如果SELinux状态参数是Enforcing，则SELinux为开启状态。如上图所示，此处SELinux为开启状态，需要运行如下命令关闭SELinux：
        -   如果您想临时关闭SELinux，输入命令`setenforce 0`。

            **说明：** 这只是暂时关闭SELinux，下次重启Linux后，SELinux还会开启。

        -   如果您想永久关闭SELinux，输入命令`vi /etc/selinux/config`编辑SELinux配置文件。回车后，把光标移动到`SELINUX=enforcing`这一行，按下`i`键进入编辑模式，修改为`SELINUX=disabled`， 按下`Esc`键，然后输入`:wq`并回车以保存并关闭SELinux配置文件。

            **说明：** 您可参考redhat关于[SELinux的官方文档](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/5/html/deployment_guide/ch-selinux#s1-SELinux-resources)来决定何时开启SELinux。

    3.  重启系统使设置生效。

## 步骤二：安装Nginx {#section_k4c_fpk_s9c .section}

1.  运行以下命令安装Nginx。

    ``` {#codeblock_mm5_52p_id8}
    yum -y install nginx
    ```

2.  运行以下命令查看Nginx版本。

    ``` {#codeblock_pzg_a2b_k9a}
    nginx -v                            
    ```

    返回结果如下所示，表示Nginx安装成功。

    ``` {#codeblock_cy7_8co_14b}
    nginx version: nginx/1.12.2                            
    ```


## 步骤三：安装MySQL {#section_axa_m3u_o81 .section}

1.  运行以下命令更新YUM源。

    ``` {#codeblock_tei_2bl_bkz}
    rpm -Uvh  http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
    ```

2.  运行以下命令安装MySQL。

    ``` {#codeblock_3dg_f0x_loe}
    yum -y install mysql-community-server
    ```

3.  运行以下命令查看MySQL版本号。

    ``` {#codeblock_z1o_7ul_nfg}
    mysql -V
    ```

    返回结果如下，表示MySQL安装成功。

    ``` {#codeblock_lkj_fo3_88i}
    mysql  Ver 14.14 Distrib 5.7.25, for Linux (x86_64) using  EditLine wrapper
    ```


## 步骤四：安装PHP {#section_oiz_zvt_k79 .section}

1.  依次运行以下命令更新YUM源。

    ``` {#codeblock_93c_b7q_s2k}
    # yum install -y http://dl.iuscommunity.org/pub/ius/stable/CentOS/7/x86_64/ius-release-1.0-15.ius.centos7.noarch.rpm
    # rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
    ```

    **说明：** 本教程以`ius-release-1.0-15.ius.centos7.noarch.rpm`版本为例。实际安装过程中，请您使用最新版本ius-release软件包。

2.  运行以下命令安装PHP。

    ``` {#codeblock_v50_a09_g48}
    yum -y install php70w-devel php70w.x86_64 php70w-cli.x86_64 php70w-common.x86_64 php70w-gd.x86_64 php70w-ldap.x86_64 php70w-mbstring.x86_64 php70w-mcrypt.x86_64  php70w-pdo.x86_64   php70w-mysqlnd  php70w-fpm php70w-opcache php70w-pecl-redis php70w-pecl-mongo
    ```

3.  运行以下命令查看PHP版本。

    ``` {#codeblock_6r6_xgw_exz}
    php -v
    ```

    返回结果如下所示，表示安装成功。

    ``` {#codeblock_v91_t1r_cih}
    PHP 7.0.33 (cli) (built: Dec  6 2018 22:30:44) ( NTS )
    Copyright (c) 1997-2017 The PHP Group
    Zend Engine v3.0.0, Copyright (c) 1998-2017 Zend Technologies
        with Zend OPcache v7.0.33, Copyright (c) 1999-2017, by Zend Technologies                
    ```


## 步骤五：配置Nginx {#section_s8d_hii_4e5 .section}

1.  运行以下命令备份Nginx配置文件。

    ``` {#codeblock_yzp_5uv_4yo}
    cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
    ```

2.  运行以下命令打开Nginx配置文件。

    ``` {#codeblock_6zv_q75_ys2}
    vim /etc/nginx/nginx.conf
    ```

3.  按`i`进入编辑模式。
4.  在server大括号内，添加下列配置信息，使Nginx支持PHP请求。

    ``` {#codeblock_p2t_fz5_mxa}
            location / {
                index index.php index.html index.htm;
            }
            #配置Nginx通过fastcgi方式处理您的PHP请求
            location ~ .php$ {
                root /usr/share/php;
                fastcgi_pass 127.0.0.1:9000; #Nginx通过本机的9000端口将PHP请求转发给PHP-FPM进行处理。
                fastcgi_index index.php;
                fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
                include fastcgi_params;  #Nginx调用fastcgi接口处理PHP请求
            }                
    ```

    **说明：** 若不添加此配置信息，则会导致Nginx无法处理您的PHP请求，即您请求的PHP页面将无法打开。

5.  运行以下命令启动Nginx服务。

    ``` {#codeblock_zis_eg6_rch}
    systemctl start nginx
    ```

6.  运行以下命令添加Nginx服务开机自启动。

    ``` {#codeblock_8iv_yvk_zul}
    systemctl enable nginx
    ```


## 步骤六：配置MySQL {#section_goj_i3b_qdx .section}

1.  运行以下命令启动MySQL服务。

    ```
    systemctl start mysqld
    ```

2.  运行以下命令设置MySQL服务开机自启动。

    ``` {#codeblock_aaq_x7y_d7o}
    systemctl enable mysqld
    ```

3.  运行以下命令查看/var/log/mysqld.log文件，获取并记录root用户的初始密码。

    ```
    # grep 'temporary password' /var/log/mysqld.log
    2016-12-13T14:57:47.535748Z 1 [Note] A temporary password is generated for root@localhost: p0/G28g>lsHD
    ```

    **说明：** 下一步重置root用户密码时，会使用该初始密码。

4.  运行下列命令配置MySQL的安全性。

    ``` {#codeblock_vs0_nak_g5n}
    mysql_secure_installation
    ```

    安全性的配置包含以下五个方面：

    1.  重置root账号密码。

        ``` {#codeblock_qmi_g87_eim}
        Enter password for user root: #输入上一步获取的root用户初始密码
        The 'validate_password' plugin is installed on the server.
        The subsequent steps will run with the existing configuration of the plugin.
        Using existing password for root.
        Estimated strength of the password: 100 
        Change the password for root ? ((Press y|Y for Yes, any other key for No) : Y #是否更改root用户密码，输入Y
        New password: #输入新密码，长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号。特殊符号可以是()` ~!@#$%^&*-+=|{}[]:;‘<>,.?/
        Re-enter new password: #再次输入新密码
        Estimated strength of the password: 100 
        Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y
        ```

    2.  输入`Y`删除匿名用户账号。

        ``` {#codeblock_l8a_6bl_whx}
        By default, a MySQL installation has an anonymous user, allowing anyone to log into MySQL without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother. You should remove them before moving into a production environment.
        Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y  #是否删除匿名用户，输入Y
        Success.
        ```

    3.  输入`Y`禁止root账号远程登录。

        ``` {#codeblock_dip_16q_xty}
        Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y #禁止root远程登录，输入Y
        Success.
        ```

    4.  输入`Y`删除test库以及对test库的访问权限。

        ``` {#codeblock_hw6_3f5_dok}
        Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y #是否删除test库和对它的访问权限，输入Y
        - Dropping test database...
        Success.
        ```

    5.  输入`Y`重新加载授权表。

        ``` {#codeblock_xg0_kp8_y7y}
        Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y #是否重新加载授权表，输入Y
        Success.
        All done!
        ```

    更多详情，请参见[官方文档](http://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html)。


## 步骤七：配置PHP {#section_vb1_xud_6x4 .section}

1.  在/usr/share/php目录下新建phpinfo.php文件，用于展示phpinfo信息。具体步骤如下：
    1.  运行`vim /usr/share/php/phpinfo.php`命令打开文件。
    2.  按`i`进入编辑模式。
    3.  输入下列内容。

        ``` {#codeblock_ij8_lhu_gbb}
        <?php echo phpinfo(); ?>
        ```

    4.  按`：wq`保存并退出。
2.  运行以下命令启动PHP-FPM。

    ``` {#codeblock_629_nxj_p8w}
    systemctl start php-fpm
    ```

3.  运行以下命令设置PHP-FPM开机自启动。

    ``` {#codeblock_641_cgj_xo7}
    systemctl enable php-fpm
    ```


## 步骤八：测试访问 {#section_d8a_adj_z1v .section}

1.  打开浏览器。
2.  在地址栏输入`http://<ECS实例公网IP地址>/phpinfo.php`。

    返回结果如下图所示，表示LNMP环境部署成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/64105/155869165044922_zh-CN.png)


## 下一步 {#section_pbt_ozb_ge7 .section}

测试访问LNMP平台成功后，建议您运行以下命令将/usr/share/php/phpinfo.php文件删除，以避免安全隐患。

``` {#codeblock_59p_7tt_do3}
rm -rf /usr/share/php/phpinfo.php
```

