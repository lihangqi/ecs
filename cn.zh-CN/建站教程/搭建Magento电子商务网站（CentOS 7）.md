# 搭建Magento电子商务网站（CentOS 7） {#concept_jny_5rl_2fb .concept}

Magento是一款开源电商网站框架，其丰富的模块化架构体系及拓展功能可为大中型站点提供解决方案。它使用PHP开发，支持版本范围从PHP 5.6到PHP 7.1，并使用MySQL存储数据。本教程主要介绍如何在阿里云ECS实例上搭建Magento电子商务网站。

## 适用对象 {#section_its_wrl_2fb .section}

适用于熟悉ECS、Linux系统、vim基本添加和删除命令，刚开始使用阿里云进行建站的用户。

## 项目配置 {#section_gxm_xrl_2fb .section}

本教程使用的软件版本信息如下：

-   操作系统：公共镜像CentOS 7.2 64位
-   Apache：2.4.6
-   MySQL：5.7
-   PHP：7.0
-   Composer：1.8.5
-   Magento：2.1

本教程使用的ECS实例硬件配置如下：

-   CPU：2vCPU
-   内存：4GiB
-   网络类型：VPC

**说明：** 搭建Magento服务器，所选实例规格内存不能小于2GiB。

## 前提条件 {#section_nln_zrl_2fb .section}

