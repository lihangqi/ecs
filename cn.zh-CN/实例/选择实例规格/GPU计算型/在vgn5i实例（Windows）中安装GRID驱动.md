# 在vgn5i实例（Windows）中安装GRID驱动 {#task_264305 .task}

如果您的GPU计算型实例需要支持OpenGL图形显示，必须安装GRID驱动。GPU计算型实例配备的NVIDIA GPU计算卡尚未激活NVIDIA GRID License，GPU图形功能受到限制。您可以安装NVIDIA官方发布的试用版GRID驱动来使用OpenGL图形功能。本文以操作系统为Windows Server 2016 64-bit的轻量级GPU计算性实例vgn5i为例，介绍如何安装GRID驱动。

-   创建一台vgn5i实例，确保实例可以访问公网，具体操作请参见[创建GPU计算型实例](cn.zh-CN/实例/选择实例规格/GPU计算型/创建GPU计算型实例.md#)。

    **说明：** 建议您选择**公共镜像**中的镜像。

-   使用Windows Remote Desktop或者在本地机器上安装远程连接工具，例如VNC Viewer。
-   获取GRID License：
    -   访问[NVIDIA官网](https://www.nvidia.com/object/nvidia-enterprise-account.html)填写注册信息，审批通过后即获取90天试用的License。
    -   联系阿里云客户支持人员获取用于临时测试的License。
    -   向NVIDIA购买License。

1.  [远程连接实例](cn.zh-CN/实例/连接实例/连接方式导航.md#section_mjm_rgx_wdb)。
2.  下载GRID驱动安装包。 
    -   如果实例位于华南1 可用区C、可用区D下，请下载[GRID 7.0 Guest驱动](http://nvdia-driver-410.oss-cn-shenzhen.aliyuncs.com/Windows_Guest_Drivers.zip)。
    -   如果实例位于其它地域和可用区，请下载GRID 8.0 Guest驱动：
        -   [适用于Win10、Windows Server 2016的GRID8.0驱动](http://nvidia-418.oss-cn-shenzhen.aliyuncs.com/425.31_grid_win10_server2016_64bit_international.exe)
        -   [适用于Win8、Win7、Windows Server 2012R2、Windows Server 2008R2的GRID8.0驱动](http://nvidia-418.oss-cn-shenzhen.aliyuncs.com/425.31_grid_win8_win7_server2012R2_server2008R2_64bit_international.exe)
3.  双击安装包，按提示完成安装。 

    **说明：** 对于Windows系统，GPU驱动安装生效后，Windows自带的远程连接（RDP）协议有可能不支持DirectX、OpenGL等相关应用。您需要自行安装VNC服务和客户端，或其它支持此类应用的协议，例如PCOIP、XenDeskop HDX 3D等。

4.  重启实例。
5.  添加License服务器并激活License。 
    1.  [远程连接实例](cn.zh-CN/实例/连接实例/连接方式导航.md#section_mjm_rgx_wdb)。
    2.  右击桌面，然后单击**NVIDIA 控制面板**。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/217881/155911446047965_zh-CN.png)

    3.  选择**许可** \> **管理许可证**。
    4.  输入License服务器的IP和端口，然后单击**应用**。 

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/217881/155911446047967_zh-CN.png)

        显示**您的系统已获取GRID vGPU许可**，表示License激活成功。


