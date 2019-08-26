# 搭建Joomla基础管理平台 {#concept_an2_t25_2fb .concept}

Joomla是一套知名的内容管理系统。Joomla是使用PHP语言加上Mysql数据开发的软件系统，Joomla的最新版本是3.x，这一版本实现了许多技术上的优化调整，是目前的稳定版本。

本文主要说明如何在阿里云ECS上搭建Joomla基础管理平台。使用的操作系统为Linux CentOS 6.5 64位。

## 适用对象 {#section_ftm_bg5_2fb .section}

适用于熟悉 ECS，熟悉 Linux 系统， ECS 实例搭建刚开始使用阿里云进行建站的用户。

## 基本流程 {#section_gtq_cg5_2fb .section}

使用云服务器 ECS 搭建 Joomla 平台的操作步骤如下：

购买 ECS 实例，如果需要备案网站，请选择包年包月付费模式。对于个人使用的小型网站，一台云服务器 ECS 实例可以满足需求。

这里只介绍新购实例。如果您有镜像，可以使用自定义镜像创建实例。

**说明：** 这个文档中描述的实例将结合 云市场 的 joomla 镜像 使用，而这个产品目前仅支持 CentOS、Ubuntu 和 Aliyun Linux。

**操作步骤**

1.  登录 [云服务器管理控制台](https://account.aliyun.com/login/login.htm?oauth_callback=https%3A%2F%2Fecs.console.aliyun.com%2F#/home)。如果尚未注册，单击 **免费注册**。
2.  选择 **云服务器ECS** \> **实例**。单击 **创建实例**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813612404_zh-CN.png)

3.  选择付费方式：包年包月或按量付费。因为目前只有包年包月的 ECS 可以备案，如果您需要备案网站，请选择 **包年包月**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813612405_zh-CN.png)

4.  选择地域。所谓地域，是指实例所在的地理位置。您可以根据所在的地理位置选择地域。地域与用户距离越近，延迟相对越少，下载速度相对越快。

    例如，如果您的网站访问者都分布在北京地区，则可以选择 华北 2。

    **说明：** 

    -   实例创建完成后，不支持更换地域。
    -   不同地域提供的可用区数量、实例系列、存储类型、实例价格等也会有所差异。请根据您的业务需求进行选择。
5.  选择网络类型。对于建站的用户，选择 **经典网络** 即可。然后选择安全组。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813612406_zh-CN.png)

6.  选择实例，根据您网站的访问量选择实例规格（CPU、内存）。对于个人网站，1 核 2GB 或 2 核 4GB 一般能够满足需求。关于实例规格的详细介绍，请参考实例规格族。实例系列 II 是实例系列 I 的升级版，提供更高的性能，推荐使用。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813612407_zh-CN.png)

7.  选择网络带宽。因为创建的实例需要访问公网，如果选择 0 Mbps，则不分配公网 IP，实例将无法访问公网，所以，无论是 按固定带宽 还是 按使用流量 付费，带宽都不能选择 0 Mbps。
    -   按固定带宽付费。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813612408_zh-CN.png)

    -   按使用流量付费。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813612409_zh-CN.png)

8.  选择镜像。您可以在镜像里面点击镜像市场，再点击从镜像市场选择，搜索 [Joomla!建站系统](https://market.aliyun.com/products/53616009/jxsc000035.html?spm=5176.730005.0.0.AoD4Vi)，然后点击使用就可以使用镜像。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712410_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712411_zh-CN.png)

9.  选择 **系统盘** 和 **数据盘**。您可以创建全新的磁盘作为数据盘，也可以选择 **用快照创建磁盘**，将快照的数据直接复制到磁盘中作为数据盘。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712412_zh-CN.png)

10. 设置实例的登录密码和实例名称。请务必牢记密码。您也可以在创建完成后再设置密码。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712413_zh-CN.png)

11. 设置购买的时长和数量。
12. 单击页面右侧价格下面的 **立即购买**。
13. 确认订单并付款。

实例创建好之后，您会收到短信和邮件通知，告知您的实例名称、公网 IP 地址、内网 IP 地址等信息。您可以使用这些信息登录和管理实例。

很多重要的信息都是通过绑定手机的短信接收，并且重要的操作（如重启、停止等）都需要手机接收验证码，因此请务必保持绑定手机通信畅通。

## 部署 Web 环境 {#section_nwl_cd1_ffb .section}

通过 ECS 更换系统盘，来更换所需要的镜像，这里选择 php 运行环境（centos 64 位 | php5.4|nginx1.4|joomla）。

-   镜像版本说明操作系统：centos 6.5 64 位。

    镜像版本 V1.0 软件明细：Nginx1.4.7-PHP 5.4.27-MySQL5.5.37-FTP2.2.2- Joomla!3.3.3 1.2、镜像安装说明。

-   镜像环境里相应软件的安装，是基于阿里云 linux 版的一键安装包源码 1.3.0 版本，在此基础上修改、优化了相应功能，编译安装完成。
-   在镜像环境中，/root/sh-1.3.0-centos-joomla.zip 是安装镜像环境的脚本。您可以在 centos 6.5 系统中自行采用此脚本安装，安装后的环境跟镜像里初始化的环境一致。

    **说明：** 如果采用此脚本安装镜像环境，需要 chmod 777 -R sh-1.3.0-centos-joomla 赋予 777 安装权限。

