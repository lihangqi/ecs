# 使用SSH密钥对连接Linux实例 {#concept_ucj_wrx_wdb .concept}

本文介绍了如何在Windows和Linux环境中使用SSH密钥对登录Linux实例。

## 前提条件 {#section_zcp_vlq_pgb .section}

-   您已经拥有一台分配了密钥对的Linux实例。您可以在[创建ECS实例时分配密钥对](../../../../../intl.zh-CN/个人版快速入门/步骤 2：创建ECS实例.md#)，也可以为实例[绑定密钥对](intl.zh-CN//绑定和解绑 SSH 密钥对.md#)。
-   实例所在的安全组必须添加以下安全组规则。具体操作，请参见[添加安全组规则](../../../../../intl.zh-CN/安全/安全组/添加安全组规则.md#)。

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
    |----|----|----|----|----|----|----|----|---|
    |VPC|不需要配置|入方向|允许|SSH\(22\)|22/22|地址段访问|0.0.0.0/0|1|
    |经典网络|公网|


## 操作方式 {#section_zfx_jlq_pgb .section}

根据本地设备的操作系统，您可以用不同的方式使用 SSH 密钥对登录 Linux 实例：

-   [本地为Windows环境](#)
-   [本地为Linux或支持SSH命令的环境](#)

## 本地为Windows环境 {#windows .section}

本节以PuTTY和PuTTYgen为例，介绍如何在Windows环境中将阿里云生成的私钥文件转换为PuTTY支持的格式，并通过SSH远程连接工具登录Linux实例。

**说明：** 请提前下载并安装[PuTTY](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe)和[PuTTYgen](https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe)。

1.  （可选）如果您正在使用阿里云生成的.pem私钥文件，必须先按以下步骤转为.ppk私钥文件。如果您使用的私钥文件本身已经是.ppk文件，可以略过这一步。

    **说明：** 在[使用SSH密钥对](../../../../../intl.zh-CN/安全/SSH密钥对/使用SSH密钥对.md#)时下载.pem私钥文件。

    1.  启动PuTTYgen。本示例中的PuTTYgen版本为0.68。
    2.  在**Parameters** \> **Type of key to generate**中，选中RSA。

        **说明：** **Number of bits in a generated key**的值不需要设置，软件会根据导入的私钥信息自动更新。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15510813115187_zh-CN.png)

    3.  单击**Load**，选择显示所有类型的文件，找到您的.pem文件。

        **说明：** PuTTYgen默认仅显示扩展名为.ppk的文件。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15510813115188_zh-CN.png)

    4.  选择您从阿里云下载的.pem格式的私钥文件，然后单击**打开**。
    5.  单击**OK**（确定）关闭确认对话框。
    6.  单击**Save private key**。PuTTYgen会显示一条关于在没有口令的情况下保存密钥的警告，单击**是\(Y\)**。
    7.  指定与密钥对相同的私钥名称，保存。PuTTY会自动为文件添加.ppk扩展名。
2.  启动PuTTY。
3.  选择**Connection** \> **SSH** \> **Auth**，再单击**Browse…**，选择前面所生成的.ppk文件。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15510813125191_zh-CN.png)

4.  单击**Session**。
    -   在**Host Name \(or IP address\)**里输入账号和需要连接的实例公网IP地址，格式为**root@IP 地址**。
    -   在**Port**里输入端口号**22**。
    -   **Connection type**选择**SSH**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15510813125192_zh-CN.png)

5.  单击**Open**，开始连接您的Linux实例。

当页面上出现`Connection established.` 时，说明您已经成功地使用密钥对登录实例。

## 本地为Linux或其它支持SSH命令的环境 {#linux .section}

本节介绍如何在Linux或其他支持SSH命令的环境（如Windows下的MobaXterm）下使用SSH密钥对登录Linux实例。

-   **方式一**
    1.  找到您所下载的.pem私钥文件在本地机上的存储路径，例如/root/mysshkey.pem。

        **说明：** 在[使用SSH密钥对](../../../../../intl.zh-CN/安全/SSH密钥对/使用SSH密钥对.md#)时下载.pem私钥文件。此处路径和文件名称仅为示例，请根据实际情况修改。

    2.  运行命令修改私钥文件的属性：`chmod 400 [.pem私钥文件在本地机上的存储路径]`。例如， `chmod 400 /root/mysshkey.pem`。
    3.  运行命令连接至实例：`ssh -i [.pem私钥文件在本地机上的存储路径] root@[公网IP地址]`。例如， `ssh -i /root/mysshkey.pem root@10.10.10.100`。
-   **方式二**

    您也可以通过SSH配置来简化连接命令。

    1.  进入根目录下的ssh目录，按照如下方式修改config文件。

        ```
        Host ecs    // 输入ECS实例的名称
        HostName 192.*.*.*   // 输入ECS实例的公网IP地址
        Port 22   // 输入端口号，默认为22
        User root   // 输入登录账号
        IdentityFile ~/.ssh/ecs.pem // 输入.pem私钥文件在本机的地址
        ```

    2.  保存config文件。
    3.  重启SSH。
    4.  运行命令连接至实例：`ssh [ECS名称]`。例如，`ssh ecs`。

## 相关连接 {#section_ccc_3lq_pgb .section}

您也可以使用用户名密码验证连接Linux实例。具体操作，请参见[使用用户名密码验证连接Linux实例](intl.zh-CN/实例/实例生命周期/连接实例/使用用户名密码验证连接Linux实例.md#)和[使用管理终端连接Linux实例](intl.zh-CN/实例/实例生命周期/连接实例/使用管理终端连接Linux实例.md#)。

