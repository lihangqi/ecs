# 部署Ghost博客（CentOS 7） {#concept_npp_vh1_ffb .concept}

Ghost是一个免费的开源博客平台，使用JavaScript编写，基于Node.js，旨在简化个人博客和在线出版物的在线发布过程。

此外，将来随着业务的扩展，您可以利用阿里云强大的产品平台，平滑地横向和纵向扩展服务容量，例如：

-   扩展单个 ECS 实例的 CPU 和内存规格，增强服务器的处理能力。
-   增加多台 ECS 实例，并利用负载均衡，在多个实例中进行负载的均衡分配。
-   利用弹性伸缩（Auto Scaling），根据业务量自动增加或减少 ECS 实例的数量。
-   利用对象存储 OSS（Object Storage Service），存储静态网页和海量图片、视频等。

## 适用对象 {#section_ltx_fk1_ffb .section}

本文档介绍如何使用一台基本配置的云服务器 ECS 实例搭建 Ghost。适用于刚开始使用阿里云进行建站的个人用户。

## 基本流程 {#section_esn_hk1_ffb .section}

使用云服务器 ECS 搭建 Ghost 网站的操作步骤如下：

1.  购买 ECS 实例。
2.  部署 Web 环境。
3.  安装 Ghost。
4.  购买域名。
5.  备案域名。
6.  解析。

## 步骤 1：购买 Linux 实例 {#section_ayc_mk1_ffb .section}

对于个人使用的小型网站，一台云服务器ECS实例可以满足需求。

这里只介绍新购实例。如果您有镜像，可以 [使用自定义镜像创建实例](../../../../intl.zh-CN/用户指南/实例/创建实例/使用自定义镜像创建实例.md#) 。

操作步骤

1.  登录 [云服务器管理控制台](https://ecs.console.aliyun.com/#/home)。如果尚未注册，单击 **免费注册**。
2.  选择 **云服务器 ECS** \> **实例**。单击 **创建实例**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169812460_zh-CN.png)

3.  选择付费方式：**包年包月** 或 **按量付费**。关于两种付费方式的区别，请参见 [计费对比](../../../../intl.zh-CN/产品定价/计费对比.md#) 。

    如果选择 **按量付费**，请确保账户余额至少有100元。如无余额，请进入 **充值页面** 充值后再开通。

    **说明：** 对于按量付费的实例，即使停止实例，也会继续收费。如果您不再需要该按量付费的实例，请及时 [释放实例](../../../../intl.zh-CN/用户指南/实例/释放实例.md#) 。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169812461_zh-CN.png)

4.  选择地域。所谓地域，是指实例所在的地理位置。您可以根据您的用户所在的地理位置选择地域。与用户距离越近，延迟相对越少，下载速度相对越快。例如，您的用户都分布在北京地区，则可以选择 **华北2**。

    **说明：** 

    -   实例创建完成后，不支持更换地域。
    -   不同地域提供的可用区数量、实例系列、存储类型、实例价格等也会有所差异。请根据您的业务需求进行选择。
5.  选择网络类型。对于建站的用户，选择 **经典网络** 即可。然后选择安全组。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169812462_zh-CN.png)

6.  选择实例，根据您网站的访问量选择实例规格（CPU、内存）。对于个人网站，1 核 2GB 或 2 核 4GB 一般能够满足需求。关于实例规格的详细介绍，请参考 [实例规格族](../../../../intl.zh-CN/产品简介/实例规格族.md#) 。

    实例系列 II 是实例系列 I 的升级版，提供更高的性能，推荐使用。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169812463_zh-CN.png)

7.  选择网络带宽。如果选择 0 MB，则不分配外网 IP，该实例将无法访问公网。如果您选择了 按使用流量，同时选择 0 MB 固定带宽，则同样不分配外网 IP，而且 不支持 0 MB 带宽升级，因此请谨慎选择。
    -   按固定带宽付费。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169812464_zh-CN.png)

    -   按使用流量付费。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169812466_zh-CN.png)

8.  选择镜像。如果用于建站，可以选择公共镜像中的 Linux 操作系统，如 CentOS。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169812467_zh-CN.png)

9.  选择 **系统盘**。您还可以选择 **用快照创建磁盘**，非常方便地把快照的数据直接复制到磁盘中。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169812469_zh-CN.png)

10. 设置实例的登录密码和实例名称。请务必牢记密码。您也可以在创建完成后再设置密码。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169812470_zh-CN.png)

11. 设置购买的时长和数量。
12. 单击页面右侧价格下面的 **立即购买**。
13. 确认订单并付款。

