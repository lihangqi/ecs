# 快速搭建 phpwind 论坛系统 {#concept_53855_zh .concept}

phpwind 是采用 PHP + MySQL 方式运行的开源社区程序。轻架构，高效率简易开发，帮助您快速搭建并轻松管理社区站点。phpwind 提供了 2 款完全不同的版本，分别是拥有成熟功能、海量插件支撑的 phpwind 稳定版（v8.7.1）和注重轻社区、高效、易开发的 phpwind 先进版（v9.0.1）。

本文档介绍如何使用云市场的 **PHPWind论坛系统（含智慧云虚机面板）** 快速搭建论坛，包括：

-   安装并使用 phpwind 先进版
-   安装并使用 phpwind 稳定版
-   获取商业授权

## 适用对象 {#section_w3q_kzl_2fb .section}

适用于要搭建论坛的经典网络用户。

## 安装并使用 phpwind 先进版 {#section_wgv_pzl_2fb .section}

**前提条件**

您应该已经拥有已经备案的域名。如果没有备案，购买ECS 实例后，您应到阿里云备案中心备案，备案地址为：[https://beian.aliyun.com。](https://beian.aliyun.com./)

**操作步骤**

安装并使用 phpwind 先进版包括以下几个步骤：

1.  购买安装了PHPWind论坛系统（含智慧云虚机面板）镜像的 ECS 实例。
2.  登录 phpwind 论坛。
3.  绑定域名。

**安装 PHPWind论坛系统（含智慧云虚机面板） 镜像**

1.  单击 [PHPWind论坛系统（含智慧云虚机面板）](https://market.aliyun.com/products/53616009/cmjj017608.html) 进入镜像详情页。
2.  单击 **立即购买**，按提示步骤购买 ECS 实例，其中，**网络类型** 选择 **经典网络**。

**登录 phpwind 论坛**

1.  登录 [ECS 管理控制台](https://ecs.console.aliyun.com/#/home)。
2.  在左边导航栏里，单击 **实例**，进入 ECS 实例列表页。
3.  选择所购 ECS 实例所在的地域，并找到所购 ECS 实例，在 **IP 地址** 列获取该实例的公网 IP 地址。
4.  在浏览器地址栏中，输入公网 IP 地址。屏幕上会显示提示页面。
5.  在提示页面上，单击 **获取权限** 按钮，下载权限文档 zhcloud-readme.doc。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412205_zh-CN.png)

    权限文档中包含了智慧云虚机面板权限（host\)、FTP 权限（PHPWind ftp\)、 MySQL 数据库权限（PHPWind database）和 phpwind 后台管理权限（PHPWind admin）。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412206_zh-CN.png)

6.  在浏览器地址栏里，输入 `http://实例公网 IP 地址/admin.php`，进入 phpwind 的登录页面。
7.  在 phpwind 登录页面上，输入在权限文档 zhcloud-readme.doc 中获取的 phpwind 后台管理的用户名和密码，再单击 **登录**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412207_zh-CN.png)

    登录 phpwind 后台，您就可以管理 phpwind 论坛了。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412208_zh-CN.png)


**绑定域名**

1.  登录 [智慧云虚机面板](http://zhy.yjcom.com/) 。登录信息参见权限文档 zhcloud-readme.doc：

    -   host url 是指智慧云虚机面板的登录地址；
    -   host account 是指智慧云虚机面板的登录账号；
    -   host password 是指智慧云虚机面板的登录密码。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412209_zh-CN.png)

    登录之后，如图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412210_zh-CN.png)

2.  单击 **域名绑定**，输入您的域名即可绑定。若您想禁止 IP 访问，删除含有 IP 地址的这条记录即可。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412211_zh-CN.png)


## 安装并使用 phpwind 稳定版 {#section_m4s_1xm_2fb .section}

如果您想要安装 phpwind 稳定版（v8.7.1），按下面步骤操作。如果不想要安装 phpwind 稳定版（v8.7.1），可以略过这部分内容。

1.  新增网站
2.  使用 FTP 连接到新建的站点
3.  购买并下载安装phpwind 稳定版（v8.7.1）

**前提条件**