-   在镜像环境中出于安全考虑，joomla 默认设置页面只容许 127.0.0.1 访问，/root/目录下提供一个 joomla\_opennet.sh 的脚本 。用户运行此脚本后，可以通过外网访问 joomla 的默认设置页面。
-   在镜像环境中，/root/sh-1.3.0-centos-joomla 是安装环境的主目录，镜像中的环境是在此目录下编译安装的。

## mysql 以及 ftp 的密码 {#section_bqx_pd1_ffb .section}

1.  密码存储位置： /alidata/account.log 文件中。
2.  查看密码.

    ```
    进入服务器的系统中，可以在任意的目录下，执行以下命令
    cat /alidata/account.log
    ```

    **说明：** cat 后有空格。

3.  修改 ftp 的密码。

    用 root 用户登录系统，然后执行下面命令。

    ```
    passwd www 然后输入您的 ftp 新密码。
    ```

4.  修改 mysql 的密码。

    ```
    mysqladmin -uroot -p 旧密码 password 新密码
    ```

    **说明：** -p 和旧密码之间没有空格，password 和新密码之间有空格。


## 软件目录及配置列表 {#section_j3c_yd1_ffb .section}

软件的主目录：/alidata

web 主目录：/alidata/www

ftp 主目录：/alidata/www

nginx 主目录：/alidata/server/nginx

nginx 配置文件主目录：/alidata/server/nginx/conf

php 主目录：/alidata/ server/php

php 配置文件主目录：/alidata/ server/php/etc

mysql 主目录：/alidata/server/mysql

mysql 配置文件：/etc/my.cnf

joomla 中文支持包存放目录：/alidata/res

日志目录：

/alidata/log/nginx 为 nginx 存放日志主目录

/alidata/log/php 为 php 存放日志主目录

/alidata/log/mysql 为 mysql 存放日志主目录 init 目录

/alidata/init 为当用户用镜像创建系统后，当且仅当用户在第一次启动系统的时候，调用此目录下的脚本来初始化 ftp 及 mysql 的密码（随机密码）。

## 软件操作命令汇总 {#section_zkn_j21_ffb .section}

/etc/init.d/mysqld start|stop|restart

/etc/init.d/php-fpm start|stop|restart

/etc/init.d/vsftpd start|stop|restart

/etc/init.d/nginx start|stop|restart

## 关于卸载 {#section_bn4_k21_ffb .section}

关于卸载镜像环境中安装的软件，可以参考如下命令。

```
cd /root/sh-1.3.0-centos-joomla
./uninstall.sh
```

**说明：** 

-   执行以上操作会清理环境的 /alidata 目录，请卸载前自行备份好相应数据。
-   如果不小心删除了 /root/sh-1.3.0-centos-joomla,可以解压缩 /root/sh-1.3.0-centos-joomla.zip 参考以下命令。

    ```
    cd
    unzip sh-1.3.0-centos-joomla.zip
    chmod 777 -R sh-1.3.0-centos-joomla
    cd sh-1.3.0-centos-joomla
    ./uninstall
    ```


## 在 centos6.5 系统中自行安装 {#section_g5y_421_ffb .section}

/root/sh-1.3.0-centos-joomla.zip 是安装镜像环境的脚本。值得注意的是，如果采用此脚本安装镜像环境，需要 chmod 777 -R sh-1.3.0-centos-joomla 赋予 777 安装权限,然后cd sh-1.3.0-centos-joomla目录下执行 ./install 开始安装。

根据提示输入 y。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712414_zh-CN.png)

持续安装中。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712415_zh-CN.png)

安装结束出现以下界面。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712416_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712417_zh-CN.png)

80、21、9000、3306 等端口都已开启。

## **配置外网访问** {#section_n55_t21_ffb .section}

在镜像环境中处于安全考虑，joomla 默认页面只允许 127.0.0.1 访问，/root/ 目录下提供了一个 joomla\_opennet.sh 的脚本。用户运行之后，可通过外网访问 joomla 的默认设置页面。

运行脚本文件。

```
/root/joomla_opennet.sh
```

## 配置joomla {#section_ajm_w21_ffb .section}

初次使用镜像，运行 /root/joomla\_opennet.sh 文件，在游览器中输入 http://ip，回车即可看到 joomla 的初始化界面。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712418_zh-CN.png)

选择语言，并填写相关内容，单击 **下一步**。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712419_zh-CN.png)

选择mysql数据库，填写相关权限后，单击 **下一步**。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712420_zh-CN.png)

查看相关配置是否符合，确认完毕单击 **安装**。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712421_zh-CN.png)

## 安装完毕 {#section_zbz_3f1_ffb .section}

进入服务器 /alidata/www/default 目录下删除 installation 目录。

```
cd /alidata/www/default
rm -rf installation/
```

至此，joomla 搭建完成。

访问前端网站 http://ip，访问后台管理 http://ip/administrator。

关于 Joomla 支持中文。

Joomla 安装完成之后默认前台后台都是英文界面，中文语言需要手动安装。登陆 Joomla 之后在 **Extensions（扩展）** \> **Extension Manager（扩展管理）** 打开扩展配置页面后，上传简体中文包，中文包在服务器的/alidata/res目中，将中文包下载到本地后上传。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712422_zh-CN.png)

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813712423_zh-CN.png)

单击 **Update & Install** 上传。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813812424_zh-CN.png)

在 **Extensions（扩展）** \> **Language Manager（语言管理）** 中，设置前端后台的默认语言，设置完后并单击右上角 **Logout** 重新登陆。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813912425_zh-CN.png)

登陆后就能进入中文界面了。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9784/154045813912426_zh-CN.png)