实例创建好之后，您会收到短信和邮件通知，告知您的实例名称、公网 IP 地址、内网 IP 地址等信息。您可以使用这些信息登录和管理实例。

很多重要的信息都是通过绑定手机的短信接收，并且重要的操作（如重启、停止等）都需要手机接收验证码，因此请务必保持绑定手机通信畅通。

## 步骤 2：部署 Web 环境 {#section_jfd_5l1_ffb .section}

本节介绍如何部署 Web 环境，以安装 Nginx为例：

软件包中包含的软件及版本如下：

-   nginx：1.10.2

**说明：** 这是写文档时参考的软件版本。您下载的版本可能与此不同。

**准备工作**

部署之前，请确保：

-   您的实例可以连接公网。
-   已经安装用于连接 Linux 实例的工具，如 SecureCRT。本文将以这个工具为例介绍操作步骤。

**操作步骤**

1.  确保您安装了连接 Linux 实例的工具，如 SecureCRT。
2.  打开 SecureCRT ，设置登录实例所需的信息。
3.  设置连接名称。
4.  协议选择 **SSH**。
5.  输入主机 IP 地址和用户名。
6.  单击 **确定** 保存。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912471_zh-CN.png)

7.  输入用户名 root 和登录密码。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912472_zh-CN.png)

8.  添加Nginx软件库。

    ```
    [root@localhost ~]#rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
    ```

9.  安装Nginx。

    ```
    [root@localhost ~]#yum -y install nginx
    ```

10. 设置Nginx服务器自动启动。

    ```
    [root@localhost ~]# systemctl enable nginx.service
    ```

11. 启动Nginx并查看Nginx服务状态。

    ```
    [root@localhost ~]#systemctl start nginx.service
    [root@localhost ~]#systemctl status nginx.service
    ```

12. 在浏览器中输入IP地址，可以看到默认的Nginx的网页。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912474_zh-CN.png)


至此，Nginx搭建完成。

## 步骤 3：安装 Ghost {#section_shy_4m1_ffb .section}

请先下载最新版的Ghost，网址： [https://ghost.org/zip/ghost-latest.zip](https://ghost.org/zip/ghost-latest.zip)

**操作步骤**

1.  更新系统。

    确保你的服务器系统处于最新状态。

    ```
    [root@localhost ~]# yum -y update
    ```

2.  安装Node.js。
    1.  安装EPEL。

        ```
        [root@localhost ~]# yum install epel-release -y
        ```

    2.  安装Node.js 和 npm。

        ```
        [root@localhost ~]# yum install nodejs npm --enablerepo=epel
        ```

    3.  安装进程管理器以便控制Node.js应用程序，这个进程管理器可以保持应用程序一直在运行，运行以下命令进行安装。

        ```
        [root@localhost ~]# npm install pm2 -g
        ```

    4.  安装后可以通过 node -v 和 npm -v 命令来检查 Node.js 的版本。
3.  安装Ghost。
    1.  创建Ghost安装目录。

        ```
        [root@localhost ~]# mkdir -p /var/www/ghost
        ```

    2.  进入Ghost安装目录，下载最新的Ghost版本。

        ```
        [root@localhost ~]# cd /var/www/ghost
        [root@localhost ghost]# curl -L https://ghost.org/zip/ghost-latest.zip -o ghost.zip
        ```

    3.  解压Ghost安装包。

        ```
        [root@localhost ghost]# yum install unzip -y
        [root@localhost ghost]# unzip ghost.zip
        ```

    4.  使用npm安装Ghost。

        ```
        [root@localhost ghost]# npm install -production
        ```

    5.  安装完成后用 npm start 命令启动ghost，检查有没有安装成功。
    6.  从示例配置文件复制并新建 Ghost 配置文件 config.js。

        ```
        [root@localhost ghost]# cp config.example.js config.js
        ```

    7.  配置config.js文件中的URL为自己的域名。

        ```
        [root@localhost ghost]# vim config.js
        ```

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912477_zh-CN.png)

    8.  使用进程管理器来配置Ghost永久运行。

        ```
        [root@localhost ghost]# NODE_ENV=production pm2 start index.js --name "ghost"
        ```

    9.  开启/停止/重启ghost。

        ```
        [root@localhost ghost]# pm2 start ghost
        [root@localhost ghost]# pm2 stop ghost
        [root@localhost ghost]# pm2 restart ghost
        ```

