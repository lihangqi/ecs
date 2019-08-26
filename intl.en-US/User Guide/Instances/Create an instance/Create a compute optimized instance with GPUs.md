# Create a compute optimized instance with GPUs {#concept_g5s_g2z_xdb .concept}

This topic describes how to create a compute optimized instance with GPUs \(known as GPU instances in this topic\). GPU instances are available in the gn4, gn5, gn5i, and gn6v instance type families.

## Create an instance {#section_v1b_nxz_xdb .section}

To create a GPU instance, complete the following settings. For more information, see [Create an ECS instance](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).

-   **Region**: Each instance type family is available only in the corresponding regions.

    -   gn4: North China 2 \(Zone A\), East China 2 \(Zone B\), South China 1 \(Zone C\)
    -   gn5: North China 2 \(Zone C and Zone E\), North China 5 \(Zone A\), East China 1 \(Zone F and Zone G\), East China 2 \(Zone B, Zone D, and Zone E\), South China 1 \(Zone D\), Hong Kong \(Zone B and Zone C\), Asia Pacific SE 1 \(Zone A and Zone B\), Asia Pacific SE 2 \(Zone A\), Asia Pacific SE 3 \(Zone A\), Asia Pacific SE 5 \(Zone A\), US West 1 \(Zone A and Zone B\), US East 1 \(Zone A and Zone B\), and EU Central 1 \(Zone A\)

        **Note:** If you want to deploy NVIDIA GPU Cloud \(NGC\) on a gn5 instance, the region availability differs. For more information, see [Deploy an NGC on gn5 instances](../../../../../reseller.en-US/Best Practices/GPU instances/Deploy an NGC on gn5 instances.md#).

    -   gn5i: North China 2 \(Zone A, Zone C, and Zone E\), East China 1 \(Zone B\), East China 2 \(Zone B and Zone D\), and South China 1 \(Zone A\)
    -   gn6v: East China 2 \(Zone F\)
    The preceding regions and zones are for reference only. The actual regions and zones are displayed on the page when you create an ECS instance.

-   **Instance Type**: Select **Heterogeneous Computing** \> **GPU Compute**, and then select an instance type as needed.
-   **Image**: To install a GPU driver and a CUDA library, use one of the following methods:
    -   **Method 1**: Select **Public Image**. From the drop-down list, select a CentOS 64-bit image \(any version\), the Ubuntu 16.04 64-bit image, or the SUSE Linux Enterprise Server 12 SP2 64-bit image. Then, select **Auto-install GPU Driver**, and select a CUDA library and a GPU driver as needed.

        **Note:** 

        -   If **Auto-install GPU Driver** is selected, **User Data** will be automatically generated. You can view **User Data** in the **Advanced** area on the **System Configurations** page.
        -   **User Data** is a shell script that can automatically download and install the CUDA library and the GPU driver. The installation takes about 5 to 10 minutes, depending on your intranet bandwidth and the number of your instance vCPU cores.
        -   After the instance is created and started successfully for the first time, the cloud-init tool runs the script to install the GPU driver.
        -   If you create a GPU instance by using [RunInstances](../../../../../reseller.en-US/API Reference/Instances/RunInstances.md#), you need to write the shell script to the `UserData` parameter in Base64 format.
    -   **Method 2**: Select **Marketplace Image**, search for NVIDIA, and then select an image. Currently, only CentOS 7.3 is supported.

        To use the GPU instance for deep learning, you can select an image pre-installed with the deep learning framework. Select **Marketplace Image**, search for Deep Learning, and then select the target image \(only CentOS 7.3 is available\).

    -   **Method 3**: For other images, [Download and install a GPU driver](#) after the instance is created.
-   **Network**: Select **VPC**.
-   **Network Billing Method**: Select a bandwidth as needed.

    **Note:** 

    -   If Windows 2008 R2 or an earlier OS is used, the GPU instance cannot be accessed by using the [Management Terminal](reseller.en-US/User Guide/Connect to instances/Connect to an instance by using the Management Terminal.md#) in the ECS console after the GPU driver becomes effective. Therefore, you must select **Assign Public IP**, or [Bind EIP](../../../../../reseller.en-US/User Guide/Bind EIP to cloud resources.md#) after creating the instance.
    -   If the GPU instance can access the Internet, you can log on to the GPU instance by using other protocols, such as the Remote Desktop Protocol \(RDP\) developed by Microsoft. RDP does not support DirectX or OpenGL. Therefore, you must install the VNC server and client, or use protocols that support DirectX or OpenGL, such as PCOIP and XenDesktop HDX 3D.
-   **Log on Credentials**: Set a logon credential as needed.

    **Note:** We recommend that you do not select **Set Later**. Otherwise, you will need to reset your password \(or associate an SSH key pair\) and restart the instance if you want to log on to the instance after it is created and before the GPU driver is installed. The restart will result in GPU driver installation failure.

-   **User Data**: If you select **Auto-install GPU Driver**, the corresponding shell script is displayed in this area.

## Install the GPU driver automatically {#section_gbb_nxz_xdb .section}

If you select **Auto-install GPU Driver**, you can [connect to the instance](reseller.en-US/User Guide/Connect to instances/Overview.md#) and read the log file `/root/nvidia_install.log` to check:

-   The installation progress after the instance is created.
-   The cause if the installation fails.

Warning:

Do not operate GPU or install any GPU-related software before the GPU driver is successfully installed. Otherwise, the installation will fail.

**Note:** 

-   After the GPU driver is successfully installed, the instance automatically restarts and the driver becomes effective.
-   The shell script enables the **Persistence Mode** of the driver and add this setup to the automatic startup script of the instance. This mode is then enabled by default whenever the instance is restarted. The GPU driver works more reliably in this mode.
-   When you [change the operating system](reseller.en-US/User Guide/Instances/Change the operating system.md#), note the following:
    -   If you replace Ubuntu 16.04 64-bit or SUSE Linux Enterprise Server 12 SP2 64-bit with other versions, the GPU driver cannot be installed automatically.
    -   If you replace your CentOS version, the GPU driver can still be installed automatically.
    -   If you replace your OS with another OS that does not support the automatic installation script, the GPU driver cannot be installed automatically.

## Install the GPU driver manually {#installDrive .section}

If you select an image without a pre-installed GPU driver, you need to install the GPU driver manually.

1.  Download the GPU driver package as follows:
    1.  Go to the [NVIDIA official website](https://www.nvidia.com/Download/index.aspx?lang=en-us).
    2.  Set the filter conditions that meet your instance, and then click **Search**. The filter conditions are described in the following table.

        |Item|gn4|gn5|gn5i|gn6v|
        |:---|:--|:--|:---|:---|
        |Product Type|Tesla|Tesla|Tesla|Tesla|
        |Product Series|M-Class|P-Series|P-Series|V-Series|
        |Product|M40|Tesla P100|Tesla P4|Tesla V100|
        |Operating System|Select an OS version based on the image of your instance. If your server operating system is not displayed in the drop-down list, click **Show all Operating Systems** at the bottom of the drop-down list.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9632/155055474938684_en-US.png)

|

    3.  Confirm your settings and click **DOWNLOAD**.
2.  Install the GPU driver as follows:
    -   For a Windows instance: Double-click the installation package.
    -   For a Linux instance, follow these steps:
        1.  Download and install the appropriate kernel-devel package and kernel-header package.
        2.  Run the following command to verify that the packages are successfully installed.

            ```
            sudo rpm -qa | grep $(uname -r)
            ```

            Take CentOS 7.3 as an example. If the following message is displayed, the packages are installed successfully.

            ```
            
            kernel-3.10.0-514.26.2.el7.x86_64
            kernel-headers-3.10.0-514.26.2.el7.x86_64
            kernel-tools-libs-3.10.0-514.26.2.el7.x86_64
            python-perf-3.10.0-514.26.2.el7.x86_64
            kernel-tools-3.10.0-514.26.2.el7.x86_64
            ```

        3.  Go to the download page of the driver, click the **ADDITIONAL INFORMATION** tab, and follow the instructions to install the driver.

            Take Linux 64-bit Ubuntu 14.04 as an example.

            ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9632/15505547495117_en-US.png)


## Install a GRID driver {#section_ubb_nxz_xdb .section}

If your gn5, gn5i, or gn6v instance requires OpenGL, you must install a GRID driver. For more information, see [Install a GRID driver on a gn5/gn5i/gn6v instance](../../../../../reseller.en-US/Best Practices/GPU instances/Install a GRID driver on a gn5__gn5i__gn6v instance.md#).

