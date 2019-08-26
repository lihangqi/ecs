# Drupal建站教程（CentOS7） {#concept_lqz_2p1_ffb .concept}

Drupal是使用PHP语言编写的开源内容管理框架（CMF），它由内容管理系统（CMS）和PHP开发框架（Framework）共同构成。它用于构造提供多种功能和服务的动态网站，能支持从个人博客到大型社区等各种不同应用的网站项目。

本文主要说明如何在阿里云ECS上搭建Drupal电子商务网站。

## 适用对象 {#section_hh5_jp1_ffb .section}

适用于熟悉ECS，熟悉Linux系统，刚开始使用阿里云进行建站的用户。

## 基本流程 {#section_bmv_kp1_ffb .section}

使用云服务器 ECS 搭建 Drupal 网站的操作步骤如下：

1.  选购ECS实例。
2.  构建Web运行环境。
3.  安装Drupal。

**步骤 1：选购ECS实例**

对于个人使用的小型网站，选购一台云服务器ECS实例可以满足需求，后续您可以根据实际使用情况考虑配置升级或者架构调优变更。

**步骤2：构建web环境**

在阿里云服务器上构建Web运行环境有3种方式：

-   镜像部署
-   一键安装包部署
-   手动部署（源码编译安装/YUM安装）

一般推荐镜像部署，适合新手使用，更加快捷方便，一键安装包部署以及手动部署适合对运维知识有基本了解的用户，可以满足用户个性化部署的要求。本文档基于镜像部署的方式，搭建 Drupal 网站。

即在 [创建ECS实例](https://ecs.console.aliyun.com/#/create/prepay) 时，镜像栏指定镜像市场。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/154408862512506_zh-CN.png)

单击 **从镜像市场选择**，搜索框输入LAMP进行筛选，本文选择了匹配到的第一个镜像。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/154408862512507_zh-CN.png)

单击 **购买** 后，选择 **LAMP7.0.12\_CentOS7.2** 版本。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/154408862512508_zh-CN.png)

更多镜像环境用户可在 [云市场基础环境](https://market.aliyun.com/software?spm=5176.8060583.401001.1.ReWWeQ) 中搜索筛选。

本文环境软件明细：`CentOS 7.2 | Apache 2.4.25 | MySQL 5.7.17 | PHP 7.1.1 |Drupal8.1.1`

**说明：** 这是写文档时使用的软件版本，您下载的版本可能与此不同。

**步骤 3：安装 Drupal**

1.  下载Drupal安装包。

    ```
    # wget http://ftp.drupal.org/files/projects/drupal-8.1.1.zip
    ```

2.  解压到网站根目录。

    ```
    # unzip drupal-8.1.1.zip 
    # mv drupal-8.1.1/* /var/www/html/
    ```

3.  下载中文翻译包。

    ```
    # cd /var/www/html/
    # wget -P profiles/standard/translations http://ftp.drupal.org/files/translations/8.x/drupal/drupal-8.26.zh-hans.po
    ```

4.  修改sites目录属主属组。

    ```
    # chown -R apache:apache /var/www/html/sites
    ```

5.  重启Apache服务。

    ```
    # /etc/init.d/httpd restart
    ```

6.  浏览器访问ECS服务器的公网IP/index.php ，进入到Drupal安装界面。选择安装语言，单击Save and continue。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/154408862512509_zh-CN.png)

7.  选择标准安装方式，单击 **保存并继续**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/154408862512510_zh-CN.png)

8.  填写数据库信息，单击 **保存并继续**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/154408862512511_zh-CN.png)

    **说明：** 用户登录mysql数据库后，可使用以下命令自定义用户名密码：

    -   DBNAME：数据库名称
    -   UAERNAME：数据库用户
    -   IP：本机可直接填localhost或者127.0.0.1
    -   YOURPASSWORD：数据库密码
    ```
    mysql> CREATE DATABASE DBNAME；
    mysql> CREATE USER UAERNAME；
    mysql> GRANT ALL PRIVILEGES ON *.* TO 'UAERNAME'@'IP' IDENTIFIED BY 'YOURPASSWORD' WITH GRANT OPTION;  
    mysql> FLUSH PRIVILEGES;
    ```

9.  自动安装完成后进入网站设置界面，填写站点信息，单击 **保存并继续**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/154408862512512_zh-CN.png)

10. 安装完成，后续可以根据需要对网站进行个性化设置。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9771/154408862612513_zh-CN.png)