ECS实例所在安全组的入方向已添加规则并放行端口80和3306。详细操作，请参见[添加安全组规则](../../../../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

## 基本流程 {#section_xf2_tja_cg5 .section}

1.  [安装配置Apache](#section_gno_olp_zdk)
2.  [安装配置MySQL](#section_yyy_uy3_t68)
3.  [安装配置PHP](#section_6r1_7kt_txz)
4.  [创建magento数据库](#section_l6p_2fu_5oi)
5.  [安装配置Composer](#section_6ng_7ds_rcp)
6.  [安装配置Magento](#section_dq1_blb_8q8)
7.  [配置Magento客户端](#section_s2n_ltk_g2d)
8.  [添加cron作业](#section_kcl_jnt_ax9)

## 步骤一：安装配置Apache {#section_gno_olp_zdk .section}

1.  **安装Apache** 
    1.  运行以下命令更新包和存储库。

        ``` {#codeblock_kxq_eji_aip}
        yum update -y
        ```

    2.  运行以下命令安装Apache。

        ``` {#codeblock_85o_nbb_vsf}
        yum install httpd -y
        ```

    3.  运行以下命令查看Apache是否安装成功。

        ``` {#codeblock_nc1_knf_gy3}
        httpd -v
        ```

        返回结果如下图所示，表示安装成功。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156617975044421_zh-CN.png)

2.  **配置Apache** 
    1.  运行以下命令打开Apache配置文件。

        ``` {#codeblock_612_tm5_5rn}
        vim /etc/httpd/conf/httpd.conf
        ```

    2.  在`Include conf.modules.d/*.conf`的下一行，添加`LoadModule rewrite_module modules/mod_rewrite.so`。具体步骤如下：
        1.  移动光标到`Include conf.modules.d/*.conf`下一行的行首。
        2.  按下`i`键进入编辑模式。
        3.  输入`LoadModule rewrite_module modules/mod_rewrite.so`。
        4.  按下`Esc`键，输入`:w`并回车以保存修改。
    3.  将下列内容中的`AllowOverride None`更改为`AllowOverride All`。

        ``` {#codeblock_39s_1aq_4ws}
        # AllowOverride controls what directives may be placed in .htaccess files.
        # It can be "All", "None", or any combination of the keywords:
        # Options FileInfo AuthConfig Limit
        #
        AllowOverride None
        ```

        具体步骤如下：

        1.  运行/AllowOverride controls what命令，找到要替换的内容。
        2.  移动光标至`AllowOverride None`。
        3.  按下`R`键进入替换模式。
        4.  输入`AllowOverride All`。
    4.  按下`Esc`键后，输入`:wq`并回车以保存并关闭配置文件。
3.  **启动Apache服务** 
    1.  运行以下命令启动Apache服务。

        ``` {#codeblock_s62_gt6_tn7}
        systemctl start httpd
        ```

    2.  运行以下命令添加Apache服务开机自启动。

        ``` {#codeblock_msf_n46_j1i}
        systemctl enable httpd
        ```


## 步骤二：安装配置MySQL {#section_yyy_uy3_t68 .section}

1.  **安装MySQL** 
    1.  运行以下命令添加MySQL YUM源。

        ``` {#codeblock_ra1_dsw_aj8}
        rpm -Uvh http://dev.mysql.com/get/mysql57-community-release-el7-8.noarch.rpm
        ```

    2.  运行以下命令安装MySQL。

        ``` {#codeblock_yap_emf_crj}
        yum -y install mysql-community-server
        ```

2.  **启动MySQL服务并设置开机自启动** 
    1.  运行以下命令启动MySQL服务。

        ``` {#codeblock_mtz_coj_ffg}
        systemctl start mysqld
        ```

    2.  运行以下命令设置MySQL服务开机自启动。

        ``` {#codeblock_heu_bou_pdh}
        systemctl enable mysqld
        ```

3.  **配置MySQL** 
    1.  运行以下命令查看/var/log/mysqld.log文件，获取并记录root用户的初始密码。

        ``` {#codeblock_6hi_nwt_4f3}
        # grep 'temporary password' /var/log/mysqld.log
        2016-12-13T14:57:47.535748Z 1 [Note] A temporary password is generated for root@localhost: p0/G28g>lsHD
        ```

        **说明：** 下一步重置root用户密码时，会使用该初始密码。

    2.  运行下列命令配置MySQL的安全性。

        ``` {#codeblock_qeg_j4n_bpf}
        mysql_secure_installation
        ```

        安全性的配置包含以下五个方面：

        1.  设置root账号密码。

            ``` {#codeblock_qtp_0az_w8o}
            Enter password for user root: #输入上一步中获取的root用户密码
            The 'validate_password' plugin is installed on the server.
            The subsequent steps will run with the existing configuration of the plugin.
            Using existing password for root.
            Estimated strength of the password: 100 
            Change the password for root ? ((Press y|Y for Yes, any other key for No) : Y #是否更改root用户密码，输入Y
            New password: #输入密码，长度为8至30个字符，必须同时包含大小写英文字母、数字和特殊符号。特殊符号可以是()` ~!@#$%^&*-+=|{}[]:;‘<>,.?/
            Re-enter new password: #再次输入密码
            Estimated strength of the password: 100 
            Do you wish to continue with the password provided?(Press y|Y for Yes, any other key for No) : Y
            ```

        2.  输入`Y`删除匿名用户账号。

            ``` {#codeblock_2vn_a9k_k3b}
            By default, a MySQL installation has an anonymous user, allowing anyone to log into MySQL without having to have a user account created for them. This is intended only for testing, and to make the installation go a bit smoother. You should remove them before moving into a production environment.
            Remove anonymous users? (Press y|Y for Yes, any other key for No) : Y  #是否删除匿名用户，输入Y
            Success.
            ```

        3.  输入`Y`禁止root账号远程登录。

            ``` {#codeblock_pwo_d02_13f}
            Disallow root login remotely? (Press y|Y for Yes, any other key for No) : Y #禁止root远程登录，输入Y
            Success.
            ```

        4.  输入`Y`删除test库以及对test库的访问权限。

            ``` {#codeblock_3lr_65k_9lx}
            Remove test database and access to it? (Press y|Y for Yes, any other key for No) : Y #是否删除test库和对它的访问权限，输入Y
            - Dropping test database...
            Success.
            ```

        5.  输入`Y`重新加载授权表。

            ``` {#codeblock_g13_6su_xz9}
            Reload privilege tables now? (Press y|Y for Yes, any other key for No) : Y #是否重新加载授权表，输入Y
            Success.
            All done!
            ```

        更多详情，请参见[官方文档](http://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html)。


## 步骤三：安装配置PHP {#section_6r1_7kt_txz .section}

1.  **安装PHP** 
    1.  依次运行以下命令安装PHP YUM源。

        ``` {#codeblock_pv0_08w_s1i}
        # yum install -y http://dl.iuscommunity.org/pub/ius/stable/CentOS/7/x86_64/ius-release-1.0-14.ius.centos7.noarch.rpm
        # yum -y update
        # rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
        ```

    2.  运行以下命令安装PHP7及所需扩展。

        ``` {#codeblock_ibs_jc0_p7d}
        yum -y install php70w php70w-pdo php70w-mysqlnd php70w-opcache php70w-xml php70w-gd php70w-mcrypt php70w-devel php70w-intl php70w-mbstring php70w-bcmath php70w-json php70w-iconv
        ```

    3.  运行以下命令查看PHP版本。

        ``` {#codeblock_51y_fjj_zfb}
        php -v
        ```

        返回结果如下，说明PHP安装成功。

        ``` {#codeblock_es5_vim_zur}
        PHP 7.0.33 (cli) (built: Dec  6 2018 22:30:44) ( NTS )
        Copyright (c) 1997-2017 The PHP Group
        Zend Engine v3.0.0, Copyright (c) 1998-2017 Zend Technologies
            with Zend OPcache v7.0.33, Copyright (c) 1999-2017, by Zend Technologies                        
        ```

2.  **配置PHP** 
    1.  运行以下命令打开PHP配置文件。

        ``` {#codeblock_7mp_ckf_mcd}
        vim /etc/php.ini
        ```

    2.  移动光标至最后一行的行尾。具体操作步骤如下：
        1.  输入`:$`并回车，光标将移动至文件最后一行。
        2.  按下`$`移动光标至行尾。
    3.  按下`i`键进入编辑模式。
    4.  在文件最后添加以下配置。

        ``` {#codeblock_7oi_s5c_8ze}
        memory_limit = 1024M #您可根据实际情况增加或减少内存限制
        date.timezone = Asia/Shanghai #设置时区为上海。
        ```

        添加后如下图所示。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156617975044781_zh-CN.png)

    5.  按下`Esc`键后，输入`:wq`并回车以保存并关闭文件。
    6.  重启Web服务进程。

        ``` {#codeblock_12u_kib_d5b}
        systemctl restart httpd
        ```


## 步骤四：创建Magento数据库 {#section_l6p_2fu_5oi .section}

1.  运行以下命令使用root用户和密码登录MySQL。

    ``` {#codeblock_x0q_p1g_ups}
    mysql -u root -p
    ```

2.  运行以下命令创建`magento`数据库。

    ``` {#codeblock_v9x_1bb_1qx}
    mysql> CREATE DATABASE magento; #根据实际情况将magento替换为您需要创建的数据库名称
    ```

3.  依次运行以下命令为`magento`数据库创建用户。

    ``` {#codeblock_rmr_x5y_bix}
    mysql> GRANT ALL ON magento.* TO YourUser@localhost IDENTIFIED BY 'YourPass'; #替换YourUser和YourPass为您需要创建的账号和密码
    mysql> FLUSH PRIVILEGES;
    ```

    例如，创建账号为`magentoUser`、密码为`magentoUser1@3`的用户，运行的命令为：

    ``` {#codeblock_x0y_nnr_kjv}
    mysql> GRANT ALL ON magento.* TO magentoUser@localhost IDENTIFIED BY 'magentoUser1@3';
    mysql> FLUSH PRIVILEGES;
    ```

4.  输入`exit`并回车以退出MySQL。
5.  （可选）验证新建的Magento数据库和用户是否可用。具体步骤如下：
    1.  运行以下命令使用新建账号和密码登录MySQL。

        ``` {#codeblock_cm4_x54_1k1}
        mysql -u YourUser -p   #替换YourUser为您创建的账号
        ```

    2.  运行以下命令查看新建的`magento`数据库。

        ``` {#codeblock_tpi_jib_477}
        mysql> show databases;
        +--------------------+
        | Database           |
        +--------------------+
        | information_schema |
        | magento            |
        +--------------------+
        2 rows in set (0.00 sec)
        ```

    3.  运行以下命令并回车以退出MySQL。

        ``` {#codeblock_0zp_gcq_5h1}
        mysql> exit
        ```


## 步骤五：安装配置Composer {#section_6ng_7ds_rcp .section}

Composer是一个PHP包管理和包依赖管理的工具。请按以下步骤安装配置Composer。

1.  运行以下命令安装Composer。

    ``` {#codeblock_0rj_vzg_tpp}
    curl -sS https://getcomposer.org/installer | php
    ```

2.  运行以下命令配置Composer全局使用。

    ``` {#codeblock_xkf_57g_uim}
    mv /root/composer.phar /usr/bin/composer
    ```

3.  运行命令composer -v查看Composer版本。返回结果如下，表示Composer安装成功。

    ``` {#codeblock_m7r_3nm_lpk}
      / ____/___  ____ ___  ____  ____  ________  _____
     / /   / __ \/ __ `__ \/ __ \/ __ \/ ___/ _ \/ ___/
    / /___/ /_/ / / / / / / /_/ / /_/ (__  )  __/ /
    \____/\____/_/ /_/ /_/ .___/\____/____/\___/_/
                        /_/
    Composer version 1.8.5 2019-04-09 17:46:47
    					
    ```


## 步骤六：安装配置Magento {#section_dq1_blb_8q8 .section}

您可以使用不同的方法安装Magento，可以选择是否安装示例数据。

-   如果安装Magento仅用于测试，您可以选择安装示例数据。
-   如果安装Magento用于生产环境，建议您安装全新的Magento，从头开始配置。

本教程介绍使用git下载Magento，并使用Composer安装Magento的操作步骤。

1.  依次运行以下命令下载Magento。

    ``` {#codeblock_7hw_l72_mwa}
    yum -y install git
    ```

    ``` {#codeblock_qok_s5p_2i5}
    cd /var/www/html/
    ```

    ``` {#codeblock_mnb_tqp_owx}
    git clone https://github.com/magento/magento2.git
    ```

2.  （可选）运行以下命令将Magento切换到稳定版本。

    ``` {#codeblock_5tv_zkc_c63}
    # cd magento2 &&  git checkout tags/2.1.0 -b 2.1.0
    Switched to a new branch '2.1.0'
    ```

    **说明：** 默认情况下，git下载安装的Magento是最新的开发版本。如果您在生产环境中使用，建议切换到稳定版本，否则未来将无法升级安装。

3.  运行以下命令将安装文件移到Web服务器根目录下。

    ``` {#codeblock_4yk_9pv_q4f}
    shopt -s dotglob nullglob && mv /var/www/html/magento2/* /var/www/html/ && cd ..
    ```

    **说明：** 如果不运行此命令，您只能通过`http://[ECS实例公网IP地址]/magento2`访问您的Magento站点。

4.  依次运行下列命令为Magento文件设置适当的权限。

    ``` {#codeblock_qph_fi4_2zg}
    chown -R :apache /var/www/html
    ```

    ``` {#codeblock_z65_9nx_let}
    find /var/www/html -type f -print0 | xargs -r0 chmod 640
    ```

    ``` {#codeblock_6wf_i9g_9eb}
    find /var/www/html -type d -print0 | xargs -r0 chmod 750
    ```

    ``` {#codeblock_np6_5nv_kuh}
    chmod -R g+w /var/www/html/{pub,var}
    ```

    ``` {#codeblock_u5p_o4i_yvc}
    chmod -R g+w /var/www/html/{app/etc,vendor}
    ```

    ``` {#codeblock_iut_asm_hlv}
    chmod 750 /var/www/html/bin/magento
    ```

5.  运行命令composer install安装Magento。

## 步骤七：配置Magento客户端 {#section_s2n_ltk_g2d .section}

1.  打开浏览器。
2.  在浏览器地址栏中输入`http://[ECS实例公网IP地址]`。如果出现以下页面，说明Magento安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156617975012145_zh-CN.png)

3.  单击**Agree and Setup Magento**开始配置Magento。具体步骤如下：

    1.  准备性检查。

        1.  单击**Start Readiness Check**。
        2.  检查完成后，单击**Next**。
        ![magento-check](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156617975044785_zh-CN.png)

    2.  添加数据库。

        1.  输入之前创建的数据库用户的账号和密码。本教程中创建的示例用户账号为`magentoUser`、密码为`magentoUser1@3`。
        2.  输入之前创建的数据库的名字。本教程中创建的示例数据库名字为`magento`。
        3.  单击**Next**。
        ![config-db](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156617975044786_zh-CN.png)

    3.  填写Web访问设置后，单击**Next**。

        ![config-web](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156617975144787_zh-CN.png)

    4.  填写定制商店后，单击**Next**。
    5.  填写管理员账号信息后，单击**Next**。
    6.  单击**Install Now**进行安装。
    出现如下图所示的界面时，说明Magento配置完成。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156617975112146_zh-CN.png)


## 步骤八：添加cron作业 {#section_kcl_jnt_ax9 .section}

1.  运行crontab -u apache -e设置cron运行调度工作。
2.  按下`i`键进入编辑模式。
3.  输入下列配置信息。

    ``` {#codeblock_oi5_uzo_pju}
    */10 * * * * php -c /etc /var/www/html/bin/magento cron:run
    */10 * * * * php -c /etc /var/www/html/update/cron.php
    */10 * * * * php -c /etc /var/www/html/bin/magento setup:cron:run
    ```

4.  按下`Esc`键后，输入`:wq`并回车以保存并退出。

Magento上使用cron作业的更多信息，请参见[Magento官方文档](http://devdocs.magento.com/guides/v2.0/config-guide/cli/config-cli-subcommands-cron.html)。

## 后续操作 {#section_jh3_l5l_2fb .section}

访问`http://[ECS实例公网IP]`可以看到如下图所示的默认主页。

![luma](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156617975112147_zh-CN.png)

访问`http://[ECS实例公网IP]/admin`，输入您在安装过程中设置的用户名和密码，成功登录管理面板后可看到如下界面。

![dashboard](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9769/156617975112148_zh-CN.png)

更多Magento配置信息，请参见[Magento官方文档](http://devdocs.magento.com/guides/v2.1/)。

