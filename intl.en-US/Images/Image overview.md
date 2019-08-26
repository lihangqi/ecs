# Image overview {#concept_qql_3zb_wdb .concept}

This topic provides an overview of the different types of ECS images provided by Alibaba Cloud, including their types and lifecycle. It also describes the common image operations. An image works as a file copy that includes all the data from a separate system disk or from the system disk and data disks of an ECS instance.

## Type of images {#section_nyg_r5w_ydb .section}

ECS images are classified into public images, custom images, shared images, and Marketplace images. We recommend that you maintain a sufficient balance in the linked credit card or PayPal account to complete the payment or preauthorization. For more information, see [Pricing overview](../intl.en-US/Pricing/Pricing overview.md#). 

|Image type|Description|Billing|
|:---------|:----------|:------|
|Public image|Public images are fully licensed images that are provided by Alibaba Cloud to ensure a stable, secure operating environment. They can run in all Windows Server and leading Linux operating systems. For more information, see [Public images](intl.en-US/Images/Public image/Public images.md#).| Only public images that run in the Red Hat Enterprise Linux and Windows Server operating systems are charged fees because they are licensed by Red Hat and Microsoft, respectively. All other public images are provided free of charge. The details of the fee for Red Hat Enterprise Linux and Windows Server public images are as follows:

-   Red Hat Enterprise Linux: Fees vary depending on the instance type.
-   Windows Server: If the public image is used in ECS instances in regions of Mainland China, the public image is provided free of charge. If the public image is used in ECS instances in other regions, a fee is charged.

 The public images that run in other operating systems than Windows Server and Red Hat Enterprise Linux are provided free of charge.

 |
|Custom image|Custom images are created from ECS instances or snapshots, or imported from your computer. A custom image can be used, shared, copied, and deleted only by the user who created it. For more information, see [Lifecycle of a custom image](#section_custom_image).| Custom images are billed according to the size of snapshots that are used to create a custom image:

-   The fee for maintaining an existing custom image is the same as the snapshot fee.
-   If you use a custom image to create an ECS instance, the image fee is charged as follows:
    -   If the custom image is created from a Marketplace image, the image fee consists of Marketplace image fee and snapshot fee.
    -   If the custom image is created from a free image, the image fee is the same as the snapshot fee.

For more information, see [Pricing overview](../intl.en-US/Pricing/Pricing overview.md#) and [Image commercialization FAQ](intl.en-US/Images/FAQ/Image FAQ.md#ul_xjb_nty_dhb).

 |
|Shared image|Images can be shared among Alibaba Cloud accounts. For more information, see [Share images](intl.en-US/Images/Custom image/Share custom images.md#).|When you use a shared Marketplace image, you are charged a fee according to the billing method specified by the ISV in the Alibaba Cloud Marketplace.|
|Marketplace image| Marketplace images are categorized into the following two types:

-   Marketplace images that are provided by Alibaba Cloud
-   Marketplace images that are provided by independent software vendors \(ISVs\) upon authorization of the Alibaba Cloud Marketplace

A Marketplace image contains an operating system and pre-installed software. The operating system and pre-installed software have been tested and verified by Alibaba Cloud to ensure that the image content is secure. For more information, see [Marketplace images](intl.en-US/Images/Marketplace images.md#).

 |A Marketplace image is charged according to the billing method specified by the specific ISV in the Cloud Marketplace.|

## Lifecycle of a custom image {#section_custom_image .section}

After you create or import a custom image, this image is the Available state. You can use this image to create an ECS instance, share it with another Alibaba Cloud account, copy it to another region, or delete it when you no longer need it. The following figure shows the lifecycle of a custom image.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9572/156531932634490_en-US.png)

## Create a custom image {#section_ybx_jv3_dhb .section}

After you create an ECS instance by using an existing custom image, you can configure the instance as needed. For example, you can install software and deploy projects in the instance. Additionally, you can create a custom image for the instance. For more information, see [Create a custom image by using an instance](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#).

**Note:** An ECS instance that is created by using this custom image contains all the configuration items that you have defined. For more information, see [Create an instance by using a custom image](../intl.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).

You can create a custom image by using a system disk or by using a system disk and data disks. For more information, see [Create a custom image by using a snapshot](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#).

You can also import a custom image from your computer. For more information, see [Import custom images](intl.en-US/Images/Custom image/Import images/Import custom images.md#).

## Share and copy a custom image {#section_rkp_21j_dhb .section}

Each image belongs to a region. For example, if you create a custom image in China North 2 \(Beijing\), you can use this image to create an ECS instance only in the region.

-   You can only share the image with a user who is located in the same region. To share the image with a user who is located in a different region, you need to copy the image to the region first. For more information, see [Share images](intl.en-US/Images/Custom image/Share custom images.md#).
-   If you want to use this image in a different region, you need to copy this image to the region. The image copy is independent and has a unique ID. For more information, see [Copy images](intl.en-US/Images/Custom image/Copy custom images.md#).

## Change the image for an ECS instance {#section_xvn_m3j_dhb .section}

After you create an ECS instance, you can change its image by replacing its system disk.

-   If you want to change the image to a public image, see [Replace the system disk by using a public image](../intl.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk by using a public image.md#).
-   If you want to change the image to a custom, Marketplace, or shared image, see [Replace the system disk \(non-public image\)](../intl.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

## Delete a custom image {#section_mh5_rkj_dhb .section}

You can delete a custom image when you no longer need it. After you delete a custom image, you cannot create an ECS instance by using this image or reinitialize the cloud disk for an ECS instance created by using this image. For more information, see [Reinitialize a cloud disk](../intl.en-US//Reinitialize a cloud disk.md#).

A custom image consists of the disks of an ECS instance. After you delete a custom image, the snapshots in it are not deleted. If you no longer need the snapshots, you can delete them from the snapshot list. For more information, see [Delete custom images](intl.en-US/Images/Custom image/Delete custom images.md#).

## APIs {#section_u2t_hvw_ydb .section}

You can call ECS API actions to operate an image. For more information, see [API overview](../intl.en-US/API Reference/API overview.md#section_image_t2h_vdb).

