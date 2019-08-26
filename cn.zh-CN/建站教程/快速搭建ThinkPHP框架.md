# 快速搭建ThinkPHP框架 {#concept_52954_zh .concept}

ThinkPHP是一款免费、开源、快速、简单、面向对象的轻量级PHP开发框架，遵循Apache2开源协议发布，是为了敏捷Web应用开发和简化企业应用开发而诞生的。本篇教程介绍如何使用云市场镜像快速搭建ThinkPHP框架。

## 适用对象 {#section_tmj_bxl_2fb .section}

正在学习PHP或者已基于ThinkPHP框架进行研发的开发人员。

## 基本流程 {#section_mch_cxl_2fb .section}

1.  购买ThinkPHP框架镜像。
2.  上传您的程序。
3.  切换PHP脚本适应您的程序。
4.  开启pathinfo。
5.  绑定域名。

 **购买ThinkPHP框架镜像** 

1.  单击[ThinkPHP框架（含智慧云虚机面板）](https://market.aliyun.com/products/53616009/cmjj017339.html)进入镜像详情页。
2.  单击**立即购买**，按提示步骤根据您的实际业务需求购买ECS实例。

3.  登录[ECS管理控制台](https://ecs.console.aliyun.com/#/home)。

4.  在左侧导航栏，单击**实例与镜像** \> **实例**，进入ECS实例列表页。
5.  选择已购ECS实例所在的地域，并找到目标实例，在**IP 地址**列获取该实例的公网IP地址。
6.  在浏览器地址栏中输入公网IP地址，屏幕上会显示提示页面。
7.  在提示页面，单击**获取权限**，下载权限文档zhcloud-readme.doc。

    ![安装thinkPHP框架](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/156617982312159_zh-CN.png)

    权限文档中包含了智慧云虚机面板权限（host）、FTP权限和MySQL数据库权限，请妥善保存。

    ![权限](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/156617982312160_zh-CN.png)


 **上传您的程序** 

如果您已经通过ThinkPHP框架完成了自己的应用程序，可以通过FTP上传您的程序。

1.  下载FTP工具。本篇教程以FileZilla FTP为例。下载地址为[https://www.filezilla.cn/download/client](https://www.filezilla.cn/download/client)。
2.  下载FileZilla后，双击filezilla.exe，开始按软件提示安装FileZilla FTP。
3.  启动FileZilla FTP，在**主机**、**用户名**和**密码**处分别输入FTP IP地址、FTP账号和FTP密码。相关信息，请参见权限文档zhcloud-readme.doc。

    ![启动FileZilla](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/156617982312161_zh-CN.png)

4.  单击**快速连接**，开始连接FTP。
5.  将您已经写好的应用程序拉到右边区域即可实现上传。

 **切换PHP脚本适应您的程序** 

由于PHP的版本不同所支持的PHP函数也不尽相同。若您的程序对PHP版本有严格要求，您可以通过**脚本切换**来切换到您需要的PHP版本。若没有严格要求，可跳过此步骤。

1.  登录[智慧云虚机面板](http://zhy.yjcom.com/) 。登录信息，请参见权限文档zhcloud-readme.doc。

    -   `host url`：**智慧云虚机面板**的登录地址。
    -   `host account`：**智慧云虚机面板**的登录账号。
    -   `host password`：**智慧云虚机面板**的登录密码。
    ![智慧云虚机面板](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/156617982412162_zh-CN.png)

    登录成功后，如下图所示。

    ![登录成功](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/156617982412163_zh-CN.png)

2.  单击**脚本切换** ，选择您需要的PHP版本，单击**确定** 。

    ![选择PHP版本](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/156617982412165_zh-CN.png)


 **开启pathinfo** 

使用ThinkPHP框架写的程序一般会用到pathinfo。若您需要开启pathinfo，请按如下步骤操作。

1.  登录[智慧云虚机面板](http://zhy.yjcom.com/)。
2.  单击**PATH\_INFO** , 选择您的站点，单击**开启**按钮。

    ![开启pathinfo](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/156617982412166_zh-CN.png)


 **绑定域名** 

如果您的实例公网IP地址已经完成了[域名备案](../../../../cn.zh-CN/产品简介/什么是备案.md#)，您可以在智慧云虚机面板上绑定您的域名。

1.  登录[智慧云虚机面板](http://zhy.yjcom.com/)。
2.  单击**域名绑定**，输入您的域名即可绑定。

    若您想禁止IP访问，删除含有IP地址的这条记录即可。

    ![绑定域名](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/156617982412167_zh-CN.png)


## 常见问题 {#section_ugz_lyl_2fb .section}

 **301 重定向** 

1.  登录[智慧云虚机面板](http://zhy.yjcom.com/)。
2.  找到**自定义伪静态** \> **自定义**，写入301重定向的Nginx规则，单击**保存**。

    ![自定义伪静态](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/156617982412168_zh-CN.png)

    下面以域名`yjcom.com`为例写入301重定向Nginx规则。

    -   方法 A：不使用`www.yjcom.com`域名访问网站时都301重定向到`www.yjcom.com`。

        ``` {#codeblock_pgp_x2r_39h}
        if ($host != ‘www.yjcom.com’ ) {
        rewrite ^/(.*)$ http://www.yjcom.com/$1 permanent;
        }
        ```

    -   方法 B：使用`yjcom.com`域名访问网站时才301重定向到`www.yjcom.com`。

        ``` {#codeblock_meq_9ru_off}
        if ($host = ‘yjcom.com’ ) {
        rewrite ^/(.*)$ http://www.yjcom.com/$1 permanent;
        }
        ```

        **说明：** 实际使用时，将以上代码中的域名替换为您自己的域名。


更多开源软件尽在云市场：[https://market.aliyun.com/software](https://market.aliyun.com/software)。

