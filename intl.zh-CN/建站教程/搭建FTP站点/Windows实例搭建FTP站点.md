# Windows实例搭建FTP站点 {#concept_kmr_213_ffb .concept}

本文介绍了如何使用 Windows 实例搭建 FTP 站点。此方法适用于 Windows Server 2008 及以上系统，本文以 Windows Server 2008 R2 为例。

Windows 实例搭建 FTP 站点具体操作步骤如下：

-   [步骤一： 添加 IIS 以及 FTP 服务角色](#)
-   [步骤二： 创建 FTP 用户名及密码](#)
-   [步骤三： 设置共享文件的权限](#)
-   [步骤四： 添加及设置 FTP 站点](#)
-   [步骤五： 设置安全组及防火墙](#)
-   [步骤六： 客户端测试](#)

## 步骤一： 添加 IIS 以及 FTP 服务角色 {#section_dgv_q13_ffb .section}

在创建 FTP 站点前，首先需要安装 IIS 及 FTP 服务。

1.  [远程连接](../../../../intl.zh-CN/用户指南/连接实例/使用软件连接Windows实例.md#) 并登录到 Windows 实例。
2.  选择 **开始** \> **所有程序** \> **管理工具** \> **服务管理器**。
3.  单击 **角色**，然后单击 **添加角色**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850112581_zh-CN.png)

4.  在弹出的对话框中，选择 **下一步**。
5.  选择 **Web 服务器（IIS）**，然后单击 **下一步**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850112582_zh-CN.png)

6.  选择 **IIS管理控制台** 以及 **FTP 服务器**，选择 **下一步**，单击 **安装**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850112583_zh-CN.png)


## 步骤二： 创建 FTP 用户名及密码 {#section_g5d_z13_ffb .section}

创建 Windows 用户名和密码，用于 FTP 使用。如果您希望匿名用户可以访问，此步可省略。

1.  选择 **开始** \> **管理工具** \> **服务器管理器**。
2.  单击 **配置** \> **本地用户和组** \> **用户**，并在右侧空白处单击右键，再选择 **添加用户**，本文例子中 **用户名** 使用 ftptest。

    **说明：** 密码必须包括大写字母、小写字母和数字。否则会显示无法通过密码策略。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850112584_zh-CN.png)


## 步骤三： 设置共享文件的权限 {#section_mvf_kc3_ffb .section}

您需要为在 FTP 站点共享给用户的文件夹设置访问以及修改等权限。

1.  在服务器磁盘上创建一个供 FTP 使用的文件夹，右键单击文件夹，选择 **属性**。
2.  单击 **安全**，选择 **Everyone**，然后选择 **编辑**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850112585_zh-CN.png)

3.  选择 **Everyone**，然后根据需要，选择 **Everyone** 的权限，本文例子中允许所有权限。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850112586_zh-CN.png)


## 步骤四： 添加及设置 FTP 站点 {#section_xf1_pc3_ffb .section}

安装 FTP，设置好共享文件夹权限后，您需要创建 FTP 站点。

1.  选择 **开始** \> **所有程序** \> **管理工具** \> **Internet 信息服务（IIS）管理器**。
2.  右键单击 **网站**，选择 **添加 FTP 站点**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850112587_zh-CN.png)

3.  在弹出的窗口，填写 FTP 站点名称与共享文件夹的物理路径，然后单击 **下一步**。
4.  IP 地址默认选择 **全部未分配**。端口号可自行设置，FTP 默认端口号为 21。
5.  选择 SSL 设置。

    -   **允许**：允许 FTP 服务器支持与客户端的非 SSL 和 SSL 连接。
    -   **需要**：需要对 FTP 服务器和客户端之间的通信进行 SSL 加密。
    -   **无**： 不需要 SSL 加密选择 **无**。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850212588_zh-CN.png)

6.  选择要使用的一种或多种身份验证方法。
    -   **匿名**：允许任何仅提供用户名 **anonymous** 或 **ftp** 的用户访问内容。
    -   **基本**：需要用户提供有效用户名和密码才能访问内容。由于基本身份验证通过网络传输未加密的密码，因此请仅在清楚客户端和 FTP 服务器之间的连接是安全的情况下（例如，使用安全套接字层 \(SSL\) 时）使用此身份验证方法。
7.  从 **允许访问** 列表中，选择以下选项之一：
    -   **所有用户**：所有用户（不论是匿名用户还是已标识的用户）均可访问相应内容。
    -   **匿名用户**：匿名用户可访问相应内容。
    -   **指定角色或用户组**：仅特定角色或用户组的成员才能访问相应内容。请在对应的框中键入角色或用户组。
    -   **指定用户**：仅指定用户才能访问相应内容。请在对应的框中键入用户名。
8.  选择经过授权的用户的 **读取** 和 **写入** 权限。然后单击 **完成**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850212589_zh-CN.png)


完成后可以看到搭建的 FTP 站点。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850212590_zh-CN.png)

## 步骤五： 设置安全组及防火墙 {#section_jk1_3d3_ffb .section}

搭建好 FTP 站点后，您需要在实例安全组的入方向添加一条放行 FTP 端口的规则，具体步骤参见 [添加安全组规则](../../../../intl.zh-CN/用户指南/安全组/添加安全组规则.md#)，具体配置可以参见 [安全组规则的典型应用](../../../../intl.zh-CN/用户指南/安全组/安全组规则的典型应用.md#)。

服务器防火墙默认放行 TCP 21 端口用于 FTP 服务。如果选用其他端口，您需要在防火墙中添加一条放行此端口的入站规则。

其他防火墙设置参见 [微软官方文档](https://technet.microsoft.com/zh-cn/library/hh831655(v=ws.11).aspx#Step4)。

## 步骤六： 客户端测试 {#qaz .section}

打开客户端的 **计算机**，在路径栏输入 `ftp://服务器 IP 地址:FTP 端口`（如果不填端口则默认访问21端口），例如：`ftp://0.0.0.0:20`。弹出输入用户名和密码的对话框表示配置成功，正确的输入用户名和密码后，即可对 FTP 文件进行相应权限的操作。

**说明：** 客户端使用此方法访问 FTP 站点时，需要对 IE 浏览器进行设置，才能打开 FTP 的文件夹。 打开 IE 浏览器，选择 **设置** \> **Internet选项** \> **高级**。勾选 **启用 FTP 文件夹视图**，取消勾选 **使用被动 FTP**。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/154044850212591_zh-CN.png)

## 后续操作 {#section_cdm_rd3_ffb .section}

您可以参考 [安全加固方案](https://www.alibabacloud.com/help/zh/doc-detail/37452.htm) 对 FTP 服务进行安全加固。

如果您想基于 FTP 协议来管理存储在 OSS 上的文件，安装 [OSS FTP](../../../../intl.zh-CN/常用工具/ossftp/如何快速安装OSS FTP.md#)。OSS FTP 接收普通 FTP 请求后，将对文件、文件夹的操作映射为对 OSS 的操作。

