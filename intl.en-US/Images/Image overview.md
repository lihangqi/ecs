# Image overview {#concept_qql_3zb_wdb .concept}

An ECS image stores information that you need for creating an ECS instance. You must select an image when you create an ECS instance. An image works as a copy that stores data from one or more disks. An ECS image may store data from a system disk or from both system and data disks.

## Image types {#section_nyg_r5w_ydb .section}

ECS images are classified into the following types based on their sources. Fees are charged for ECS images. We recommend that you read and understand the pricing details of ECS before you use ECS images. For more information, see [Billing overview](../../../../reseller.en-US/Pricing/Billing overview.md#).

|Type|Description|Price|
|:---|:----------|:----|
|Public image|Public images are licensed by Alibaba Cloud, which are highly secure and stable. Public images include Windows Server system images and mainstream Linux system images. For more information, see [Public image overview](reseller.en-US/Images/Public image/Public image overview.md#).| Only Windows Server and Red Hat Enterprise Linux public images are charged. Check the actual fees when you use them to create instances. The Windows Server and Red Hat Enterprise Linux public images are licensed and maintained by Microsoft and Red Hat, respectively.

-   Red Hat Enterprise Linux: Fees are calculated based on the instance specification.
-   Windows Server: Fees are calculated based on the instance specification.

 Other public images are free of charge.

 |
|Custom image|Custom images are created from instances or snapshots, or imported from your local device. Only the creator of a custom image can use, share, copy, and delete the image. For more information, see [Lifecycle of a custom image](#section_custom_image).| Custom image fees are charged in the following situations:

-   Daily-use fees. The daily-use fees are equal to the fees incurred by the snapshot where the custom image is created from. Snapshots are charged based on the storage space usage.
-   Instance creation fees. When you use a custom image to create an instance, fees are charged as follows:
    -   If the custom image is created based on an Alibaba Cloud Marketplace image, the custom image fees are equal to the total amount of fees incurred by the Alibaba Cloud Marketplace image and the corresponding snapshot.
    -   If the custom image is created based on a free image, the custom image fees are equal to the fees of the corresponding snapshot.

For more information, see [Billing overview](../../../../reseller.en-US/Pricing/Billing overview.md#) and [Image FAQ](reseller.en-US/Images/FAQ/Image FAQ.md#ul_xjb_nty_dhb).

 |
|Shared image|Shared images are images shared to you by other Alibaba Cloud accounts. For more information, see [Share images](reseller.en-US/Images/Custom image/Share custom images.md#).|If a shared image is provided by Alibaba Cloud Marketplace, the shared image is billed according to the pricing standards of the independent software vendor \(ISV\).|
|Alibaba Cloud Marketplace image| Alibaba Cloud Marketplace images are classified into the following types based on the ISV.

-   Images provided by Alibaba Cloud accounts
-   Images provided by ISVs and licensed by Alibaba Cloud Marketplace

An Alibaba Cloud Marketplace image contains an operating system and pre-installed software. The operating system and pre-installed software are tested and verified by the ISV and Alibaba Cloud to ensure that the images are safe to use. For more information, see [Marketplace images](reseller.en-US/Images/Marketplace images.md#).

 |Alibaba Cloud Marketplace images are billed according to the pricing standards of the ISV.|

## Lifecycle of a custom image {#section_custom_image .section}

After you create or import a custom image, the image is in the **Available** state. You can then use the image to create an ECS instance, share the image to another Alibaba Cloud account, or copy the image to another region. You can also delete images that you no longer need. The following figure shows the lifecycle of a custom image.

![Lifecycle of a custom image](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9572/156687662734490_en-US.png)

## Create a custom image {#section_ybx_jv3_dhb .section}

After you create an ECS instance by using an existing image, you can configure the instance as needed. For example, you can install software and deploy projects on the instance, and then create a custom image for the instance. For more information, see [Create a custom image by using an instance](reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#). Instances created from the custom image contain all the configuration items that you have defined. For more information, see [Create an instance by using a custom image](../../../../reseller.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).

You can create a custom image by using the snapshot of the system disk or both the system and data disks. For more information, see [Create a custom image by using a snapshot](reseller.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#).

You can also import a custom image from a local device. For more information, see [Import custom images](reseller.en-US/Images/Custom image/Import images/Import custom images.md#).

## Share and copy a custom image {#section_rkp_21j_dhb .section}

Each image belongs to a region. For example, if you create a custom image in the China \(Beijing\) region, you can use the image to create ECS instances in this region only.

-   When you share the image with another Alibaba Cloud account, this account can use the image in the China \(Beijing\) region only. To share the image to an Alibaba Cloud account who needs to use the image in a different region, copy the image to the target region, and then share the image to the target Alibaba Cloud account. For more information, see [Share images](reseller.en-US/Images/Custom image/Share custom images.md#).
-   If you need to use the image in another region, copy the image to that region. The image copy is signed a unique UID. It is independent of the original image. For more information, see [Copy custom images](reseller.en-US/Images/Custom image/Copy custom images.md#).

## Change images for an ECS instance {#section_xvn_m3j_dhb .section}

After you create an ECS instance, you can change its operating system by changing the image of the system disk.

-   You can replace the image of the system disk with a public image. For more information, see [Replace the system disk by using a public image](../../../../reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk by using a public image.md#).
-   You can also replace the image of the system disk with a non-public image, for example, a custom, shared, or Alibaba Cloud Marketplace image. For more information, see [Replace the system disk \(non-public image\)](../../../../reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

## Delete a custom image {#section_mh5_rkj_dhb .section}

You can delete customs images that you no longer need. After a custom image is deleted, you can no longer use it to created ECS instances. You cannot [Reinitialize a cloud disk](../../../../reseller.en-US/Block Storage/Block storage/Reinitialize a cloud disk/Reinitialize a cloud disk.md#) of an ECS instance that is created from the image.

A custom image consists of snapshots of disks that are attached to an ECS instance. The delete operation does not delete snapshots contained in the image. To delete the snapshots, navigate to the Snapshots page and delete the target snapshots. For more information, see [Delete custom images](reseller.en-US/Images/Custom image/Delete custom images.md#).

## API operations {#section_u2t_hvw_ydb .section}

You can also perform API operations to manage an image. For more information, see [API overview](../../../../reseller.en-US/API Reference/API overview.md#section_image_t2h_vdb).

