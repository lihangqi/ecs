# 手动安装GPU驱动 {#concept_ecy_qrz_wgb .concept}

如果在创建实例时没有自动安装GPU驱动，您必须在创建后手动安装。本文介绍如何下载和手动安装GPU驱动。

## 下载GPU驱动 {#installDrive .section}

1.  进入[NVIDIA 官网](http://www.nvidia.com/Download/index.aspx?lang=cn)。
2.  手动查找适用于实例的驱动程序，并单击**搜索**。筛选信息说明如下表所示。

    |信息项|gn4|gn5|gn5i|gn6v|gn6i|
    |:--|:--|:--|:---|:---|----|
    |产品类型|Tesla|Tesla|Tesla|Tesla|Tesla|
    |产品系列|M-Class|P-Series|P-Series|V-Series|T-Series|
    |产品家族|M40|Tesla P100|Tesla P4|Tesla V100|Tesla T4|
    |操作系统|根据实例的镜像选择对应的版本。 **说明：** 

    -   如果下拉列表中没有显示服务器操作系统，请单击下拉列表底部的**选择所有操作系统**。
    -   Debian操作系统，选择**Linux 64-bit**。
 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9632/15611107365114_zh-CN.png)

|

3.  确认无误后，单击**下载**按钮。

## 为Linux实例安装GPU驱动 {#section_esm_dc1_4gb .section}

**说明：** vgn5i实例的驱动安装不适用以下步骤，详细步骤请参见[在vgn5i实例（Linux）中安装GRID驱动](cn.zh-CN/实例/选择实例规格/GPU计算型/在vgn5i实例（Linux）中安装GRID驱动.md#)。

1.  下载并安装kernel对应版本的kernel-devel和kernel-header包。

    **说明：** kernel-devel和kernel版本不一致会导致在安装driver rpm过程中driver编译出错。您可以在实例里运行rpm –qa | grep kernel检测版本是否一致。确认版本后，再重新安装驱动。

2.  运行命令sudo rpm -qa | grep $\(uname -r\)，确认已经完成下载并安装kernel-devel和kernel-header包：

    以CentOS 7.3为例，如果出现以下类似信息，表示已经完成安装。

    ``` {#codeblock_cp9_0rk_x20}
    
    kernel-3.10.0-514.26.2.el7.x86_64
    kernel-headers-3.10.0-514.26.2.el7.x86_64
    kernel-tools-libs-3.10.0-514.26.2.el7.x86_64
    python-perf-3.10.0-514.26.2.el7.x86_64
    kernel-tools-3.10.0-514.26.2.el7.x86_64
    ```

3.  按NVIDIA官网GPU驱动下载页的**其他信息**描述安装GPU驱动。

    以Linux 64-bit Ubuntu 14.04为例：

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9632/15611107375117_zh-CN.png)


## 为Windows实例安装GPU驱动 {#section_o2j_hrs_qgb .section}

**说明：** vgn5i实例的驱动安装不适用以下步骤，详细步骤请参见[在vgn5i实例（Windows）中安装GRID驱动](cn.zh-CN/实例/选择实例规格/GPU计算型/在vgn5i实例（Windows）中安装GRID驱动.md#)。

直接双击安装文件，按提示完成GPU驱动安装。

**说明：** 对于Windows系统，GPU驱动安装生效后，Windows自带的远程连接（RDP）协议不支持DirectX、OpenGL等相关应用。您需要自行安装VNC服务和客户端，或其它支持的协议，例如PCOIP、XenDeskop HDX 3D等。

