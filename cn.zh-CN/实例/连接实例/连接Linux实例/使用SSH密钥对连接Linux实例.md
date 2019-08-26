# 使用SSH密钥对连接Linux实例 {#concept_ucj_wrx_wdb .task}

本文介绍了如何在Windows和Linux环境中使用SSH密钥对登录Linux实例。

在开始使用SSH密钥对连接Linux实例前，请确保您已经完成以下操作：

-   在控制台创建密钥对并下载了.pem私钥文件，详细步骤请参见[创建SSH密钥对](../cn.zh-CN/安全/SSH密钥对/使用SSH密钥对.md#section_f5c_h31_ydb)。
-   持有一台分配了密钥对的Linux实例。您可以在创建ECS实例时分配密钥对，详细步骤请参见[创建ECS实例](../cn.zh-CN/个人版快速入门/创建ECS实例.md#)。如果未在创建实例时分配密钥对，您也可以为已有实例绑定密钥对，详细步骤请参见[绑定SSH密钥对](../cn.zh-CN/安全/SSH密钥对/使用SSH密钥对.md#section_d4l_ql1_ydb)。

    **说明：** 如果ECS实例处于**运行中**（Running）状态，绑定SSH密钥对后，您必须在控制台或者使用API重启实例，才能使操作生效。

-   为实例所在的安全组添加以下安全组规则，详细步骤请参见[添加安全组规则](../cn.zh-CN/安全/安全组/添加安全组规则.md#)。

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
    |----|----|----|----|----|----|----|----|---|
    |VPC|不需要配置|入方向|允许|SSH\(22\)|22/22|地址段访问|0.0.0.0/0|1|
    |经典网络|公网|


## 本地为Windows环境 {#windows .section}

在控制台创建密钥对后自动生成的私钥文件格式为.pem，本节以PuTTYgen为例介绍如何转换私钥文件格式，并以PuTTY为例介绍如何通过SSH远程登录Linux实例。

1.  下载并安装PuTTYgen和PuTTY。 

    下载链接如下：

    -   [PuTTYgen](https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe)
    -   [PuTTY](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe)
2.  将.pem私钥文件转换为.ppk私钥文件。 
    1.  启动PuTTYgen。 本示例中的PuTTYgen版本为0.71。
    2.  选择**Type of key to generate**为**RSA**，然后单击**Load**。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/156568674651179_zh-CN.png)

    3.  选择**All Files**。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15656867465188_zh-CN.png)

    4.  选择待转换的.pem私钥文件。
    5.  在弹出的对话框中，单击**确定**。
    6.  单击**Save private key**。
    7.  在弹出的对话框中，单击**是**。
    8.  指定.ppk私钥文件的名称，然后单击**保存**。
3.  启动PuTTY。
4.  配置用于身份验证的私钥文件。 

    1.  选择**Connection** \> **SSH** \> **Auth**。
    2.  单击**Browse…**。
    3.  选择转换好的.ppk私钥文件。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15656867465191_zh-CN.png)

5.  配置连接Linux实例所需的信息。 

    1.  单击**Session**。
    2.  在**Host Name \(or IP address\)**中输入登录账号和实例公网IP地址。 格式为**root@IP 地址**。
    3.  在**Port**中输入端口号**22**。
    4.  选择**Connection type**为**SSH**。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/15656867465192_zh-CN.png)

6.  单击**Open**。 

    当出现以下提示时，说明您已经成功地使用SSH密钥对登录了实例。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9620/156568674651203_zh-CN.png)


## 本地为Linux或其它支持SSH命令的环境 {#linux .section}

本节介绍如何在Linux或其他支持SSH命令的环境（例如Windows下的MobaXterm）下使用SSH密钥对登录Linux实例。

-   通过命令配置所需信息并连接实例。
    1.  找到.pem私钥文件在本地机上的存储路径，例如/root/mysshkey.pem。

        **说明：** 此处路径和文件名称仅为示例，请根据实际情况修改。

    2.  运行以下命令修改私钥文件的属性。

        ``` {#codeblock_os2_q0l_vzt}
        chmod 400 [.pem私钥文件在本地机上的存储路径]
        ```

        示例如下：

        ``` {#codeblock_t6i_dxz_pez}
        chmod 400 /root/mysshkey.pem
        ```

    3.  运行以下命令连接至实例。

        ``` {#codeblock_jbu_lkq_l3d}
        ssh -i [.pem私钥文件在本地机上的存储路径] root@[公网IP地址]
        ```

        示例如下：

        ``` {#codeblock_db6_cnn_61w}
        ssh -i /root/mysshkey.pem root@10.10.xx.xxx
        ```

-   通过config配置所需信息并通过命令连接实例。
    1.  进入根目录下的ssh目录，按照如下方式修改config文件。

        ``` {#codeblock_gdt_den_x73}
        Host ecs    // 输入ECS实例的名称
        HostName 192.*.*.*   // 输入ECS实例的公网IP地址
        Port 22   // 输入端口号，默认为22
        User root   // 输入登录账号
        IdentityFile ~/.ssh/ecs.pem // 输入.pem私钥文件在本机的地址
        ```

    2.  保存config文件。
    3.  重启SSH。
    4.  运行命令连接至实例。

        ``` {#codeblock_hga_83q_t8h}
        ssh [ECS名称]
        ```

        示例如下：

        ``` {#codeblock_3o7_a10_2hj}
        ssh ecs
        ```


**相关文档**  


[使用管理终端连接Linux实例](cn.zh-CN/实例/连接实例/连接Linux实例/使用管理终端连接Linux实例.md#)

[使用用户名密码验证连接Linux实例](cn.zh-CN/实例/连接实例/连接Linux实例/使用用户名密码验证连接Linux实例.md#)

