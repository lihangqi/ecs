# Delete custom images {#concept_azs_5bt_xdb .concept}

This topic describes how to delete a custom image. You can delete a custom image if you no longer need it. Deleting a custom image does not impact the instances created from the image or images copied from this image. Similarly, deleting image copies of a custom image has no impact on this custom image.

## Limits {#section_2kr_4ab_wu3 .section}

-   After a custom image is deleted, it cannot be used to create new ECS instances. However, ECS instances created from the deleted custom image can still run normally \(that is, continue to incur fees\), but these instances cannot reinitialize their cloud disks.
-   If the to be deleted custom image has been shared to other accounts, you must remove all permissions that allow shared access to the custom image before you can delete the image. After a shared image is deleted:
    -   Users who are using the shared image will no longer be able to find the image through the ECS console or ECS API, nor can they use the image to create ECS instances or replace cloud disks.
    -   ECS instances that are created from the shared image cannot reinitialize their cloud disks.

## Procedure {#section_vcq_cct_xdb .section}

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
2.  Select the target region.
3.  In the left-side navigation pane, choose **Snapshots and Images** \> **Custom Images**.
4.  On the **Images** tab page, select the image you want to delete. Note that the image type must be **Custom Images**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9710/155866638447850_en-US.png)

5.  Click **Delete Image**.
6.  In the displayed dialog box, select the deletion method.
    -   **Delete**: Delete a custom image by following the general procedures.
    -   **Force Delete**: Forcibly delete a customer image. Select this option if you have created ECS instances by using this image.

        **Note:** After a custom image is forcibly deleted, instances created by using this image cannot [reinitialize their cloud disks](reinitialize their cloud disks../DNA0011894323/EN-US_TP_9679.dita#concept_stg_xd3_ydb).

7.  Click **OK**.

You can also call [DeleteImage](../../../../intl.en-US/API Reference/Images/Deleteimage.md#) to delete a custom image.

