# 使用软件连接Windows实例 {#concept_n31_wyx_wdb .concept}

如果您的实例不能访问公网，您可以 [使用管理终端连接ECS实例](intl.zh-CN/用户指南/连接实例/使用管理终端连接ECS实例.md#)。

## 前提条件 {#section_hxc_qcy_wdb .section}

在远程连接之前，必须先完成以下工作：

-   实例状态必须为 **运行中**。如果实例不在运行中，必须 [启动实例](intl.zh-CN/用户指南/实例/启动或停止实例.md#) 。
-   实例已经设置登录密码。如果未设置或密码丢失，必须 [重置实例密码](intl.zh-CN/用户指南/实例/重置实例密码.md#)。
-   实例能访问公网：
    -   专有网络（VPC）下，在创建实例时购买带宽从而分配到一个公网 IP 地址，或者在创建实例后 [绑定一个弹性公网 IP 地址](../../../../intl.zh-CN/快速入门/搭建专有网络.md#section_ux1_cmw_rdb)。
    -   经典网络下，您的实例必须分配了公网IP地址。以下是获取公网IP地址的方法：
        -   无论是包年包月实例还是按量计费实例，您在创建实例时购买了带宽即会被分配一个公网IP地址。
        -   如果您在创建包年包月实例时未设置带宽，可以 [升级带宽](intl.zh-CN/用户指南/实例/升降配/升降配概述.md#) 获取公网IP地址。
-   实例所在的安全组必须添加以下安全组规则（具体操作，请参考 [添加安全组规则](intl.zh-CN/用户指南/安全组/添加安全组规则.md#)）：

    |网络类型|网卡类型|规则方向|授权策略|协议类型|端口范围|授权类型|授权对象|优先级|
    |----|----|----|----|----|----|----|----|---|
    |VPC|不需要配置|入方向|允许|RDP\(3389\)|3389/3389|地址段访问|0.0.0.0/0|1|
    |经典网络|公网|


## 操作步骤 {#section_b55_ycy_wdb .section}

根据本地设备的操作系统不同，您可以用不同的远程连接软件连接 Windows 实例：

-   [本地设备使用 Windows 操作系统](#)
-   [本地设备使用 Linux 或 Mac OS X 系统](#)
-   [本地设备使用Mac OS操作系统](#)
-   [本地设备使用Android或iOS系统](#)

## 本地设备使用Windows操作系统 {#windows .section}

如果本地设备使用Windows操作系统，您可以使用Windows自带的远程桌面连接工具MSTSC连接Windows实例。

1.  选择以下任一方式启动 **远程桌面连接**（MSTSC\)：
    -   选择 **开始** \> **附件** \> **远程桌面连接**。
    -   单击 **开始** 图标，在搜索框里中输入 mstsc 后按回车键确认。
    -   按快捷键 **Win**（Windows 徽标键）+**R** 启动 运行 窗口，输入 mstsc 后按回车键。
2.  在 远程桌面连接 对话框中：
    1.  单击 **显示选项**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/15395104655258_zh-CN.png)

    2.  输入实例的公网IP地址或EIP地址。
    3.  输入用户名，默认为 Administrator。

        **说明：** 如果您希望下次登录时不再手动输入用户名和密码，可以选择 **允许我保存凭据**。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/15395104655259_zh-CN.png)

    4.  （可选）如果您希望将本地文件拷贝到实例中，您可以设置通过远程桌面共享本地电脑资源：单击 **本地资源** 选项卡，然后，
        -   如果您需要从本地直接复制文字信息到实例中，选择 **剪贴板**。
        -   如果您需要从本地复制文件到实例中，单击 **详细信息**，选择驱动器后再选择文件存放的盘符。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/15395104655260_zh-CN.png)

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/15395104655261_zh-CN.png)

    5.  （可选）如果您对远程桌面窗口的大小有特定的需求，可以选择 **显示** 选项卡，再调整窗口大小。一般选择全屏。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9622/15395104655262_zh-CN.png)

    6.  单击 **连接**。

成功连接到实例后，您就可以开始操作实例了。

## 本地设备使用Linux操作系统 {#linux .section}

如果本地设备使用Linux操作系统，您可以使用远程连接工具连接Windows实例。这里以rdesktop为例说明。

1.  下载并启动rdesktop。
2.  运行以下命令连接Windows实例。将示例中的参数改为您自己的参数。

    ```
    rdesktop -u administrator -p password -f -g 1024*720 192.168.1.1 -r clipboard:PRIMARYCLIPBOARD -r disk:sunray=/home/yz16184
    ```

    参数说明如下表所示。

    |参数|说明|
    |:-|:-|
    |-u|用户名，Windows实例默认用户名是Administrator。|
    |-p|登录Windows实例的密码。|
    |-f|默认全屏，需要用 **Ctrl**+**Alt**+**Enter** 组合键进行全屏模式切换。|
    |-g|分辨率，中间用星号（\*）连接，可省略，省略后默认为全屏显示。|
    |192.168.1.1|需要远程连接的服务器IP地址。需要替换为您的Windows实例的公网IP地址或 EIP 地址。|
    |-d|域名，例如域名为INC，那么参数就是 `-d inc`。|
    |-r|多媒体重新定向。比如：    -   开启声音：`-r sound`。
    -   使用本地的声卡：`-r sound : local`。
    -   开启 U 盘：`-r disk:usb=/mnt/usbdevice`。
|
    |-r clipboard:PRIMARYCLIPBOARD|实现本地设备Linux系统和Windows实例之间直接复制粘贴文字。支持复制粘贴中文。|
    |-r disk:sunray=/home/yz16184|指定本地设备Linux系统上的一个目录映射到Windows实例上的硬盘， 这样就可以不再依赖Samba或者FTP传送文件。|


## 本地设备使用Mac OS操作系统 {#macOS1 .section}

如果您本地使用Mac OS操作系统，您可以参考 [微软官网文档](https://docs.microsoft.com/zh-cn/windows-server/remote/remote-desktop-services/clients/remote-desktop-mac) 操作。

## 本地设备使用Android或iOS系统 {#mobile .section}

如果要使用移动设备远程连接您的Windows实例时，您可以使用app。具体的操作描述，请参考 [在移动设备上连接实例](intl.zh-CN/用户指南/连接实例/在移动设备上连接实例.md#)。

