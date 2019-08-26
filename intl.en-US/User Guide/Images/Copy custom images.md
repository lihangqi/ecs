# Copy custom images {#concept_a3m_5dm_xdb .concept}

Copying an image is a process in which a custom image is copied from one region to another region. Copying images across regions allows you to deploy a backup image system, or an identical application environment, in different regions. Copying images is allowed among all the regions of Alibaba Cloud. When a request of copying a custom image is initiated, ECS copies the snapshot that the custom image is created from the source region to the target region, and then creates a custom image from the copied snapshot in the target region. The speed of the process of copying the snapshot between regions depends on the network status. Moreover, Alibaba Cloud supports processing concurrent requests of copying images and your request maybe in a long queue. Therefore, it may take long time to complete the copying images operation.

## Precautions {#section_wgf_n2m_xdb .section}

ECS copies the snapshot that the custom image is created from the source region to the target region, and then creates a custom image from the copied snapshot in the target region. Therefore, you may be charged for:

-   Data transferring  between regions. Currently, there is no charge for this part of the flow, and the specific charge time is subject to the official website announcement.
-   The copied snapshot occupies the snapshot capacity.

## Procedures {#section_sv3_x2m_xdb .section}

The steps for copying a mirror on the Administration Console are as follows:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
2.  Select a region.
3.  In the left-side navigation pane, choose  **Snapshots & Images** \> **Images**.
4.  Select the custom image you want to copy, and in the **Actions** column, click  **Copy Image**.

    **Note:** 

    If your custom image is larger than 200 GB, when you click **Copy Image**, you are directed to open a ticket to complete copying the image.

5.  In the Copy Image dialog box, the ID of the selected image is displayed, and you have to complete the configurations:
    1.  Select the target region. Currently, copying images is only allowed between regions in mainland China.
    2.  **Custom Image** and **Custom Image Description**: Specify a name for the image to be displayed in the target region, and give a brief description of the image to ease future management.
    3.  Click **OK**.
6.  Click the target region and check the progress. When 100% progress is displayed, the image is copied successfully.

    **Note:** 

    When the progress is not 100% and the status of the image is **Creating**, you can click **Cancel Copy** to cancel the copying process. After the process is canceled, the image information is removed from the target region.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9699/15356807434607_en-US.png)


## Next step {#section_kmp_xfm_xdb .section}

After the copied image is ready, it is in the **Available** status, you can use the custom image to [Step 2. Create an instance](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#)create an ECS instance or [Change the system disk \(custom image\)](intl.en-US/User Guide/Cloud disks/Change the system disk (custom image).md#)change a system disk.

In the [ECS console](https://ecs.console.aliyun.com/#/home), check the snapshot for creating the custom image in the **Snapshot**.

## FAQ {#section_alb_2gm_xdb .section}

[FAQs about copying images](https://www.alibabacloud.com/help/zh/faq-detail/40569.htm?spm=a2c63.q38357.a3.5.218e437aDm1XZR)

