# Drupal建站教程（CentOS7） {#concept_lqz_2p1_ffb .task}

本文介绍如何在阿里云ECS上搭建Drupal电子商务网站。

使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。

Drupal是使用PHP语言编写的开源内容管理框架（CMF），它由内容管理系统（CMS）和PHP开发框架（Framework）共同构成。它用于构造提供多种功能和服务的动态网站，能支持从个人博客到大型社区等各种不同应用的网站项目。

本教程适用于熟悉ECS，熟悉Linux系统，刚开始使用阿里云进行建站的用户。

## 操作步骤 {#section_z74_yzt_kll .section}

使用云服务器ECS搭建Drupal网站的操作步骤如下：

1.  [步骤一：选购ECS实例](#section_i87_j52_9zo)
2.  [步骤二：构建Web环境](#section_y3l_5ds_jz7)
3.  [步骤三：安装Drupal](#section_mdj_fvs_xov)

## 步骤一：选购ECS实例 {#section_i87_j52_9zo .section}

对于个人使用的小型网站，选购一台云服务器ECS实例可以满足需求，后续您可以根据实际使用情况考虑配置升级或者架构调优变更。

## 步骤二：构建Web环境 {#section_y3l_5ds_jz7 .section}

在阿里云服务器上构建Web运行环境有以下三种方式：

-   镜像部署
-   一键安装包部署
-   手动部署（源码编译安装/YUM安装）

一般推荐镜像部署，适合新手使用，更加快捷方便。一键安装包部署以及手动部署适合对运维知识有基本了解的用户，可以满足用户个性化部署的要求。本文介绍基于镜像部署的方式，搭建Drupal网站。

1.  在创建ECS实例时，在镜像区域，选择**镜像市场** \> **从镜像市场选择（含操作系统）**。其他配置请参见[创建ECS实例](https://ecs.console.aliyun.com/#/create/prepay)。
2.  在搜索框中输入**LAMP**进行筛选，本文选择了匹配到的第一个镜像。 

    ![搜索镜像](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/156531809812507_zh-CN.png)

3.  单击**购买**后，选择**LAMP7.0.12\_CentOS7.2**版本。 

    ![选择镜像版本](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/156531809812508_zh-CN.png)

    更多镜像环境用户可在 [云市场基础环境](https://market.aliyun.com/software?spm=5176.8060583.401001.1.ReWWeQ)中搜索筛选。

    本文环境软件明细：`CentOS 7.2 | Apache 2.4.25 | MySQL 5.7.17 | PHP 7.1.1 |Drupal8.1.1` 

    **说明：** 这是写文档时使用的软件版本，您下载的版本可能与此不同。


## 步骤三：安装Drupal {#section_mdj_fvs_xov .section}

完成以下操作，安装Drupal：

1.  下载Drupal安装包。 

    ``` {#codeblock_eym_wte_4tz}
    # wget http://ftp.drupal.org/files/projects/drupal-8.1.1.zip
    ```

2.  解压到网站根目录。 

    ``` {#codeblock_dnw_tfi_yye}
    # unzip drupal-8.1.1.zip 
    # mv drupal-8.1.1/* /var/www/html/
    ```

3.  下载中文翻译包。 

    ``` {#codeblock_jb5_uss_5zb}
    # cd /var/www/html/
    # wget -P profiles/standard/translations http://ftp.drupal.org/files/translations/8.x/drupal/drupal-8.26.zh-hans.po
    ```

4.  修改sites目录属主属组。 

    ``` {#codeblock_dh0_o87_8d4}
    # chown -R apache:apache /var/www/html/sites
    ```

5.  重启Apache服务。 

    ``` {#codeblock_cdb_vp2_n0e}
    # /etc/init.d/httpd restart
    ```

6.  浏览器访问ECS服务器的公网IP/index.php ，进入到Drupal安装界面。选择安装语言，单击**Save and continue**。 

    ![选择安装语言](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/156531809812509_zh-CN.png)

7.  选择标准安装方式，单击**保存并继续**。 

    ![选择安装方式](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/156531809912510_zh-CN.png)

8.  填写数据库信息，单击**保存并继续**。 

    ![设置数据库](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/156531809912511_zh-CN.png)

    **说明：** 用户登录mysql数据库后，可使用以下命令自定义用户名密码：

    -   DBNAME：数据库名称
    -   UAERNAME：数据库用户
    -   IP：本机可直接填localhost或者127.0.0.1
    -   YOURPASSWORD：数据库密码
    ``` {#codeblock_mdp_tpg_qaz}
    mysql> CREATE DATABASE DBNAME；
    mysql> CREATE USER UAERNAME；
    mysql> GRANT ALL PRIVILEGES ON *.* TO 'UAERNAME'@'IP' IDENTIFIED BY 'YOURPASSWORD' WITH GRANT OPTION;  
    mysql> FLUSH PRIVILEGES;
    ```

9.  自动安装完成后进入网站设置界面，填写站点信息，单击**保存并继续**。 

    ![设置站点信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/156531809912512_zh-CN.png)


安装完成，后续可以根据需要对网站进行个性化设置。

![后续操作](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/156531810012513_zh-CN.png)

