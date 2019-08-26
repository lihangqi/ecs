# Create a custom image by using an instance {#concept_ech_5bm_xdb .concept}

You can create a custom image based on an ECS instance. That is, you can fully copy all its disks and pack the data into an image.

During this process, snapshots are automatically created for all disks of the instance, including the system disk and data disks. All the created snapshots compose a new custom image. The following figure details this process.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9697/15458098094599_en-US.png)

For information about creating an image from a snapshot, see [create a custom image by using a snapshot](intl.en-US/User Guide/Images/Create custom image/Create a custom image by using a snapshot.md#).

## Considerations {#section_yw3_zbm_xdb .section}

-   Make sure you have deleted all confidential data in the ECS instance before creating a custom image to guarantee data security.
-   During creation, do not change the status of the instance. Specifically, do not stop, start, or restart the instance.
-   If your custom image contains data disks, new data disks along with the ECS instance are created together. The data on the data disk duplicates the data disk snapshot in your custom image according to the mount device.
-   You can export custom images that contain data disks.
-   You cannot use a custom image which contains data disks to replace the system disk.

## Procedure {#section_ojf_2cm_xdb .section}

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
2.  Select the target region.
3.  In the left-side navigation pane, click **Instances**.
4.  Find the target instance and click **More** \> **Disk and Image** \> **Create Custom Image**.
5.  Enter a name and description for the image.
6.  Click **Create**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9697/15458098094601_en-US.png)


The image is available after all snapshots of all disks have been created.

## Additional operation {#section_rwd_lcm_xdb .section}

See [create a custom image by using a snapshot](intl.en-US/User Guide/Instances/Create an instance/Create an instance from a custom image.md#).

