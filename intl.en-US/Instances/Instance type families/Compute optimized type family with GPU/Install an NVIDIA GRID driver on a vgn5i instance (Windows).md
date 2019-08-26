# Install an NVIDIA GRID driver on a vgn5i instance \(Windows\) {#task_264305 .task}

This topic describes how to install an NVIDIA GRID driver for instances running Windows Server 2016\(64-bit\) of the vgn5i instance type family. You must install an NVIDIA GRID driver if your GPU-equipped compute optimized instance requires Open Graphics Library \(OpenGL\). By default, the NVIDIA GRID license granted to NVIDIA GPUs is not activated, but you can activate the license by using a trial license to build a license server.

-   A vgn5i instance that can access the Internet is created. For more information, see [Create a compute optimized instance with GPU](reseller.en-US/Instances/Instance type families/Compute optimized type family with GPU/Create a compute optimized instance with GPU.md#).

    **Note:** We recommend that you select a **Public Image** when you create an instance.

-   The Remote Desktop Connection tool or a remote connection tool such as VNC Viewer is installed on your local machine.
-   An NVIDIA GRID license is obtained. If you need to obtain a license, you can:
    -   Visit the [NVIDIA official website](https://www.nvidia.com/object/nvidia-enterprise-account.html) and register an account to apply for a 90-day trial license.
    -   Obtain a temporary license from Alibaba Cloud technical support.
    -   Buy a license from NVIDIA.

1.  [Connect to the instance](Connect to the instanceEN-US_TP_9618.dita#concept_tmr_pgx_wdb).
2.  Download the NVIDIA GRID driver package. 
    -   If your instance is located in China \(Shenzhen\) Zone C or Zone D, run the following command to download [GRID 7.0 Guest](http://nvdia-driver-410.oss-cn-shenzhen.aliyuncs.com/Windows_Guest_Drivers.zip).
    -   If your instance is located in other regions or zones, run the following command to download GRID 8.0 Guest based on your Windows operating system:
        -   [GRID 8.0 for Windows 10 and Windows Server 2016](http://nvidia-418.oss-cn-shenzhen.aliyuncs.com/425.31_grid_win10_server2016_64bit_international.exe)
        -   [GRID 8.0 for Windows 8, Windows 7, Windows Server 2012R2, and Windows Server 2008R2](http://nvidia-418.oss-cn-shenzhen.aliyuncs.com/425.31_grid_win8_win7_server2012R2_server2008R2_64bit_international.exe)
3.  Install the NVIDIA GRID driver. 

    **Note:** For Windows operating systems, the Remote Desktop Protocol \(RDP\) may not support DirectX or OpenGL after the GPU driver is installed. In this case, you need to manually install the VNC server and client, or use other protocols that support the preceding applications, for example, PCoIP or XenDeskop HDX 3D.

4.  Restart the instance.
5.  Add a license server and activate the license. 
    1.  [Connect to the instance](Connect to the instanceEN-US_TP_9618.dita#concept_tmr_pgx_wdb).
    2.  Right-click on the desktop and choose **NVIDIA Control Panel**.
    3.  In the left-side navigation pane, choose **Licensing** \> **Manage License**.
    4.  Enter the IP address and port number of the license server, and click **Apply**. 

        If **Your system is licensed for GRID vGPU** is displayed, the license is activated.


