# 快速搭建 ThinkPHP 框架 {#concept_52954_zh .concept}

ThinkPHP 是一款免费开源的，快速、简单的面向对象的轻量级 PHP 开发框架，遵循 Apache2 开源协议发布，是为了敏捷 Web 应用开发和简化企业应用开发而诞生的。

## 适用对象 {#section_tmj_bxl_2fb .section}

本文档介绍如何使用云市场的 **ThinkPHP 框架（含智慧云虚机面板）** 快速搭建 ThinkPHP 框架。适用于正在学习 PHP 或者已经基于 ThinkPHP 框架研发的开发者。

## 基本流程 {#section_mch_cxl_2fb .section}

1.  购买 ThinkPHP 框架镜像。
2.  上传您的程序。
3.  切换 PHP 脚本适应您的程序。
4.  开启 pathinfo。
5.  绑定域名。

**购买 ThinkPHP 框架镜像**

1.  单击 [ThinkPHP 框架（含智慧云虚机面板）](https://market.aliyun.com/products/53616009/cmjj017339.html) 进入镜像详情页。
2.  单击 **立即购买**，按提示步骤根据您的实际业务需求购买 ECS 实例。

3.  登录 [ECS 管理控制台](https://ecs.console.aliyun.com/#/home)。

4.  在左边导航栏里，单击 **实例**，进入 ECS 实例列表页。
5.  选择所购 ECS 实例所在的地域，并找到所购 ECS 实例，在 **IP 地址** 列获取该实例的公网 IP 地址。
6.  在浏览器地址栏中输入公网 IP 地址。屏幕上会显示提示页面。
7.  在提示页面上单击 **获取权限** 按钮，下载权限文档 zhcloud-readme.doc。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/155408495412159_zh-CN.png)

    权限文档中包含了智慧云虚机面板权限、FTP 权限和 MySQL 数据库权限，请保存好。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/155408495412160_zh-CN.png)


**上传您的程序**

如果您已经用 ThinkPHP 框架写好了自己的应用程序，您可以通过 FTP 上传您的程序。

1.  下载 FTP 工具。我们这里以 FileZilla FTP工具为例。下载地址为：[https://www.filezilla.cn/download/client](https://www.filezilla.cn/download/client)。
2.  下载 FileZilla 后，双击 filezilla.exe，开始按软件提示安装 FileZilla FTP。
3.  启动 FileZilla FTP，在 **主机**、**用户名** 和 **密码** 处分别输入 FTP IP 地址、FTP 账号和 FTP 密码，相关信息详见权限文档 zhcloud-readme.doc。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/155408495412161_zh-CN.png)

4.  单击 **快速连接**，开始连接 FTP。
5.  将您已经写好的应用程序拉到右边区域即可实现上传。

**切换 PHP 脚本适应您的程序**

由于 PHP 的版本不同所支持的 PHP 函数也不尽相同。若您的程序对 PHP 版本有严格的要求，您可以通过 **脚本切换** 来切换到您需要的 PHP 版本。如果没有严格要求，这一步就可以略过。

1.  登录 [智慧云虚机面板](http://zhy.yjcom.com/) 。登录信息参见权限文档 zhcloud-readme.doc：

    -   `host url` 是指 **智慧云虚机面板** 的登录地址；
    -   `host account` 是指 **智慧云虚机面板** 的登录账号；
    -   `host password` 是指 **智慧云虚机面板** 的登录密码。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/155408495412162_zh-CN.png)

    登录之后，如图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/155408495412163_zh-CN.png)

2.  单击 **脚本切换** ，选择您需要的 PHP 版本，单击 **确定** 。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/155408495512165_zh-CN.png)


**开启 pathinfo**

使用 ThinkPHP 框架写的程序一般会用到 pathinfo。若您确实需要开启 pathinfo，请按如下操作。

1.  登录 [智慧云虚机面板](http://zhy.yjcom.com/)。
2.  单击 **PATH\_INFO** , 选择您的站点，单击开启按钮。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/155408495512166_zh-CN.png)


**绑定域名**

如果您的实例公网 IP 地址已经完成了 [域名备案](../../../../../cn.zh-CN/产品简介/什么是备案.md#)，您可以在智慧云虚机面板上绑定您的域名。

1.  登录 [智慧云虚机面板](http://zhy.yjcom.com/)。
2.  单击 **域名绑定**，输入您的域名即可绑定。

    若您想禁止 IP 访问，删除含有 IP 地址的这条记录即可。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/155408495512167_zh-CN.png)


## 常见问题 {#section_ugz_lyl_2fb .section}

**301 重定向**

1.  登录 [智慧云虚机面板](http://zhy.yjcom.com/)。
2.  找到 **自定义伪静态** \> **自定义**，写入 301 重定向的 Nginx 规则，单击 **保存**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9781/155408495512168_zh-CN.png)

    下面以域名 `yjcom.com` 为例写 301 重定向 Nginx 规则。

    -   方法 A：不使用 `www.yjcom.com` 域名访问网站时都 301 重定向到 `www.yjcom.com`。

        ```
        if ($host != ‘www.yjcom.com’ ) {
        rewrite ^/(.*)$ http://www.yjcom.com/$1 permanent;
        }
        ```

    -   方法 B：使用 `yjcom.com` 域名访问网站时才 301 重定向到 `www.yjcom.com`。

        ```
        if ($host = ‘yjcom.com’ ) {
        rewrite ^/(.*)$ http://www.yjcom.com/$1 permanent;
        }
        ```

        **说明：** 实际使用时，将以上代码中的域名替换为您自己的域名。


更多开源软件尽在云市场：[https://market.aliyun.com/software](https://market.aliyun.com/software)。

