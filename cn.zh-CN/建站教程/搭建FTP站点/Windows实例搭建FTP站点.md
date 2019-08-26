# Windows实例搭建FTP站点 {#concept_kmr_213_ffb .task}

本文介绍了如何使用Windows实例搭建FTP站点。此方法适用于Windows Server 2008及以上系统，本文以Windows Server 2008 R2为例。

使用本教程进行操作前，请确保您已经注册了阿里云账号。如还未注册，请先完成[账号注册](https://account.aliyun.com/register/register.htm?)。

## 视频教程 {#section_7om_xoz_i14 .section}

  

## 操作步骤 {#section_z74_yzt_kll .section}

Windows 实例搭建FTP站点的具体操作步骤如下：

1.  [步骤一：添加IIS以及FTP服务角色](#section_qx9_w5k_gvc)
2.  [步骤二：创建FTP用户名及密码](#section_ztx_c4b_edr)
3.  [步骤三：设置共享文件的权限](#section_jd9_tsn_noi)
4.  [步骤四：添加及设置FTP站点](#section_0gy_5s5_oku)
5.  [步骤五：设置安全组及防火墙](#section_ovb_r91_w7d)
6.  [步骤六：客户端测试](#section_xex_vgd_epn)

## 步骤一：添加IIS以及FTP服务角色 {#section_qx9_w5k_gvc .section}

在创建FTP站点前，首先需要安装IIS及FTP服务。

1.  远程连接Windows实例。具体操作，请参见[在本地客户端上连接Windows实例](../cn.zh-CN/实例/连接实例/连接Windows实例/在本地客户端上连接Windows实例.md#)。
2.  单击**开始** \> **所有程序** \> **管理工具** \> **服务器管理器**。
3.  在左侧导航栏，单击**角色**，然后在**角色摘要**区域单击**添加角色**。 

    ![添加角色](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516334612581_zh-CN.png)

4.  在弹出的对话框中，单击**下一步**。
5.  选中**Web 服务器（IIS）**，然后单击**下一步**。 

    ![角色服务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516334612582_zh-CN.png)

6.  选中**IIS管理控制台**以及**FTP 服务器**，单击**下一步**。 

    ![角色服务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516334612583_zh-CN.png)

7.  单击**安装**。

## 步骤二：创建FTP用户名及密码 {#section_ztx_c4b_edr .section}

完成以下操作，创建Windows用户名和密码，用于FTP使用。如果您希望匿名用户可以访问，可省略此步骤。

1.  单击**开始** \> **管理工具** \> **服务器管理器**。
2.  单击**配置** \> **本地用户和组** \> **用户**，并在右侧空白处单击右键，再选择**新用户**。
3.  在新用户对话框中，设置用户名和密码。然后单击**创建**。 本示例中**用户名**使用ftptest。

    **说明：** 密码必须包括大写字母、小写字母和数字。否则会显示无法通过密码策略。

    ![添加新用户](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516334712584_zh-CN.png)


## 步骤三：设置共享文件的权限 {#section_jd9_tsn_noi .section}

您需要为在FTP站点共享给用户的文件夹设置访问和修改等权限。

1.  在服务器磁盘上创建一个供FTP使用的文件夹。右键单击文件夹，选择**属性**。 本示例中，在C盘下创建一个名为ftp的文件夹。
2.  单击**安全**页签，然后单击**编辑**。
3.  单击**添加**。
4.  在弹出的对话框中，输入对象名称Everyone，然后单击**确定**。
5.  在**组或用户名**区域，单击刚刚添加的**Everyone**，然后根据需要，选择**Everyone**的权限，本示例中允许所有权限。 

    ![设置权限](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516334712586_zh-CN.png)


## 步骤四：添加及设置FTP站点 {#section_0gy_5s5_oku .section}

安装FTP，设置好共享文件夹权限后，您需要创建FTP站点。

1.  单击**开始** \> **所有程序** \> **管理工具** \> **Internet 信息服务（IIS）管理器**。
2.  在左侧导航栏，右键单击**网站**，选择**添加 FTP 站点**。 

    ![添加FTP站点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516334712587_zh-CN.png)

3.  在弹出的对话框中，填写**FTP站点名称**与共享文件夹的**物理路径**，然后单击**下一步**。 本示例中**FTP 站点名称**设置为ftptest，**物理路径**请选择在[步骤三：设置共享文件的权限](#section_jd9_tsn_noi)中创建的FTP文件夹路径。

    ![添加FTP站点信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516334754646_zh-CN.png)

4.  **IP 地址**默认选择**全部未分配**。端口号可自行设置，FTP默认端口号为21。
5.  选择SSL设置，然后单击**下一步**。 

    -   **允许**：允许FTP服务器支持与客户端的非SSL和SSL连接。
    -   **需要**：需要对FTP服务器和客户端之间的通信进行SSL加密。
    -   **无**： 不需要SSL加密。
    ![绑定和SSL设置](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516334812588_zh-CN.png)

6.  选择要使用的一种或多种身份验证方法。 
    -   **匿名**：允许任何仅提供用户名**anonymous**或**ftp**的用户访问内容。
    -   **基本**：需要用户提供有效用户名和密码才能访问内容。由于基本身份验证通过网络传输未加密的密码，因此请仅在清楚客户端和FTP服务器之间的连接是安全的情况下（例如，使用安全套接字层SSL时）使用此身份验证方法。
7.  从**允许访问**列表中，选择以下选项之一： 
    -   **所有用户**：所有用户（不论是匿名用户还是已标识的用户）均可访问相应内容。
    -   **匿名用户**：匿名用户可访问相应内容。
    -   **指定角色或用户组**：仅特定角色或用户组的成员才能访问相应内容。请在对应的文本框中输入角色或用户组。
    -   **指定用户**：仅指定用户才能访问相应内容。请在对应的文本框中输入用户名。
8.  选中经过授权的用户的**读取**和**写入**权限。然后单击**完成**。 

    ![身份验证和授权信息](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516335912589_zh-CN.png)


完成后可以看到搭建的FTP站点。

![FTP站点](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516335912590_zh-CN.png)

## 步骤五：设置安全组及防火墙 {#section_ovb_r91_w7d .section}

搭建好FTP站点后，您需要在实例安全组的入方向添加一条放行FTP端口的安全组规则，具体步骤请参见[添加安全组规则](../cn.zh-CN/安全/安全组/添加安全组规则.md#)，具体配置请参见[安全组应用案例](../cn.zh-CN/安全/安全组/安全组应用案例.md#)和[常用端口的典型应用](../cn.zh-CN/安全/安全组/常用端口的典型应用.md#)。

服务器防火墙默认放行TCP 21端口用于FTP服务。如果选用其他端口，您需要在防火墙中添加一条放行此端口的入站规则。

具体操作，请参见[设置 ECS 实例远程连接防火墙](http://help.aliyun.com/document_detail/40858.html)。

其他防火墙设置请参见[微软官方文档](https://technet.microsoft.com/zh-cn/library/hh831655(v=ws.11).aspx#Step4)。

## 步骤六：客户端测试 {#section_xex_vgd_epn .section}

完成以下步骤，在客户端上测试：

1.  设置IE浏览器。 
    1.  打开IE浏览器，单击**设置** \> **Internet选项**。
    2.  单击**高级**页签。在**设置**区域，选中**启用 FTP 文件夹视图**复选框，清除**使用被动 FTP**复选框。
2.  打开客户端的**计算机**，在路径栏中输入`ftp://服务器 IP 地址:FTP 端口`（如果不填端口则默认访问21端口），例如：`ftp://0.0.0.0:20`。 

    ![输入ftp地址](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516335912591_zh-CN.png)

    如果弹出输入用户名和密码的对话框表示配置成功，输入正确的用户名和密码后，即可对FTP文件进行相应权限的操作。本示例中，请输入[步骤二：创建FTP用户名及密码](#section_ztx_c4b_edr)中创建的FTP用户名（ftptest）和对应的密码。

    ![登录身份](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21753/156516335954648_zh-CN.png)


您可以对 FTP 服务进行安全加固。详情请参见[安全加固方案](https://help.aliyun.com/knowledge_detail/37452.html)。

如果您想基于FTP协议来管理存储在OSS上的文件，您可以安装OSS FTP。具体操作，请参见[安装OSS FTP](../../../../../cn.zh-CN/常用工具/ossftp/如何快速安装ossftp.md#)。OSS FTP接收普通FTP请求后，将对文件、文件夹的操作映射为对OSS的操作。

