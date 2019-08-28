# 创建GPU计算型实例 {#concept_g5s_g2z_xdb .task}

GPU计算型实例必须安装GPU驱动才可以使用。您可以在创建实例时自动安装GPU驱动，也可以在实例创建后手动安装GPU驱动。本文介绍如何创建GPU计算型实例并自动安装驱动。

如果您使用了自动安装GPU驱动功能，请注意：

-   自动安装只支持Linux公共镜像。
-   自动安装脚本已更新到v2.1版本，支持自动安装不同版本的GPU驱动、CUDA、cuDNN库。
-   自动安装过程受不同实例规格的内网带宽和CPU核数的影响，安装时间约10～15分钟，在安装过程中无法使用GPU，请勿对实例进行任何操作，也不要安装其它GPU相关软件，以防自动安装失败，导致实例不可用。
-   如果您在创建完成后更换操作系统 ，请确保使用同一镜像或者为可自动安装CUDA和GPU驱动的镜像，以防自动安装失败。详情请参见[支持自动安装CUDA和GPU驱动的镜像](#step_cq7_0by_971)。
-   您可以远程连接实例，通过安装日志查看安装进程和结果：
    -   如果正在安装，您可以看到安装进度条。
    -   如果已经安装成功，您可以看到安装结果提示**NVIDIA INSTALL OK**。
    -   如果安装失败，您将看到安装结果提示**NVIDIA INSTALL FAIL**。
    -   详细安装日志位于/root/nvidia/nvidia\_install.log。

## 操作步骤 {#section_v44_dhm_ks8 .section}

本步骤重点介绍GPU计算型实例相关的配置，如果您想了解其他通用配置，请参见[创建ECS实例](intl.zh-CN/实例/创建实例/使用向导创建实例.md#)。

1.  前往[ECS售卖页](https://ecs-buy.aliyun.com/wizard/#/)。
2.  完成基础配置。在选择配置时，请注意： 
    -   **地域**：请根据下表选择地域和可用区。如果售卖页显示的地域和可用区和表格不一致，以售卖页为准。

        提供各GPU计算型实例规格族的地域和可用区如下表所示：

        |实例规格|地域和可用区|
        |----|------|
        |gn4|         -   华北2（北京）可用区A，华东2（上海）可用区B
        -   华南1（深圳）可用区C、B
 |
        |gn5|         -   华北2（北京）可用区D、G、C，华北3（张家口）可用区A、B，华北5（呼和浩特）可用区A
        -   华东1（杭州）可用区I、G、F，华东2（上海）可用区F、D、B、E
        -   华南1（深圳）可用区A、B、C、D、E
        -   中国（香港）可用区C、B
        -   新加坡 可用区B、A，澳大利亚（悉尼）可用区B、A，马来西亚（吉隆坡）可用区B、A，印度尼西亚（雅加达）可用区A
        -   日本（东京）可用区B、A
        -   美国（硅谷）可用区B、A，美国（弗吉尼亚）可用区B、A
        -   德国（法兰克福）可用区B、A
        -   印度（孟买）可用区A
 |
        |gn5i|         -   华北2（北京）可用区G、C、E，华北3（张家口）可用区A、B
        -   华东1（杭州）可用区G、B，华东2（上海）可用区D、E
        -   华南1（深圳）可用区A、C、D、E
 |
        |gn6v|         -   华北2（北京）可用区H、G，华北3（张家口）可用区A、B
        -   华东1（杭州）可用区H、I，华东2（上海）可用区F
        -   华南1（深圳）可用区E
        -   美国（硅谷）可用区B
 |
        |gn6i|         -   华东1（杭州）可用区H，华东2（上海）可用区F、G
        -   华南1（深圳）可用区E
        -   新加坡 可用区C
 |

    -   **实例**：定位到**异构计算GPU/FPGA** \> **GPU计算型**，然后根据需求选择实例规格。
    -   **镜像**：部分公共镜像支持自动安装GPU驱动，您也可以在镜像市场选择预装了GPU驱动和相关软件的镜像。

        **说明：** 如果您使用共享镜像和自定义镜像，需要自行保证安装了需要的GPU驱动和相关软件。

        -   公共镜像是由阿里云官方或第三方合作商家提供的系统基础镜像，支持自动安装GPU驱动的公共镜像如下：

            -   CentOS 64位（目前提供的所有自营版本均支持）
            -   Ubuntu16.04 64位镜像
            -   Ubuntu18.04 64位镜像
            -   SUSE Linux Enterprise Server 12 SP2 64位镜像
            如果您选择的镜像支持自动安装GPU驱动，勾选**自动安装GPU驱动**，并选择GPU驱动、CUDA、cuDNN库版本。如果是新业务系统，建议选择最新的版本。

            对于支持自动安装GPU驱动的镜像，如果您不勾选**自动安装GPU驱动**，可以在**实例自定义数据**模块下配置安装脚本，安装脚本请参见[自动安装脚本v2.1](#section_bl2_k23_ygb)。

            如果您不使用自动安装GPU驱动功能，或者镜像不支持自动安装GPU驱动，您可以在创建实例后手动安装GPU驱动。具体操作，请参见[手动安装GPU驱动](intl.zh-CN/实例/选择实例规格/GPU计算型/手动安装GPU驱动.md#)。

            **说明：** 如果调用RunInstances接口创建GPU计算型实例，必须通过UserData参数上传安装脚本，脚本内容需要采用Base64方式编码。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9632/156679892639823_zh-CN.png)

        -   镜像市场提供经严格审核的优质镜像，预装操作系统、应用环境和各类软件，无需配置即可一键部署云服务器。目前镜像市场提供了支持深度学习和机器学习的镜像：
            -   如果GPU计算型实例用于深度学习，您可以选择预装深度学习框架的镜像。在镜像市场搜索关键字深度学习并选择可用的镜像，目前仅支持CentOS 7.3。
            -   如果GPU计算型实例用于机器学习，您可以选择预装RAPIDS加速库的镜像，在镜像市场搜索关键字RAPIDS并选择可用的镜像。目前仅支持Ubuntu16.04。更多信息，请参见[在GPU实例上使用RAPIDS加速图像搜索任务](../../../../intl.zh-CN/最佳实践/GPU实例最佳实践/在GPU实例上使用RAPIDS加速图像搜索任务.md#)。

                **说明：** 镜像中预装了NVIDIA RAPIDS机器学习加速库以及TensorFlow、Keras开源深度学习框架，您可以快速使用RAPIDS加速数据准备、机器学习和图像分析任务，并结合深度学习框架进行深度学习训练和推理。

            -   NVIDIA GPU Cloud VM Image（虚拟机镜像）是运行针对NVIDIA GPU优化的深度学习框架和HPC应用程序容器的优化环境。gn5、gn5i、gn6v、gn6i均支持NGC，更多信息，请参见[在gn5实例上部署NGC环境](../../../../intl.zh-CN/最佳实践/GPU实例最佳实践/在gn5实例上部署NGC环境.md#)。
3.  完成网络和安全组配置。在选择配置时，请注意： 
    -   **网络**：选择**专有网络**。
    -   **公网带宽**：请根据您的业务需要选择带宽。

        **说明：** 如果您在**基础配置**中选用了Windows 2008 R2及以下版本的镜像，在GPU驱动安装生效后，您将无法通过管理终端连接GPU计算型实例，远程连接时会始终显示黑屏或停留在启动界面。您需要在此处勾选**分配公网IP地址**，或者在创建实例后绑定弹性公网IP，以便通过其他协议连接实例，例如RDP（Windows自带的远程连接）、PCOIP、XenDeskop HDX 3D等。其中RDP不支持DirectX、OpenGL等应用，您需要自行安装VNC服务和客户端。

4.  完成系统配置。在选择配置时，请注意： 
    -   **登录凭证**：建议选择**密钥对**或**自定义密码**。如果您选择**创建后设置**，通过管理终端登录实例时必须绑定SSH密钥对或者重置密码，然后重启实例使修改生效。如果此时GPU驱动尚未安装完成，重启操作会导致安装失败。
    -   **实例自定义数据**：
        -   如果您在基础配置页面的**镜像**中选择了**自动安装GPU驱动**，此处会显示自动安装CUDA和GPU驱动的注意事项和Shell脚本内容。

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9632/156679892739825_zh-CN.png)

        -   如果您未选择**自动安装GPU驱动**，可以在**实例自定义数据**处配置安装脚本，脚本示例请参见[自动安装脚本v2.1](#section_bl2_k23_ygb)。
5.  根据需要完成分组设置并确认订单，完成创建GPU计算型实例。 

    **说明：** 

    -   如果您配置了自动安装脚本，实例启动后会自动安装GPU驱动。安装完成后实例会自动重启，重启过后GPU驱动才能正常工作。
    -   GPU驱动在Persistence Mode下工作更稳定。安装脚本会自动开启GPU驱动的Persistence Mode，并将该设置添加到Linux系统服务中，开机自动启动服务，确保实例重启后还能默认开启Persistence Mode。

## 自动安装GPU驱动脚本 {#section_xcj_1s5_xgb .section}

实例首次启动时，cloud-init会自动执行Shell脚本安装GPU驱动、CUDA、cuDNN库。

-   如果您勾选了**自动安装GPU驱动**，可选的GPU驱动、CUDA、cuDNN库版本如下：

    |CUDA|GPU驱动|cuDNN|支持的实例规格|支持的公共镜像版本（仅支持自营镜像）|
    |----|-----|-----|-------|------------------|
    |10.1.168|418.67|7.5.0|     -   gn5
    -   gn5i
    -   gn6v
    -   gn4
    -   gn6i
 |     -   Ubuntu18.04
    -   Ubuntu16.04
    -   Centos7.x
    -   Centos6.x
 |
    |10.0.130|     -   418.67
    -   410.104
 |     -   7.5.0
    -   7.4.2
    -   7.3.1
 |     -   gn5
    -   gn5i
    -   gn6v
    -   gn4
    -   gn6i
 |     -   Ubuntu18.04
    -   Ubuntu16.04
    -   Centos7.x
    -   Centos6.x
 |
    |9.2.148|     -   418.67
    -   410.104
 |     -   7.5.0
    -   7.4.2
    -   7.3.1
    -   7.1.4
 |     -   gn5
    -   gn5i
    -   gn4
    -   gn6v
 |     -   Ubuntu16.04
    -   Centos7.x
    -   Centos6.x
 |
    |9.0.176|     -   418.67
    -   410.104
    -   390.116
 |     -   7.5.0
    -   7.4.2
    -   7.3.1
    -   7.1.4
    -   7.0.5
 |     -   gn5
    -   gn5i
    -   gn4
    -   gn6v
 |     -   Ubuntu16.04
    -   Centos7.x
    -   Centos6.x
    -   SUSE 12sp2
 |
    |8.0.61|     -   418.67
    -   410.104
    -   390.116
 |     -   7.1.3
    -   7.0.5
 |     -   gn5
    -   gn5i
    -   gn4
 |     -   Ubuntu16.04
    -   Centos7.x
    -   Centos6.x
 |

-   如果您在**实例自定义数据**配置安装脚本，脚本内容请参见[自动安装脚本v2.1](#section_bl2_k23_ygb)。

    自动安装脚本v2.1具有以下优势：

    -   提供最新版本的CUDA、GPU驱动和cuDNN库。
    -   登录实例后，如果正在安装驱动，您可以看到安装进度条。如果已经安装成功，您可以看到安装结果提示**NVIDIA INSTALL OK**；如果安装失败，您将看到安装结果提示**NVIDIA INSTALL FAIL**。
    使用自动安装脚本v2.1时，您需要修改安装脚本的以下参数，指定GPU驱动、CUDA、cuDNN版本号，例如：

    ``` {#codeblock_wyr_3ly_ap6}
    DRIVER_VERSION="410.104"
    CUDA_VERSION="10.0.130"
    CUDNN_VERSION="7.5.0"
    ```

    **说明：** 如果镜像是CentOS或SUSE操作系统，安装脚本使用.run安装包进行安装，如果镜像是Ubuntu操作系统，安装脚本使用.deb安装包进行安装。


## 自动安装脚本v2.1 {#section_bl2_k23_ygb .section}

``` {#codeblock_kt8_pv1_y35}
#!/bin/sh

#Please input version to install
DRIVER_VERSION=""
CUDA_VERSION=""
CUDNN_VERSION=""

INSTALL_DIR="/root/nvidia"
log=${INSTALL_DIR}/nvidia_install.log

#using .deb to install driver and cuda on ubuntu OS
#using .run to install driver and cuda on ubuntu OS
nvidia_script="nvidia_install.sh"
script_download_url=$(curl http://100.100.100.200/latest/meta-data/source-address | head -1)"/opsx/ecs/linux/binary/nvidia/script/${nvidia_script}"
echo $script_download_url

mkdir $INSTALL_DIR && cd $INSTALL_DIR
wget -t 10 --timeout=10 $script_download_url && sh ${INSTALL_DIR}/${nvidia_script} $DRIVER_VERSION $CUDA_VERSION $CUDNN_VERSION
```

**相关文档**  


[手动安装GPU驱动](intl.zh-CN/实例/选择实例规格/GPU计算型/手动安装GPU驱动.md#)

[在GPU计算型实例中安装GRID驱动](intl.zh-CN/实例/选择实例规格/GPU计算型/在GPU计算型实例中安装GRID驱动.md#)

[手动卸载GPU驱动](intl.zh-CN/实例/选择实例规格/GPU计算型/手动卸载GPU驱动.md#)

[GPU监控](../../../../intl.zh-CN/用户指南/主机监控/GPU监控.md#)

