# Create an instance by using a custom image {#task_w5v_sgv_xdb .task}

This topic describes how to create an instance by using a custom image. If you want to create an ECS instance that has the same operating system, software applications, and data as an existing instance, you can create a custom image and use it to create the new ECS instance. This method improves the deployment efficiency.

-   If the image and the instance are in the same region, create a custom image by using one of the following methods:
    -   [Import an image](reseller.en-US/Images/Custom image/Import images/Notes for importing images.md#)
    -   [Create a custom image by using an instance](../reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#)
    -   [Create a custom image by using a snapshot](../reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#)
-   If the custom image and the instance are in different regions, copy the custom image to the target region. For more information, see [Copy custom images](../reseller.en-US/Images/Custom image/Copy custom images.md#).
-   If the image to be used is owned by another account, it must be shared with you first. For more information, see [Share custom images](../reseller.en-US/Images/Custom image/Share custom images.md#).

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  In the upper-right corner of the Instances page, click **Create Instance**.
4.  Follow the steps when you [create an instance by using the wizard](reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#). When creating an ECS instance, note the following: 
    -   Region: Select the region where the image is located.
    -   Image: Select **Custom Image** or **Shared Image**, and then select an image from the drop-down list.

        **Note:** If the selected custom image contains more than one data disk snapshot, an equal number of cloud disks are automatically created to function as data disks. By default, the size of each data disk is equal to that of the source snapshot. You can only increase the size of a data disk.

5.  Confirm the order.

