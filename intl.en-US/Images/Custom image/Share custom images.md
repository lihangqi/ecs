# Share custom images {#concept_e1j_jgm_xdb .concept}

This topic describes how to share custom images. After you share a custom image with an Alibaba Cloud account, this account has permission to create an ECS instance by using the shared image.

## Background information {#section_a01_oyj_bdc .section}

You are not billed for sharing a custom image with an Alibaba Cloud account or when the user of this account uses the shared image to create an ECS instance. Additionally, the shared image is not counted in the image quota assigned to the account. Only a user who creates an ECS instance from the shared custom image is charged.

**Note:** For information about the billing of shared images, see [Images](reseller.en-US/Images/Image overview.md#table_hwf_rpj_dhb).

## Limits {#section_brs_2fu_qa1 .section}

Before you share a custom image with an Alibaba Cloud account, note the following limits:

**Note:** The use of a shared custom image is the responsibility of the user. We recommend that you use shared custom images only from trusted sources. Alibaba Cloud does not bear any risks associated with the sharing of custom images.

-   You can share only the custom images created under your account. You cannot share custom images that were created and shared by other accounts.
-   We recommend that you first delete all sensitive data and files from the custom image to be shared to maintain account and data security.
-   Each custom image can be shared with up to 50 accounts.
-   Custom images cannot be shared across regions. If you want to share a custom image with an account that requires the shared image to be used in a different region, you must copy this image to the region first. For more information, see [Copy images](reseller.en-US/Images/Custom image/Copy custom images.md#).

## Procedure {#section_hxp_u9b_thw .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.
3.  In the top navigation bar, select a region.
4.  Select the target custom image. In the **Actions** column, choose **More** \> **Shared Image**.
5.  Select **Alibaba Cloud Account ID** from the **Account Type** drop-down list, enter the target account ID in the **Account** field, and click **Shared Image**.

    For information about how to obtain the ID of an account, see [Appendix: How to get the account ID](#title_zr9_8fb_ez6).

    ![share_image_dialogbox](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9700/15661861166801_en-US.png)

    After you share a custom image with an account, the account can view this shared image by choosing **Instances & Images** \> **Images** \> **Shared Images** in the same region in the ECS console.


You can also call the [ModifyImageSharePermission](../reseller.en-US/API Reference/Images/ModifyImageSharePermission.md#) and [DescribeImageSharePermission](../reseller.en-US/API Reference/Images/DescribeImageSharePermission.md#) API actions to share a custom image.

## What to do next {#section_ogp_isn_r7i .section}

If you want to delete a shared image, you must first stop sharing this image with all other Alibaba Cloud accounts. After you delete a shared image, the users of the accounts with which you previously shared this image cannot:

-   Query information of this image.
-   Use this image to create ECS instances or replace system disks.
-   Reinitialize the system disks for the ECS instances that were created by using this image. For information about how to reinitialize a disk, see [Reinitialize a cloud disk](reseller.en-US/Block Storage/Block storage/Reinitialize a cloud disk/Reinitialize a cloud disk.md#).

## Appendix: Get the ID of an account {#section_qz0_ggu_63l .section}

To find the ID of an account, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Hover your pointer over your avatar, for example, **example@aliyun.com**, and then choose **Security Settings** from the account menu.
3.  On the displayed page, find the account ID.

    ![Security Settings](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9700/15661861176803_en-US.png)


