# Share images {#concept_e1j_jgm_xdb .concept}

After creating a custom image, you can share it with other Alibaba Cloud users. Shared images help new users adapt to ECS faster as they can quickly create ECS instances and set up business environments based on your custom images. Moreover, shared images do not consume the image quota of the account from which an image is shared.

## Attention {#section_v3m_rgm_xdb .section}

You can only share custom images you have created, not custom images created and shared by other users. Each custom image can be shared with up to 50 users within the same Alibaba Cloud region. That is, an image cannot be shared across regions.

Before sharing an image, make sure that all sensitive data and files have been deleted from the image.

**Note:** The integrity or security of shared images is not guaranteed. Make sure that you use only images shared by trusted accounts before using shared images. Besides, you shall bear the risk on your own. After you create an instance based on a shared image, be sure to [connect the instance](reseller.en-US/User Guide/Connect to instances/Overview.md#) to check the integrity and security of the image.

**Sharing image restrictions**

If your custom image has been shared with other accounts, you must remove all the sharing relationships for that image before you can delete the image. After deleting a shared custom image:

-   Users who are using the shared image will no longer be able to find the image through the ECS console or ECS API, nor can they use the image to create ECS instances or replace system disks.
-   ECS instances that are created from the shared image cannot re-initialize their system disks.

## Share an image {#section_g5c_dgn_j2b .section}

To share an image in the ECS console, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Select the target region.
3.  In the left-side navigation pane, choose **Snapshots and Images** \> **Images**.
4.  Select the target **Custom Image** the, in the **Actions** column, click **Share Image**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9700/15483148516790_en-US.png)

5.  In the pop-up dialog box, select **Alibaba Cloud Account ID** in the **Account Type** drop-down list. Then, enter the account ID that you want to share the image with in the **Account** box. For more information, see [Appendix:How to get the account ID?](#).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9700/15483148516801_en-US.png)

    **Note:** If you want to stop sharing the image with an account, click **Unshare** next to the account. After you cancel the sharing, that account will be unable to query and use the image. This means that i that account has already created an instance by using this shared image, the instance will be unable to [re-initialize the system disk](reseller.en-US/User Guide/Cloud disks/Reinitialize a cloud disk.md#).

6.  \(Optional\) For the accounts with whom you share an image, these account can view the shared image in **Snapshots and Images** \> **Images** \> **Share Image** in the same region in the ECS console.

You can also use the ECS APIs [ModifyImageSharePermission](reseller.en-US/API Reference/Images/ModifyImageSharePermission.md#) and [DescribeImageSharePermission](reseller.en-US/API Reference/Images/DescribeImageSharePermission.md#) to share an image.

## Next steps {#section_d22_5hm_xdb .section}

After an image is shared with other users, they can use it to create one or more instances.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Create one or more instances by referring to [Step 2. Create an instance](../../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#)Create an instance in *Quick Start*. Note that you should select **Shared Image** during the procedure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9700/15483148516802_en-US.png)


They can also use the shared image to [Replace the system disk \(non-public image\)](reseller.en-US/User Guide/Cloud disks/Replace the system disk (non-public image).md#) for instances.

## Appendix: How to get the account ID? {#HowToFindAccountId .section}

To find your account ID, follow these steps:

1.  Log on to the ECS console.
2.  Hover your mouse over your avatar and then click **Security Settings** from the account menu.
3.  On the page that appears, the account ID is displayed at the right as follows.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9700/15483148516803_en-US.png)


