# Install the GPU driver {#concept_ecy_qrz_wgb .concept}

This topic describes how to download and install the GPU driver. If you do not configure your GPU driver to automatically install when you create the GPU instance, you must install it manually after the GPU instance is created.

## Download the GPU driver {#installDrive .section}

To download a GPU driver, follow these steps:

1.  Go to [NVIDIA website](http://www.nvidia.com/Download/index.aspx?lang=en).
2.  Locate the drivers for your NVIDIA products, and click **Search**. The following table provides relevant metrics.

    |Item|gn4|gn5|gn5i|gn6v|gn6i|
    |:---|:--|:--|:---|:---|----|
    |Product type|Tesla|Tesla|Tesla|Tesla|Tesla|
    |Product series|M-Class|P-Series|P-Series|V-Series|T-Series|
    |Product|M40|Tesla P100|Tesla P4|Tesla V100|Tesla T4|
    |Operating system \(OS\)|Select a release according to the image of your instance. **Note:** 

    -   If your OS is not in the drop-down list, click **Select All Operating Systems** at the bottom of the list.
    -   For Debian, select **Linux 64-bit**.
 ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9632/15622112685114_en-US.png)

|

3.  Confirm the information is correct, then click **Download**.

## Install the GPU driver for a Linux instance {#section_esm_dc1_4gb .section}

To install the GPU driver, follow these steps:

1.  Download and install the kernel-devel and kernel-header packages based on your kernel version.
2.  Run the sudo rpm -qa | grep $\(uname -r\) command to verify that the kernel-devel and kernel-header packages are successfully installed.

    For example, if you are using CentOS 7.3, the installation is successful if the following information is displayed.

    ``` {#codeblock_zo4_b15_ifb}
    kernel-3.10.0-514.26.2.el7.x86_64
    kernel-headers-3.10.0-514.26.2.el7.x86_64
    kernel-tools-libs-3.10.0-514.26.2.el7.x86_64
    python-perf-3.10.0-514.26.2.el7.x86_64
    kernel-tools-3.10.0-514.26.2.el7.x86_64
    ```

3.  Install the GPU driver according to the description in the **ADDITIONAL INFORMATION** area of the GPU download page.

    The following figure uses Linux 64-bit Ubuntu 14.04 for example.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9632/15622112695117_en-US.png)


**Note:** 

-   The preceding operations do not apply to a vgn5i instance. For information about how to install a GRID driver on a vgn5i Linux instance, see [Install an NVIDIA GRID driver on a vgn5i instance \(Linux\)](reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Install an NVIDIA GRID driver on a vgn5i instance (Linux).md#).
-   The version of kernel-devel and kernel-header must match your kernel version. Otherwise, driver compilation errors will occur during driver rpm installation. You can run rpm –qa | grep kernel in your instance to check version consistency before installing the driver.

## Install the GPU driver for a Windows instance {#section_o2j_hrs_qgb .section}

Double-click the executable file to install the driver as instructed.

**Note:** 

-   The preceding operation does not apply to a vgn5i instance. For information about how to install a GRID driver on a vgn5i Windows instance, see [Install an NVIDIA GRID driver on a vgn5i instance \(Windows\)](reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Install an NVIDIA GRID driver on a vgn5i instance (Windows).md#).
-   For Windows instances, the Windows RDP protocol does not support DirectX or OpenGL after the GPU driver is successfully installed. In this case, you need to install the VNC service and client or other protocols \(for example, PCoIP, and XenDeskop HDX 3D\).