4.  安装Nginx。
    1.  添加Nginx软件库。

        ```
        [root@localhost ~]# rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
        ```

    2.  安装Nginx。

        ```
        [root@localhost ~]# yum -y install nginx
        ```

    3.  设置Nginx服务器自动启动。

        ```
        [root@localhost ~]# systemctl enable nginx.service
        ```

    4.  启动Nginx并查看Nginx服务状态。

        ```
        [root@localhost ~]#systemctl start nginx.service
        [root@localhost ~]#systemctl status nginx.service
        ```

    5.  在浏览器中输入IP地址，可以看到默认的Nginx的网页。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912478_zh-CN.png)

5.  配置Nginx作为Ghost的反向代理。
    1.  进入Nginx配置目录，新建Ghost博客的Nginx配置文件。

        ```
        [root@localhost ~]#vim /etc/nginx/conf.d/ghost.conf
        ```

    2.  将以下内容输入到ghost.conf中，把 **server\_name** 改成实际的域名。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912479_zh-CN.png)

    3.  修改默认的配置文件default.conf为default.conf.bak，使Nginx只应用ghost.conf。

        ```
        [root@localhost ~]#mv default.conf default.conf.bak
        ```

    4.  重启Nginx服务。

        ```
        [root@localhost conf.d]# systemctl restart nginx.service
        ```

6.  访问Ghost博客。
    1.  在浏览器输入 http://IP 或 http://域名 即可访问Ghost。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912480_zh-CN.png)

        **说明：** 如果访问出现502，请检查是否由于防火墙的问题引起，可以关闭防火墙。

    2.  需要对博客进行编辑修改，在浏览器输入 http://IP/ghost 即可。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912481_zh-CN.png)


## 步骤 4：购买域名 {#section_syf_f41_ffb .section}

您可以给自己的网站设定一个单独的域名。您的用户可以使用易记的域名访问您的网站，而不需要使用复杂的 IP 地址。

建议通过 [阿里云购买域名](https://wanwang.aliyun.com/)。

**操作步骤**

1.  在 [购买域名](https://wanwang.aliyun.com/) 页面，搜索想用的域名，如尚未被注册，则可以购买。选择要购买的域名及期限，然后结算。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912482_zh-CN.png)

2.  在确认订单的时候，需要选择域名的所有者是个人还是企业。为方便操作，建议暂时先选择个人，以后可以在会员中心进行修改。本文档将以个人用户为例。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912483_zh-CN.png)

3.  如果这是您首次购买域名，需要 [创建消息模板](https://domain.console.aliyun.com/#/infotemplate)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912484_zh-CN.png)

4.  比较便捷的方式是选择用会员信息自动填写。请务必填写真实信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912486_zh-CN.png)

5.  完成后需要进行实名认证。上传个人身份证正面扫描件。审核一般需要 3 ~ 5 个工作日。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294169912487_zh-CN.png)


## 步骤 5：备案 {#section_sdf_m41_ffb .section}

对于域名指向中国境内服务器的网站，必须进行网站备案。在域名获得备案号之前，网站是无法开通使用的。

阿里云有代备案系统，方便您进行备案。备案免费，一般审核时间为20天左右。请您耐心等待。

**操作步骤**

1.  首先给购买的ECS实例 [申请备案服务号](https://bsn.console.aliyun.com/#/bsnApply/ecs)。这个服务号在备案时会用到。选择 **备案管理** \> **备案服务号申请**，然后单击 **申请**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294170012488_zh-CN.png)

2.  在弹出的提示信息对话框中，单击 **确定**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294170012489_zh-CN.png)

3.  申请成功后，页面自动跳转到备案服务号管理页面，显示与 ECS 实例绑定的备案号。然后单击 [备案专区](https://beian.aliyun.com/)，了解备案相关信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294170012490_zh-CN.png)

4.  首次备案的用户，需要在 [ICP代备案管理系统](https://beian.gein.cn/account/login.htm) 注册一个备案账号。注意，该账号不是阿里云账号，而是申请备案专用的账号。

    关于首次备案的详细步骤，请参考 [首次备案](../../../../intl.zh-CN/备案流程/首次备案.md#) 。


## 步骤 6：配置域名解析 { .section}

您需要在阿里云万网上配置域名解析之后，用户才能通过域名访问您的网站。

**操作步骤**

1.  登录 [域名管理控制台](https://netcn.console.aliyun.com/core/domain/list)。
2.  在域名列表中找到要解析的域名，然后单击 **解析**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294170012491_zh-CN.png)

3.  单击 **新手引导设置**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294170012492_zh-CN.png)

4.  输入您的 Linux 实例的公网 IP 地址。然后单击 **提交**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294170012493_zh-CN.png)

5.  设置成功，会出现如下信息。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9768/154294170012494_zh-CN.png)


恭喜您！您可以使用域名访问自己的网站了！

