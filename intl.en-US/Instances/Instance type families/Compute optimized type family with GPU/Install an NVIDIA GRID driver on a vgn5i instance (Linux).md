# Install an NVIDIA GRID driver on a vgn5i instance \(Linux\) {#task_265413 .task}

This topic describes how to install an NVIDIA GRID driver for instances running 64-bit Ubuntu 16.04 of the vgn5i instance type family. You must install an NVIDIA GRID driver if your GPU-equipped compute optimized instance requires Open Graphics Library \(OpenGL\). By default, the NVIDIA GRID license granted to NVIDIA GPUs is not activated, but you can activate the license by using a trial license to build a license server.

-   A vgn5i instance that can access the Internet is created. For more information, see [Create a compute optimized instance with GPU](reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

    **Note:** We recommend that you select a **Public Image** when you create the instance.

-   A remote connection tool such as VNC Viewer is installed on your local machine.
-   An NVIDIA GRID license is obtained. If you need to obtain a license, you can:
    -   Visit the [NVIDIA official website](https://www.nvidia.com/object/nvidia-enterprise-account.html) and register an account to apply for a 90-day trial license.
    -   Obtain a temporary license from Alibaba Cloud technical support.
    -   Buy a license from NVIDIA.

1.  Disable Nouveau. 
    1.  [Connect to the instance](Connect to the instanceEN-US_TP_9618.dita#concept_tmr_pgx_wdb).
    2.  Check whether the blacklist-nouveau.conf file exists. 

        ``` {#codeblock_7zf_4ev_kc1}
        ls /etc/modprobe.d/blacklist-nouveau.conf
        ```

    3.  If the file exists, skip this step. If the file does not exist, run the `vim /etc/modprobe.d/blacklist-nouveau.conf` command to create the file and then add the following content to the file: 

        ``` {#codeblock_g6f_j4z_pvs}
        blacklist nouveau
        blacklist lbm-nouveau
        options nouveau modeset=0
        ```

    4.  Remove Nouveau and generate kernel initramfs. 

        ``` {#codeblock_ld4_m8t_tic}
        rmmod nouveau
        update-initramfs -u
        ```

    5.  Restart the instance. 

        ``` {#codeblock_e9q_zsd_esn}
        reboot
        ```

2.  Download the NVIDIA GRID driver package. 
    1.  [Connect to the instance](Connect to the instanceEN-US_TP_9618.dita#concept_tmr_pgx_wdb).
    2.  Download the NVIDIA GRID driver package. 
        -   If your instance is located in China \(Shenzhen\) Zone C or Zone D, run the following command to download GRID 7.0 Guest:

            ``` {#codeblock_174_jwp_hm0}
            wget http://nvdia-driver-410.oss-cn-shenzhen.aliyuncs.com/NVIDIA-Linux-x86_64-410.39-grid.run
            ```

        -   If your instance is located in other regions or zones, run the following command to download GRID 8.0 Guest:

            ``` {#codeblock_j73_ryt_kza}
            wget http://nvidia-418.oss-cn-shenzhen.aliyuncs.com/NVIDIA-Linux-x86_64-418.70-grid.run
            ```

3.  Install the NVIDIA GRID driver. 

    ``` {#codeblock_q5p_a0t_2yt}
    chmod +x NVIDIA-Linux-x86_64-410.39-grid.run
    ./NVIDIA-Linux-x86_64-410.39-grid.run
    ```

4.  Check whether the NVIDIA GRID driver is installed. 

    ``` {#codeblock_14q_dqo_bhf}
    nvidia-smi
    ```

    The driver is installed if GRID driver information similar to the following figure is displayed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/218964/156221946047400_en-US.png)

5.  Add a license server. 
    1.  Switch to the /etc/nvidia directory. 

        ``` {#codeblock_n3j_934_bd0}
        cd /etc/nvidia
        ```

    2.  Create a gridd.conf file. 

        ``` {#codeblock_hov_9c8_fpw}
        cp gridd.conf.template gridd.conf
        ```

    3.  Add license server information to the created gridd.conf file. 

        ``` {#codeblock_5bd_ljr_qtw}
        ServerAddress=IP address of the license server
        ServerPort=Port of the license server (default port: 7070)
        FeatureType=1
        ```

6.  Restart the instance for the license server configuration to take effect. 

    ``` {#codeblock_akc_eql_1tw}
    reboot
    ```

7.  Check whether the license is activated. 
    1.  [Connect to the instance](Connect to the instanceEN-US_TP_9618.dita#concept_tmr_pgx_wdb).
    2.  Check the license status. 

        ``` {#codeblock_yie_9gq_qll}
        systemctl status nvidia-gridd
        ```

        The license is activated if **License acquired successfully** is displayed.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/218964/156221946047964_en-US.png)


