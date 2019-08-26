# Create a ga1 instance {#concept_zq2_z3v_xdb .concept}

## Image description {#section_rmr_2jv_xdb .section}

GPU visualization computing ga1 instances use the AMD S7150 series GPU. Alibaba Cloud and AMD work together to optimize GPU drivers, so you can select the following images with preinstalled drivers from **Image Marketplace**:

-   Ubuntu16.04 with AMD GPU driver preinstalled
-   Windows Server 2016 English version with AMD GPU driver preinstalled
-   Ubuntu16.04 with AMD GPU driver and KDE preinstalled

## Procedure {#section_tmr_2jv_xdb .section}

You can create a ga1 instance by following the instructions provided in [creating an instance](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#). Use the following configurations when configuring an instance:

-   **Network**: Select **VPC**. The current GPU-rendered ga1 instances only support VPCs.
-   **Instance**: Select **Heterogeneous Computing** \> **GPU Visualization Compute** \> **GPU Rendering Type ga1**.
-   **Image**: Click **Marketplace Image**, and then click **Select from image market \(including operating system\)**. Enter GPU or AMD in the search box to search images.

    **Note:** It is recommended that you purchase or subscribe to these images because you can select images later for another instance directly from **Purchased Images** or **Subscribed Images**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9628/15510731585119_en-US.png)


## Precautions {#section_rk5_kjv_xdb .section}

-   The driver used for GPU visualization computing ga1 instances is optimized jointly by Alibaba Cloud and AMD. It is currently available only in images provided by Alibaba Cloud. No driver download link is provided, so you cannot install the driver on your own.
-   If the driver does not work due to uninstallation or deletion of GPU driver-related components, [change a system disk](reseller.en-US/Block storage/Cloud disks/Change the operating system/Replace the system disk (public image).md#) to restore the GPU functions.

    **Warning:** Changing a system disk may cause data loss.

-   If you use an unspecified image when creating a GPU visualization computing ga1 instance, the instance driver will not work. In this case, [change a system disk](reseller.en-US/Block storage/Cloud disks/Change the operating system/Replace the system disk (public image).md#) to use the image with an AMD GPU driver preinstalled.
-   For Windows, after the GPU driver takes effect, the **Connect** function cannot be used, and the Management Terminal page displays a black screen or the startup page. In this case, use another protocol to enter the OS, for example, Windows embedded Remote Desktop Protocol \(RDP\).
-   RDP does not support DirectX, OpenGL, or other related applications. You need to install the VNC service and client or use other protocols, such as XenDeskop HDX 3D and PCOIP.

