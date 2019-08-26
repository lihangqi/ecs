# 在vgn5i实例（Linux）中安装GRID驱动 {#task_265413 .task}

如果您的GPU计算型实例需要支持OpenGL图形显示，必须安装GRID驱动。GPU计算型实例配备的NVIDIA GPU计算卡尚未激活NVIDIA GRID License，GPU图形功能受到限制。您可以安装NVIDIA官方发布的试用版GRID驱动来使用OpenGL图形功能。本文以操作系统为Ubuntu 16.04 64-bit的轻量级GPU计算性实例vgn5i为例，介绍如何安装GRID驱动。

-   创建一台vgn5i实例，确保实例可以访问公网，具体操作请参见[创建GPU计算型实例](intl.zh-CN/实例/选择实例规格/GPU计算型/创建GPU计算型实例.md#)。

    **说明：** 建议您选择**公共镜像**中的镜像。

-   在本地机器上安装远程连接工具，例如VNC Viewer。
-   获取GRID License：
    -   访问[NVIDIA官网](https://www.nvidia.com/object/nvidia-enterprise-account.html)填写注册信息，审批通过后即获取90天试用的License。
    -   联系阿里云客户支持人员获取用于临时测试的License。
    -   向NVIDIA购买License。

1.  禁用nouveau。 
    1.  [远程连接实例](intl.zh-CN/实例/连接实例/连接方式导航.md#section_fjm_rgx_wdb)。
    2.  查看是否存在blacklist-nouveau.conf文件。 

        ``` {#codeblock_7zf_4ev_kc1}
        ls /etc/modprobe.d/blacklist-nouveau.conf
        ```

    3.  如果文件存在，则跳过本步骤。如果文件不存在，则执行命令`vim /etc/modprobe.d/blacklist-nouveau.conf`创建文件，并在文件中添加以下内容禁用nouveau。 

        ``` {#codeblock_g6f_j4z_pvs}
        blacklist nouveau
        blacklist lbm-nouveau
        options nouveau modeset=0
        ```

    4.  生成kernel initramfs。 

        ``` {#codeblock_ld4_m8t_tic}
        rmmod nouveau
        update-initramfs -u
        ```

    5.  重启实例。 

        ``` {#codeblock_e9q_zsd_esn}
        reboot
        ```

2.  下载GRID驱动包。 
    1.  [远程连接实例](intl.zh-CN/实例/连接实例/连接方式导航.md#section_fjm_rgx_wdb)。
    2.  下载GRID驱动安装包。 
        -   如果实例位于华南1 可用区C、可用区D下，请下载GRID 7.0 Guest驱动：

            ``` {#codeblock_174_jwp_hm0}
            wget http://nvdia-driver-410.oss-cn-shenzhen.aliyuncs.com/NVIDIA-Linux-x86_64-410.39-grid.run
            ```

        -   如果实例位于其它地域和可用区，请下载GRID 8.0 Guest驱动：

            ``` {#codeblock_j73_ryt_kza}
            wget http://nvidia-418.oss-cn-shenzhen.aliyuncs.com/NVIDIA-Linux-x86_64-418.70-grid.run
            ```

3.  安装GRID驱动。 

    ``` {#codeblock_q5p_a0t_2yt}
    chmod +x NVIDIA-Linux-x86_64-410.39-grid.run
    ./NVIDIA-Linux-x86_64-410.39-grid.run
    ```

4.  测试GRID驱动是否安装成功。 

    ``` {#codeblock_14q_dqo_bhf}
    nvidia-smi
    ```

    如果返回以下GRID驱动信息，说明驱动安装成功。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/218964/156221945047400_zh-CN.png)

5.  添加License服务器。 
    1.  切换到/etc/nvidia目录。 

        ``` {#codeblock_n3j_934_bd0}
        cd /etc/nvidia
        ```

    2.  创建gridd.conf文件。 

        ``` {#codeblock_hov_9c8_fpw}
        cp gridd.conf.template gridd.conf
        ```

    3.  在gridd.conf文件中添加License服务器的信息。 

        **说明：** 您需要向NVIDIA购买License后自行搭建License服务器。

        ``` {#codeblock_5bd_ljr_qtw}
        ServerAddress=License服务器的IP
        ServerPort=License服务器的端口（默认为7070）
        FeatureType=1
        ```

6.  重启实例使License服务器配置生效。 

    ``` {#codeblock_akc_eql_1tw}
    reboot
    ```

7.  查看License是否激活成功。 
    1.  [远程连接实例](intl.zh-CN/实例/连接实例/连接方式导航.md#section_fjm_rgx_wdb)。
    2.  查看License状态。 

        ``` {#codeblock_yie_9gq_qll}
        systemctl status nvidia-gridd
        ```

        返回结果显示**License acquired successfully**，表示License激活成功。

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/218964/156221945147964_zh-CN.png)