您应已经安装了 FTP 工具。在这里，我们以 FileZilla FTP 为例（下载地址为：[https://www.filezilla.cn/download/client](https://www.filezilla.cn/download/client)）。

您应该已经拥有已经备案的域名。如果没有备案，购买ECS 实例后，您应到阿里云备案中心备案，备案地址为：[https://beian.aliyun.com。](https://beian.aliyun.com./)

**新增网站**

1.  登录 [智慧云虚机面板](http://zhy.yjcom.com/)。
2.  单击 **增加网站** ，进入新增站点的页面。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412212_zh-CN.png)

3.  指定一个 FTP 账号密码，选择站点目录，单击 **下一步**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412213_zh-CN.png)

4.  **启用JSP** 选择 **否**，**启用PHP** 选择 **是**，**PHP版本** 选择 **PHP5.4** 版本。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412214_zh-CN.png)

5.  **类型** 选择 **mysql**，指定数据库 **名称** 及 数据库 **密码**，单击 **下一步**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412215_zh-CN.png)

6.  输入一个 **域名**，单击 **执行创建**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412216_zh-CN.png)


至此，您已经成功创建了一个新的站点。您可以查看新站点 FTP 和数据库的权限：

-   查看 FTP 的权限：进入面板首页，单击 **FTP 账号**，单击 **查看密码**，可以查看到新站点的 FTP 账号和 FTP 密码。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412217_zh-CN.png)

-   查看数据库权限：在 [智慧云虚机面板](http://zhy.yjcom.com/) 的 **数据库** 可以查看到。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412218_zh-CN.png)


**使用 FTP 连接到新建的站点**

1.  启动 FileZilla FTP。
2.  输入 ECS 实例的公网 IP 地址、FTP 账号、FTP 密码，单击 **快速链接**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481412219_zh-CN.png)


## 购买并下载安装 phpwind 稳定版（v8.7.1） {#section_npd_fym_2fb .section}

1.  单击 [phpwind 8.7.1安装包（UTF8）](https://market.aliyun.com/products/53616009/cmjj017608.html) 进入程序下载详情页。确认信息后，单击 **立即购买**。
2.  确认订单后，单击 **确认开通**。
3.  开通成功后，单击 **管理控制台**。
4.  在 已购买的服务 里，找到 phpwind 8.7.1安装包（UTF8），单击 **管理**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512220_zh-CN.png)

5.  在 **应用管理信息** 中，单击下载地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512221_zh-CN.png)

6.  下载并解压安装包。
7.  在 FTP 中，打开 phpwind 8.7.1安装包（UTF8）的 upload 目录，将 upload 目录下的程序上传到站点根目录下。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512222_zh-CN.png)

8.  在浏览器中访问 **新增站点** 里绑定的域名。
9.  在弹出对话框中，单击 **接受**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512223_zh-CN.png)

10. 单击 **下一步**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512224_zh-CN.png)

11. 输入数据库权限，单击 **下一步**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512225_zh-CN.png)

12. 完成安装，进入 phpwind 论坛首页。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512226_zh-CN.png)


**获取商业授权**

如果您的 phpwind 论坛需要商业授权，请按下列步骤操作。获取商业授权后，您可以合理合法地商业使用 phpwind 论坛程序。

如果不需要商业授权，可以省略这部分操作。

1.  单击 [phpwind商业授权（含软件包）](https://market.aliyun.com/products/55586021/cmjz000579.html) ，进入phpwind商业授权详情页。
2.  单击 **立即购买**，按步骤付 1 元购买。
3.  登录 [ECS 管理控制台](https://ecs.console.aliyun.com/#/home)。
4.  进入 **云市场** \> **已购买服务**，找到 phpwind 商业授权，单击 **管理**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512228_zh-CN.png)

5.  在 **应用管理信息** 中，单击管理地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512229_zh-CN.png)

6.  单击 **点击这里下载**，得到验证文件 verify.html，通过 FTP 工具上传至站点根目录，再单击 **立即授权**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512230_zh-CN.png)

7.  输入您的站点域名，单击 **确定**，就完成商业授权了。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512231_zh-CN.png)


## 常见问题 {#section_xyr_d1n_2fb .section}

**301 重定向**

1.  登录 [智慧云虚机面板](http://zhy.yjcom.com/)。
2.  找到 **自定义伪静态** \> **自定义**，写入 301 重定向的 Nginx 规则，单击 **保存**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9786/155408481512232_zh-CN.png)

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


**使用智慧云虚机面板需要对公网开放哪些端口？**

-   确保您 ECS 实例所在的安全组已经对公网开放如下端口：21 端口、80 端口、3306 端口、1777 端口、8081 端口。
-   确保您使用的安全软件没有封掉 1777 端口。

更多开源软件尽在云市场：[https://market.aliyun.com/software](https://market.aliyun.com/software)。

