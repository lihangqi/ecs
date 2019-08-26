# Create an instance from a custom Image {#task_w5v_sgv_xdb .task}

If you want to run an ECS instance on Alibaba Cloud that runs an operating system, software applications, and data on an ECS instance, a virtual machine, or a cloud server, you can create a custom image and use it to create an ECS instance. This method improves the deployment efficiency.

-   If the image and the instance are in the same region, create a custom image by using one the following methods:
    -   [Importing an image](intl.en-US/User Guide/Images/Import images/Notes for importing custom images.md#)
    -   [Create a custom image by using an instance](intl.en-US/User Guide/Images/Create custom image/Create a custom image by using an instance.md#)
    -   [Create a custom mirror using a snapshot](intl.en-US/User Guide/Images/Create custom image/Create a custom mirror using a snapshot.md#)
-   If the custom image and the instance are in different regions, copy the custom image to the target region. For more information, see [Copy custom images](intl.en-US/User Guide/Images/Copy custom images.md#).
-   If the image to be used is not owned by another account, it must be shared with you. For more information, see [Share images](intl.en-US/User Guide/Images/Share images.md#).

1.   Log on to the [ECS console](https://ecs.console.aliyun.com/#/home). 
2.   In the left-side navigation pane, click **Instances**. 
3.   In the upper-right corner of the Instance List page, click **Create Instance**. 
4.   On the purchase page, follow the steps mentioned in [Create an ECS instance](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#). However, before doing so, consider the following: 
    -   Region: Select the region where the image is located.
    -   Image: Select **Custom Image** or **Shared Image**, and then select an image from the drop-down list.

        **Note:** If the selected custom image contains more than one data disk snapshot, an equal number of cloud disks are automatically created to work as data disks. By default, the size of each data disk is equal to that of the source snapshot. You are only allowed to increase the size of a data disk and you cannot decrease it.

5.   Confirm the order. 

