# Manage custom images {#concept_xmy_cbt_xdb .concept}

You can modify the name and description of your custom images to help you organize and identify them, and you can delete custom images that you no longer require

## Modify the name and description of a custom image {#section_tdr_l33_m2b .section}

To modify the name and description of a custom image, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
2.  In the left-side navigation pane, select **Snapshots and Images** \> **Images**.
3.  Select the target region.
4.  Find the custom image to be edited and then click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9709/15429848077167_en-US.png) icon..
5.  Enter a name for the custom image.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9709/15429848077166_en-US.png)

6.  In the Actions column, click **Modify Description** and then, in the dialog box, enter a **Custom Image Description**.
7.  Click **Save**.

Alternatively, you can modify the name and description of a custom image by calling the ECS API [ModifyImageAttribute](../../../../intl.en-US/API Reference/Images/ModifyImageAttribute.md#).

## Delete custom images {#section_w3n_c43_m2b .section}

To delete one or more custom images, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
2.  In the left-side navigation pane, select **Snapshots and Images** \> **Images**.
3.  Select the target region.
4.  Select one or more custom images that you want to delete, and then click **Delete**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9709/15429848077168_en-US.png)

5.  In the dialog box that appears, select the required method for deleting the custom images:

    -   **Delete**: The custom images are deleted normally.
    -   **Force Delete**: The custom images are deleted forcibly. Check **I confirm to forcibly Delete the selected instances**.

        **Note:** After you forcibly delete the custom images, [cloud disk reinitialization](intl.en-US/User Guide/Cloud disks/Reinitialize a cloud disk.md#) of the instances that you have created from the images cannot be performed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9709/15429848077169_en-US.png)

6.  Click **OK**.

Alternatively, you can delete custom images by calling the ECS API [DeleteImage](../../../../intl.en-US/API Reference/Images/Deleteimage.md#).

