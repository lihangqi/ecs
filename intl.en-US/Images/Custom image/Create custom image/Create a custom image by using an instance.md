# Create a custom image by using an instance {#concept_ech_5bm_xdb .concept}

This topic describes how to create a custom image by using an instance. After creating an instance, you can customize the instance according to your service needs and create a custom image for it. New instances created from the custom image inherit all the customizations you have made for the original instance.

During custom image creation, snapshots are automatically created for all disks of the instance, including the system disk and data disks. All the created snapshots compose a new custom image. The following figure details this process.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9697/15661824734599_en-US.png)

The instance and the custom image that is created from this instance must belong to the same region. For example, if the instance is located in China East 1, the custom image must also be located in China East 1. If you need to use the image in another region, you must first copy the image to that region. For more information, see [Copy custom images](reseller.en-US/Images/Custom image/Copy custom images.md#).

If your instance expired or is released, you can also use the system disk snapshots of the instance to create a custom image, and then use this image to create a new instance to retrieve data in the original instance. For more information, see [Create a custom image by using a snapshot](reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#).

## Considerations {#section_yw3_zbm_xdb .section}

-   Make sure you have deleted all confidential data in the ECS instance before creating a custom image to guarantee data security.
-   You can create a custom image without stopping the instance. During creation, do not change the status of the instance. Specifically, do not stop, start, or restart the instance.
-   The time required for creating a custom image depends on the disk size of the instance.
-   If your custom image contains snapshots of data disks, new data disks are created based on the snapshots. If you create a data disk along with an ECS instance, data on the new data disk duplicates the data disk snapshot according to the mount device.

## Precautions for Linux instances {#section_pha_va2_15j .section}

Before creating a custom image using a Linux instance, follow these instructions:

-   Do not load data disk information to the /etc/fstab directory. Otherwise, instances created from the custom image cannot be started.
-   We strongly recommended that you umount all the file systems mounted on the Linux instance before creating a custom image. Otherwise, instances created from the custom image may not be started or used.
-   Do not upgrade the kernel or operating system unless other required.
-   Do not adjust system disk partitions. Currently, the system disk supports only one root partition.
-   Ensure that the system disk has available space.
-   Do not modify key system files such as /sbin, /bin, and /lib.
-   Do not modify the default login username `root`.

## Procedure {#section_ojf_2cm_xdb .section}

1.  Find the target instance.
2.  In the **Actions** column, choose **More** \> **Disk and Image** \> **Create Custom Image**.
3.  In the displayed dialog box, enter a name and description for the image.
4.  Click **Create**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9697/15661824744601_en-US.png)


The image is available after all snapshots of all disks have been created.

## What to do next {#section_5xb_2cw_pjd .section}

[Create an instance by using the custom image](../DNECS19100341/EN-US_TP_9627.dita#task_w5v_sgv_xdb).

