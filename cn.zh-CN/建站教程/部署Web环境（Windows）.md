# 部署Web环境（Windows） {#concept_dt2_ghm_2fb .concept}

本节介绍如何使用阿里云镜像，一键部署 Web 环境，包括安装 IIS 组件（不包括 FTP 组件）、PHP 环境、重定向 Rewrite、MySQL、phpwind。该示例不需要更换系统盘。

创建实例以及配置安全组时：

-   请务必选择至少2GB或更高内存的实例规格，1 核 1GB 的实例规格无法启动 Mysql。
-   请务必完成安全组的详细配置，开通端口21（FTP服务），端口3389，端口80。

## 操作步骤 {#section_imp_jss_2fb .section}

1.  在浏览器中打开阿里云的[云市场](http://market.aliyun.com/)。
2.  搜索**阿里云windows一键安装web环境**，然后购买该软件。
3.  登录[阿里云管理控制台](http://console.aliyun.com/)。选择**产品与服务** \> **云市场**。
4.  单击**已购买的服务**。在**阿里云Windows一键安装Web环境**的右侧，单击**下载**，一键下载安装包。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9773/155064056839009_zh-CN.png)

5.  解压缩安装包。通过远程连接，将解压后的安装包拷贝到云服务器 ECS 实例上。

    **说明：** 远程连接时，建议不要在控制台中完成。为了方便直接将软件进行本地机与远程机的复制粘贴，请参考[连接Windows实例](https://help.aliyun.com/document_detail/25435.html?spm=5176.doc25425.6.603.4xAo0R)进行操作。

6.  安装包启动后，单击**下一步**。
7.  指定安装目录，默认使用**C:\\websoft** 。然后单击**安装**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9773/155064056912197_zh-CN.png)

8.  系统会依次自动安装 IIS 组件（不包括 FTP 组件）、PHP 环境、重定向 Rewrite、MySQL、phpwind。

    **说明：** 在安装过程中，每完成一项，需要您手动**按任意键继续**，如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9773/155064056912203_zh-CN.png)

9.  安装 MySQL 时，会报错**服务名无效**（因之前未安装过MySQL），请直接忽略。
10. 将安装目录下的 account.log 中的 MySQL 密码复制粘贴到相应的数据库密码项中，并填写数据库名称、phpwind 管理员的登录密码，然后单击**创建数据**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9773/155064056912248_zh-CN.png)

11. phpwind 安装程序自动在 MySQL 中创建库和数据表。完成后直接进入 phpwind 登录页。phpwind 安装完毕。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9773/155064056912249_zh-CN.png)

12. 开始安装 FTP 服务。
13. 创建 FTP 用户，并将 FTP 站点的路径设置到 phpwind 的根目录，按任意键继续。
14. 安装 phpMyAdmin 。默认访问端口号为 8080，并在 IIS 中创建站点和连接池。
15. 完成后按任意键启动浏览器，打开 phpMyAdmin 站点，输入安装目录下的 account.log 文件中的 MySQL 账号信息进行登录。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9773/155064056912250_zh-CN.png)

    登录后即可看到所有 MySQL 中的数据库，包括之前命名的 phpwind 数据库。如下图所示。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9773/155064056912251_zh-CN.png)

16. 安装全部完毕。按任意键关闭窗口。
17. 安装完成后，您可以打开 IIS，查看所有部署的服务和站点内容。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9773/155064056912252_zh-CN.png)


您已经成功部署了 Web 环境，可以制作和发布站点了。

