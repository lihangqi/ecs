# Image FAQ {#concept_q1j_bty_dhb .concept}

-   Aliyun Linux 2 FAQ
    -   [What differences are there between Aliyun Linux 2 and Aliyun Linux?](#section_w6f_5bb_qr1)
    -   [How do I use Aliyun Linux 2 in Alibaba Cloud?](#section_98t_rct_ulf)
    -   [Am I charged for the use of Aliyun Linux 2 in Alibaba Cloud ECS?](#section_cuu_e0w_lig)
    -   [Which ECS instance types does Aliyun Linux 2 support?](#section_oab_cqd_mcz)
    -   [Does Aliyun Linux 2 support 32-bit applications and databases?](#section_ich_g5d_yex)
    -   [Does Aliyun Linux 2 provide a GUI desktop?](#section_1wi_oiy_xpw)
    -   [Can I view the source code of Aliyun Linux 2 components?](#section_nzi_uw7_gpv)
    -   [Is Aliyun Linux 2 backward-compatible with the current Aliyun Linux version?](#section_3pu_hh2_3bu)
    -   [Can I use Aliyun Linux 2 locally?](#section_03c_szd_12p)
    -   [Which third-party applications can run on Aliyun Linux 2?](#section_ojw_0q8_j00)
    -   [What are the advantages of Aliyun Linux 2 when compared with other Linux operating systems?](#section_ygx_9it_kif)
    -   [What data protection functions are included with Aliyun Linux 2?](#section_bsd_rg8_f7n)
    -   [Does Aliyun Linux 2 support data encryption?](#section_x42_zxc_g6q)
    -   [How do I grant permissions to manage Aliyun Linux 2?](#section_cy0_7v9_35z)
-   General issues
    -   [What is an image?](#section_hhl_prx_fhb)
    -   [What are the benefits of an image?](#section_owg_qrx_fhb)
    -   [Which server environments and application scenarios are supported by the current images?](#section_lfh_rrx_fhb)
    -   [Are the images safe?](#section_sdd_srx_fhb)
    -   [Can I change a selected image?](#section_ovb_trx_fhb)
    -   [What should I do if problems occur during the installation or use of an image?](#section_kl5_trx_fhb)
    -   [Does the system disk of an ECS instance support KMS encryption, and can I use KMS encryption through Terraform or Packer?](#section_iru_c7j_5dy)
-   Snapshot FAQ
    -   [What are the differences and relationships between snapshots and images?](#section_bmh_2xf_3ds)
    -   [How do I migrate the ECS snapshots under account A to account B?](#section_ed5_k10_dzu)
    -   [Cannot a data disk snapshot be used to create a custom image? So how do I migrate the data disk snapshots under account A to account B?](#section_lyx_6pb_932)
    -   [What should I do when the snapshot rollback fails due to deletion of the instance that is used to create the snapshot?](#section_5p6_ip2_7g0)
    -   [Can the system snapshot of an ECS instance be downloaded to a local computer?](#section_1ff_9s6_3i5)
    -   [Do the snapshots still exist after the corresponding instance is released?](#section_ocf_oay_z1e)
    -   [Why does it prompt me of "RequestId: xxx associated" when I want to delete a snapshot from the snapshot chain list in China North 2?](#section_72i_6dy_wdp)
    -   [I used to have an instance in China East 1 \(Hangzhou\), which was released upon expiration and whose data disks have snapshots. Can I roll back those snapshots in a newly purchased instance in the same region?](#section_c7y_3ij_f53)
-   Custom image FAQ
    -   [How do I view the usage of a data disk?](#section_hrq_fgx_fhb)
    -   [How do I unmount a disk table and delete its data?](#section_lzy_rgx_fhb)
    -   [How can I confirm that a data disk has been unmounted and a new custom image can be created?](#section_wdy_3ty_dhb)
    -   [Does a custom image still exist after the corresponding instance is released?](#section_qbd_ghx_fhb)
    -   [After an instance expires or releases its data, is the corresponding custom image affected? Are instances created from the custom image affected?](#section_zc5_shx_fhb)
    -   [Can I replace the operating system of an instance created with a custom image? Can the original custom image still be used after replacing the system?](#section_j1z_thx_fhb)
    -   [Can I use a custom image when I change the system disk and choose another operating system?](#section_b21_zhx_fhb)
    -   [Can I use a custom image to replace the system disk data of another ECS instance?](#section_cv1_g3x_fhb)
    -   [Is it possible to upgrade the CPU, memory, bandwidth, and hard disk of an ECS instance that is created with a custom image?](#section_y35_m3x_fhb)
    -   [Can I use a custom image across regions?](#section_twm_n3x_fhb)
    -   [Can a custom image of a Subscription instance be used to create a Pay-As-You-Go instance?](#section_t5m_cjx_fhb)
    -   [Why does the system disk auto-expansion fail in an instance created with a custom image? What can I do?](#section_oqc_u0t_5ri)
    -   [Why do I need to comment out mounted items when creating a custom image or ECS instance?](#section_uar_ern_zbt)
    -   [How do I configure and use the private Docker image registry?](#section_4wu_r5p_bi1)
-   Image copying FAQ
    -   [When do I need to copy a custom image?](#section_pbs_h4c_ghb)
    -   [Which images can be copied?](#section_j4j_n4c_ghb)
    -   [Which regions support copying custom images currently?](#section_jcb_44c_ghb)
    -   [How long does it take to copy a custom image?](#section_wzx_44c_ghb)
    -   [How am I charged when I copy a custom image?](#section_nbz_q4c_ghb)
    -   [What are the limitations of source and destination images during the copy process?](#section_inj_s4c_ghb)
    -   [How do I copy the images under my Alibaba Cloud account to other regions under other Alibaba Cloud accounts?](#section_kyv_54c_ghb)
    -   [Is the copy image operation subject to image capacity limitation?](#section_k14_x4c_ghb)
    -   [I copied a custom image to another region where it appears as Available, but when I used it to create an instance, it prompts "The specified image is disabled or deleted". Why?](#section_lxo_ujw_fm3)
    -   [How do I migrate data from the international station to China?](#section_oqq_9z9_t00)
-   Image sharing FAQ
    -   [How many images can be shared to me?](#section_xry_y4c_ghb)
    -   [How many users can each image be shared to?](#section_pwp_ypc_ghb)
    -   [Does using a shared image take up my image quota?](#section_agd_2qc_ghb)
    -   [Is there a geographical limitation when creating an instance by using a shared image?](#section_mls_2qc_ghb)
    -   [What are the risks of creating an instance with a shared image?](#section_p4w_lqc_ghb)
    -   [What are the risks if I share a custom image with other accounts?](#section_r4q_nqc_ghb)
    -   [Can I share an image from account A with account B?](#section_abm_4qc_ghb)
    -   [After I share an image with others, can I still create an instance by using that image?](#section_xny_pqc_ghb)
    -   [Can an image created from instance A in a China North region be shared with instance B in a China East region?](#section_b5i_fn9_i06)
-   Image exporting FAQ
    -   [Why is there no option to export an image?](#section_j80_1pu_tv2)
    -   [I want to export an image to my local computer for testing. What should I do?](#section_9dl_9cs_oba)
-   Image deleting FAQ
    -   [Can I delete a custom image after I used it to create an ECS instance?](#section_lvj_dht_8a4)
    -   [Can I delete a custom image from my account after I have shared it with another account?](#section_fqt_49s_s3v)
    -   [What are the impacts after I cancel the sharing of a custom image \(M\) with account A?](#section_qn6_1dm_1tn)
    -   [When I was deleting an image, it prompts that "the image cannot be deleted because the specified image ID is involved with existing instances". Why?](#section_qe9_38d_hvk)
-   Image replacement \(operating system\) FAQ
    -   [When I try to replace a system disk, can I replace the corresponding image by replacing the system disk if the selected image contains data disks?](#section_053_0tw_h6a)
    -   [I want to replace the operating system of my ECS instance with an existing image. What should I do?](#section_69i_52e_jfd)
    -   [Can an image created from an instance under account A be used to replace a disk under account B?](#section_oww_crp_0j9)
-   Image fee FAQ
    -   [When I am creating an instance with a custom image, why is the configuration cost higher than that of creating an instance with a public image?](#section_k04_yg7_uoa)
-   Image commercialization FAQ
    -   [How do I buy a Marketplace image?](#section_hxc_rqc_ghb)
    -   [How long can I use a purchased image?](#section_hqw_prc_ghb)
    -   [Is refunding available to the images on the Image Market?](#section_gzm_qrc_ghb)
    -   [After commercialization of the image market, are free images still available on the market?](#section_okl_src_ghb)
    -   [I bought an image on the image market in Hangzhou. Can I use it to create an ECS instance or replace a system disk in Beijing?](#section_ndz_src_ghb)
    -   [My ECS instance is created with an image on the image market. Do I need to make further payment when I upgrade or renew my ECS instance?](#section_jwc_fsx_fhb)
    -   [My ECS instance is created with an image on the image market. After my ECS instance is released, can I continue to use that image free of charge when I purchase an ECS instance?](#section_yqb_wrc_ghb)
    -   [I created an ECS instance with an image on the image market and then created a custom image from that instance. Do I need to pay for the image when I create an ECS instance by using this custom image?](#section_pnn_yrc_ghb)
    -   [If I buy an image from the image market and copy it to another region for ECS instance creation, do I need to pay for the image?](#section_bqm_zrc_ghb)
    -   [If I share a custom image from the image market to account B for ECS instance creation, does account B need to pay for the image?](#section_ymk_1sc_ghb)
    -   [Is a fee incurred if I replace a system disk by using an image on the image market or an image that originates from the image market?](#section_uj5_1sc_ghb)
    -   [My ECS instance is using an image on the image market. Is a fee incurred if I reset the system disk?](#section_nj4_bsc_ghb)
    -   [How do I call ECS APIs to create an ECS instance or replace a system disk by using an image on the image market or a custom or shared image that originates from the image market?](#section_xl1_csc_ghb)
    -   [If I do not buy an image that is on the image market or originates from the image market, will errors be reported when I call ECS APIs to use that image for ECS instance creation or system disk replacement?](#section_sxt_hsc_ghb)
    -   [I configured ECS to automatically create instances whose number ranges from 10 to 100. What should I do with images on the image market for this purpose?](#section_nfx_5sc_ghb)
    -   [Do images of the image market support bulk purchase?](#section_clp_ysc_ghb)
    -   [If an image on the image market is no longer available for sale \(such as jxsc000010 and jxsc000019\), what should I do to ensure the normal functioning of auto scaling settings?](#section_stt_zsc_ghb)
    -   [Can one product code support images of different regions?](#section_os3_btc_ghb)
    -   [I bought 100 images with the same product code. Can I use them in all regions?](#section_uzj_ctc_ghb)
    -   [After I select the "IO Optimized Instance" option, I cannot select images on the image market when purchasing an ECS instance. Why is that and how do I deal with it?](#section_tch_39p_cv5)
-   Image market prepaid images FAQ
    -   [What are Subscription and weekly paid images on the image market?](#section_zxy_n5c_ghb)
    -   [Which ECS instances can I use with a prepaid image?](#section_fts_45c_ghb)
    -   [How do I buy a prepaid image? Can I buy it separately?](#section_rfp_s5c_ghb)
    -   [How do I pay for prepaid images?](#section_xhj_w5c_ghb)
    -   [Can I use a prepaid image after it expires? How do I continue to use it?](#section_cc4_x5c_ghb)
    -   [After purchasing a prepaid image, can I request a refund if I no longer want to use it?](#section_gwb_z5c_ghb)
    -   [How is the fee settled when a refund is made?](#section_hvt_z5c_ghb)
    -   [Can a prepaid image be converted to a Pay-As-You-Go image?](#section_hpg_1vc_ghb)
    -   [Can I replace a prepaid image with another image and vice versa? How is the fee calculated?](#section_sqw_1vc_ghb)
    -   [Where can I view and manage the prepaid images I purchased?](#section_fmx_fvc_ghb)
    -   [Is there a fee for a custom image created with a prepaid image? How will such a custom image be affected if the relevant prepaid image expires?](#section_klq_gvc_ghb)
-   ECS instance and operating system FAQ
    -   [Why cannot some ECS instances choose the Windows operating system?](#section_ajg_qwc_ghb)
    -   [Is a fee incurred when an ECS instance uses a operating system?](#section_ttw_qwc_ghb)
    -   [Can I install or upgrade my operating system myself?](#section_zhs_twc_ghb)
    -   [Do the operating systems have a graphical interface?](#section_ulp_xwc_ghb)
    -   [How do I choose an operating system?](#section_wqy_zwc_ghb)
    -   [Do public images come with the FTP service?](#section_jtv_dxc_ghb)
    -   [Which SUSE versions does Alibaba Cloud support?](#section_mgc_fxc_ghb)
    -   [What services or support are provided by the SUSE operating systems?](#section_jpr_fxc_ghb)
    -   [After an ECS instance is released upon expiration, if an image is manually created for the instance, can I retrieve the data of the previous instance?](#section_uj1_il5_0xb)
    -   [I have an ECS instance now, and want to buy another ECS instance by using an image of the current ECS instance. What should I do?](#section_d2a_pl9_3vq)
    -   [I purchased a new ECS instance, how do I restore my shared image to this newly purchased ECS instance?](#section_54f_mg4_r2p)
    -   [The operating system of my instance is Windows Server 2008 R2 Enterprise Edition. It now prompts that the operating system is not genuine? What should I do?](#section_dcb_fs7_ljf)
    -   [I have multiple accounts on Alibaba Cloud, and I want to transfer one instance under account A to account B, or use an image to migrate the environment and applications to an instance under account B. What should I do?](#section_cvk_0gm_ods)
    -   [Can ECS instances in different VPCs communicate with each other?](#section_lqt_tci_xa6)
    -   [How to handle CentOS DNS resolution timeout?](#section_x8y_les_u5u)

## What differences are there between Aliyun Linux 2 and Aliyun Linux? {#section_w6f_5bb_qr1 .section}

Aliyun Linux 2 differs from Aliyun Linux in the following aspects:

-   Aliyun Linux 2 is optimized for containers to better support cloud-native applications.
-   Aliyun Linux 2 is equipped with an updated Linux kernel and updated user mode packages.

## How do I use Aliyun Linux 2 in Alibaba Cloud? {#section_98t_rct_ulf .section}

Alibaba Cloud provides an official public image for Aliyun Linux 2. You can select this image when you create an ECS instance.

## Am I charged for the use of Aliyun Linux 2 in Alibaba Cloud ECS? {#section_cuu_e0w_lig .section}

No, the Aliyun Linux 2 image is free to use. You are only charged for the usage of the corresponding ECS instance to which the image is applied.

## Which ECS instance types does Aliyun Linux 2 support? {#section_oab_cqd_mcz .section}

Aliyun Linux 2 supports most ECS instance types, including ECS Bare Metal Instance.

**Note:** Aliyun Linux 2 cannot be applied to instances that use the Xen virtual machine platform or the classic network, and will not be displayed as an image option for them.

## Does Aliyun Linux 2 support 32-bit applications and databases? {#section_ich_g5d_yex .section}

No. Currently, Aliyun Linux 2 does not support 32-bit applications or databases.

## Does Aliyun Linux 2 provide a GUI desktop? {#section_1wi_oiy_xpw .section}

No. Currently, Aliyun Linux 2 does not provide a GUI desktop.

## Can I view the source code of Aliyun Linux 2 components? {#section_nzi_uw7_gpv .section}

Yes. Aliyun Linux 2 complies with open source protocols. You can use the yumdownloader tool or visit official Alibaba Cloud download pages to download the source code package. You can also download the source code tree of the Aliyun Linux kernel from Github.

## Is Aliyun Linux 2 backward-compatible with the current Aliyun Linux version? {#section_3pu_hh2_3bu .section}

Yes. Aliyun Linux 2 is fully compatible with Aliyun Linux 17.01.

**Note:** If you use a kernel module that you compiled, you may need to re-compile it on Aliyun Linux 2 before you can use it.

## Can I use Aliyun Linux 2 locally? {#section_03c_szd_12p .section}

No. Currently, Aliyun Linux 2 only supports Alibaba Cloud ECS. Third-party virtualized platforms are not supported.

## Which third-party applications can run on Aliyun Linux 2? {#section_ojw_0q8_j00 .section}

Currently, Aliyun Linux 2 is binary-code compatible with CentOS 7.6.1810. Therefore, applications that can run on CentOS can also run on Aliyun Linux 2.

## What are the advantages of Aliyun Linux 2 when compared with other Linux operating systems? {#section_ygx_9it_kif .section}

Compared with CentOS and RHEL, Aliyun Linux 2 has the following advantages:

-   Updates are released at a faster pace. More advanced Linux kernels, user mode software, and toolkit are provided.
-   No configuration required, out-of-the-box functionality.
-   Zero run-time billing \(compared with RHEL\); provided with commercial support \(compared with CentOS\).

## What data protection functions are included with Aliyun Linux 2? {#section_bsd_rg8_f7n .section}

Aliyun Linux 2 is binary-code compatible with CentOS 7.6.1810 and RHEL 7.6, and is compliant with the RHEL safety specifications. Aliyun Linux 2 protects your data by using the following methods:

-   It uses industry standard vulnerability scanning and security test tools to conduct periodical security scanning.
-   It periodically accesses the CVE patch of CentOS 7 to fix OS security vulnerabilities.
-   It supports existing OS security solutions of Alibaba Cloud.
-   It uses the same mechanism as CentOS 7 to release user security alerts and patch updates.

## Does Aliyun Linux 2 support data encryption? {#section_x42_zxc_g6q .section}

Yes. Aliyun Linux 2 retains the data encryption toolkit of CentOS 7 to support data encryption implemented by CentOS 7 and KMS.

## How do I grant permissions to manage Aliyun Linux 2? {#section_cy0_7v9_35z .section}

The method to grant permissions to manage Aliyun Linux 2 is the same as that of Alibaba Cloud CentOS 7. This means that an administrator of CentOS 7 can use the same management commands to grant permissions of Aliyun Linux 2.

## What is an image? {#section_hhl_prx_fhb .section}

An image is a software configuration template that is pre-installed with an operating system, running environment \(such as PHP/.NET/JAVA/LAMP\), control panel, and website building system. By applying an image to your ECS instances, you can easily deploy the same running environment or software applications in your ECS instances.

## What are the benefits of an image? {#section_owg_qrx_fhb .section}

In the past, after you launched an ECS instance, you had to configure the environment and install the software yourself, which was painstaking and time consuming. Now, by deploying an image to your ECS instances with one click, you can have the same system environment or software in your ECS instances, quickly create a ready-to-use running environment, and easily build and manage a website.

## Which server environments and application scenarios are supported by the current images? {#section_lfh_rrx_fhb .section}

The image marketplace provides hundreds of high-quality third-party images, which not only fully support the deployment of PHP/.NET/JAVA/LAMP/Docker containers, but also meet the individual needs of website building, application development, and visualization management.

## Are the images safe? {#section_sdd_srx_fhb .section}

All the image providers have extensive experience in system maintenance and environment configuration. All images are based on Alibaba Cloud official operating systems that include Alibaba Cloud Security, and are subject to strict security auditing beforehand. Please feel free to use them.

## Can I change a selected image? {#section_ovb_trx_fhb .section}

Yes. In the ECS console, choose to replace the system disk, and then select the target image. Note that replacing an image will result in loss of system disk data. Please back up the data before confirming the replacement.

## What should I do if problems occur during the installation or use of an image? {#section_kl5_trx_fhb .section}

Check the service information on the purchase page, and then contact your image provider through online TradeManager, telephone, or email to fix your issues in time.

## Does the system disk of an ECS instance support KMS encryption, and can I use KMS encryption through Terraform or Packer? {#section_iru_c7j_5dy .section}

The system disk of an ECS instance supports KMS encryption by using the key that is automatically generated by KMS. After you select KMS encryption, ECS automatically creates a dedicated CMK in the region where KMS is used. For more information, see [ECS disk encryption](../../../../intl.en-US/Block Storage/Block storage/ECS disk encryption.md#).

Support for Terraform is available, while support BYOK encryption and Packer encryption is in development.

In Terraform, you can set the encrypted parameter to enable or disable KMS encryption. For more information, see [alicloud\_disks](https://www.terraform.io/docs/providers/alicloud/d/disks.html).

## What are the differences and relationships between snapshots and images? {#section_bmh_2xf_3ds .section}

**The differences between snapshots and images:**

-   Images can be used to create ECS instances directly, while snapshots cannot.
-   A snapshot can be a data backup of the system disk or data disk of an ECS instance, while an image must contain the system disk data of an ECS instance.
-   A snapshot can only be used for data recovery of the current ECS instance disk, while an image can be used to replace the system disk of any ECS instance or create a new ECS instance.
-   Snapshots cannot be used across regions. If you need to restore instance data in other regions, you can use a custom image. For more information, see [Copy custom images](intl.en-US/Images/Custom image/Copy custom images.md#).

-   The application scenarios are different. Here are a few scenarios for snapshots and custom images:

    Application scenarios of snapshots:

    -   Regular data backup. An automatic snapshot policy is applied to back up data according to the pre-set period, such as daily, weekly, or monthly.
    -   Temporary data backup, for example:
        -   Temporary system changes such as system update and application release. To prevent misoperations, manually create a snapshot to perform backup before performing changes.
        -   Create a snapshot to back up data before the system disk is expanded.
        -   Disk data migration. Create a snapshot of the target disk and use the snapshot as the underlying data for another disk.
    Application scenarios of custom images:

    -   Back up systems that do not change in the short term, such as applications and systems that have been released or updated.
    -   Create new ECS instances, such as deployment of applications in batch.
    -   System and data migration, such as migrating ECS instances from Classic networks to VPCs.
    -   Restore systems across regions and zones.

**The relationships between snapshots and images:**

When you create a custom image by using an instance, ECS creates a snapshot for each disk of the instance. That is, a custom image contains the snapshots of all the disks of an ECS instance. For more information, see [Create a custom image by using an instance](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#).

Custom images can also be created by using a system disk snapshot. For more information, see [Create a custom image by using a snapshot](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#).

## How do I migrate the ECS snapshots under account A to account B? {#section_ed5_k10_dzu .section}

Snapshots do not support migration. If needed, you can create an image from snapshots and share it with another account. For more information, see [Create a custom image by using a snapshot](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#) and [Share images](intl.en-US/Images/Custom image/Share custom images.md#).

## Cannot a data disk snapshot be used to create a custom image? So how do I migrate the data disk snapshots under account A to account B? {#section_lyx_6pb_932 .section}

Only a system disk snapshot can be used to create a custom image while a data disk snapshot cannot.

To migrate data disk snapshots under account A to account B, follow these steps:

1.  Create an image for the original instance of a data disk snapshot. For more information, see [Create a custom image by using an instance](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#).
2.  Share the image to account B. For more information, see [Share images](intl.en-US/Images/Custom image/Share custom images.md#).
3.  In account B, use the image to purchase a new Pay-As-You-Go instance. For more information, see [Create an instance by using a custom image](../../../../intl.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).
4.  Create a snapshot for the data disk of the newly purchased instance. For more information, see [Create a snapshot](../../../../intl.en-US/Snapshots/Use snapshots/Create a snapshot.md#).
5.  Release the newly purchased instance. For more information, see [Release an instance](../../../../intl.en-US/Instances/Manage instances/Release an instance.md#).

## What should I do when the snapshot rollback fails due to deletion of the instance that is used to create the snapshot? {#section_5p6_ip2_7g0 .section}

You can follow these steps:

1.  Create a custom image by using the snapshot. For more information, see [Create a custom image by using a snapshot](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#).
2.  Replace the system disk and select the custom image for the replacement. For more information, see [Replace the system disk \(non-public image\)](../../../../intl.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

## Can the system snapshot of an ECS instance be downloaded to a local computer? {#section_1ff_9s6_3i5 .section}

A snapshot cannot be downloaded to a local computer. You can create an image with a snapshot and then request to export the image. For more information, see [Create a custom image by using a snapshot](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using a snapshot.md#) and [Export custom images](intl.en-US/Images/Custom image/Export custom images.md#).

## Do the snapshots still exist after the corresponding instance is released? {#section_ocf_oay_z1e .section}

Manual snapshots are retained while automatic snapshots are cleared when the corresponding instance is released. For more information, see [Snapshot FAQ](../../../../intl.en-US/Snapshots/Snapshot FAQ.md#).

## Why does it prompt me of "RequestId: xxx associated" when I want to delete a snapshot from the snapshot chain list in China North 2? {#section_72i_6dy_wdp .section}

Your snapshot has been used to create a custom image. You need to delete the custom image before you can delete the snapshot.

## I used to have an instance in China East 1 \(Hangzhou\), which was released upon expiration and whose data disks have snapshots. Can I roll back those snapshots in a newly purchased instance in the same region? {#section_c7y_3ij_f53 .section}

Snapshot rollback is applicable only to the original instance. You can use the snapshot of the previous data disk to create a cloud disk and mount the cloud disk to the new instance. For more information, see [Create a cloud disk by using a snapshot](../../../../intl.en-US/Block Storage/Block storage/Create a cloud disk/Create a cloud disk by using a snapshot.md#) and [Attach a cloud disk](../../../../intl.en-US/Block Storage/Block storage/Attach a cloud disk.md#).

## How do I view the usage of a data disk? {#section_hrq_fgx_fhb .section}

You can run the df command to view the usage of a data disk and where the file system is mounted. For example: df –lh.

You can run the fdisk command to get the partition information of a data disk. For example: fdisk -l.

## How do I unmount a disk table and delete its data? {#section_lzy_rgx_fhb .section}

Assume /dev/hda5 is already mounted on /mnt/hda5. You can run any of the following commands to unmount the mounted file system:

``` {#codeblock_zpp_ir9_d8h}
umount /dev/hda5
umount /mnt/hda5
umount /dev/hda5 /mnt/hda5
```

 /etc/fstab is an important configuration file in Linux systems. It contains detailed information about the file system and storage devices that are mounted in the system at startup.

If you do not want to mount a specified partition when you launch an instance, you need to delete the corresponding statement in the current file. For example, deleting the following statement can break xvdb1 at startup:

``` {#codeblock_jtn_3gg_msw}
/dev/xvdb1 /leejd ext4 defaults 0 0
```

Other important configuration files in Linux systems are as follows:

|Configuration file|Description|Risk of changing the file|
|:-----------------|:----------|:------------------------|
|/etc/issue\*, /etc/\*-release, /etc/\*\_version|The system release configuration file|Modifying /etc/issue\* causes the system release to be recognized improperly and system creation failure.|
|/boot/grub/menu.lst, /boot/grub/grub.conf|The system boot configuration file|Modifying /boot/grub/menu.lst causes the kernel to be loaded improperly and system boot failure.|
|/etc/fstab|The configuration file for partitions mount at system startup|Modifying this file causes failure of loading abnormal partitions and system boot failure.|
|/etc/shadow|The system password-related configuration file|If this file is modified to read-only, the password file cannot be modified and system creation fails.|
|/etc/selinux/config|The system security policy configuration file|Modifying /etc/selinux/config to enable SELinux causes system boot failure.|

## How can I confirm that a data disk has been unmounted and a new custom image can be created? {#section_wdy_3ty_dhb .section}

1.  Confirm that the statement of automatically mounting data disk partitions in the /etc/fstab file has been deleted.
2.  Run the mount command to view the mount information of all devices. Ensure that the corresponding data disk partition information is not included in the execution results.

## Does a custom image still exist after the corresponding instance is released? {#section_qbd_ghx_fhb .section}

Yes.

## After an instance expires or releases its data, is the corresponding custom image affected? Are instances created from the custom image affected? {#section_zc5_shx_fhb .section}

No.

## Can I replace the operating system of an instance created with a custom image? Can the original custom image still be used after replacing the system? {#section_j1z_thx_fhb .section}

Yes.

## Can I use a custom image when I change the system disk and choose another operating system? {#section_b21_zhx_fhb .section}

Yes. For more information, see [Replace the system disk \(non-public image\)](../../../../intl.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

**Note:** After a system disk is replaced with a custom image, the original data is fully covered.

## Can I use a custom image to replace the system disk data of another ECS instance? {#section_cv1_g3x_fhb .section}

Yes. For more information, see [Replace the system disk \(non-public image\)](../../../../intl.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

**Note:** The custom image will completely cover all data in the system disk of the target ECS instance.

## Is it possible to upgrade the CPU, memory, bandwidth, and hard disk of an ECS instance that is created with a custom image? {#section_y35_m3x_fhb .section}

Yes.

## Can I use a custom image across regions? {#section_twm_n3x_fhb .section}

No. A custom image can only be used in the same region. For example, a custom image created from an instance in the China East 1 region cannot be used to create ECS instances in China East 2.

If you need to use a custom image across regions, you can first copy the image to the target region. For more information, see [Copy custom images](../../../../dita-oss-bucket/SP_2/DNA0011894323/intl.en-US/Images/Custom image/Copy custom images.md#).

## Can a custom image of a Subscription instance be used to create a Pay-As-You-Go instance? {#section_t5m_cjx_fhb .section}

Yes. The usage of a custom image has nothing to do with the billing method.

## Why does the system disk auto-expansion fail in an instance created with a custom image? What can I do? {#section_oqc_u0t_5ri .section}

The possible reason may be that the cloud-init service is not installed, the cloud-init service fails, or the file system does not support the expansion.

When the automatic expansion of a system disk fails, you can manually expand the capacity.

## Why do I need to comment out mounted items when creating a custom image or ECS instance? {#section_uar_ern_zbt .section}

When you create an ECS instance by using a custom image, the following reasons can cause the failure of mounting disks:

-   The created ECS instance does not have a data disk.
-   The data disk is a new disk and has not been formatted or partitioned.
-   The mounted disks in the /etc/fstab file are not commented out in the created custom image.

The following shows an example of data disk mounting failure, where the data disk of an ECS instance is not partitioned, and the mounted disks are not commented out in the /etc/fstab file of the custom image.

1.  The ECS instance data disk is not partitioned, as shown in the following figure:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147740/156592667546300_en-US.png)

2.  In the ECS instance created from the custom image, the mounted disks are not commented out in /etc/fstab, as shown in the following figure:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147740/156592667646301_en-US.png)

3.  Upon instance startup, data disks are mounted according to the configuration in /etc/fstab. However, the mount operation fails because data disks are not partitioned, as shown in the following figure:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147740/156592667646302_en-US.png)


The general case where you do not need to comment out mounted disks: when you create an ECS instance, you select data disks and create them from a partitioned and formatted data disk snapshot.

If the problem is not resolved, [contact after-sales technical support](https://selfservice.console.aliyun.com/ticket/createIndex).

## How do I configure and use the private Docker image registry? {#section_4wu_r5p_bi1 .section}

 **The Private Docker image registry and Alibaba Cloud OSS** 

Image management is at the core of Docker. To allow organizations to share images internally, Docker officially created an open source project docker-registry on Github, which is intended for building private Docker image repository.

 **Quick start supports the docker-registry of Alibaba Cloud OSS** 

You can download docker-registry from [GitHub](https://github.com/docker/docker-registry) and then install it. You can run `pip install docker-registry-driver-alioss` to install the OSS driver.

1.  Run docker registry:

    ``` {#codeblock_028_yze_uie}
     docker run -e OSS_BUCKET=-e STORAGE_PATH=/docker/ -e OSS_KEY=-e OSS_SECRET=-p 5000:5000 -d chrisjin/registry:ali_oss
    ```

2.  Configure config.yml:

    ``` {#codeblock_rvn_x7o_ncu}
     ```local: &local
     <<: *common
     storage: alioss
     storage_path: _env:STORAGE_PATH:/devregistry/
     oss_bucket: _env:OSS_BUCKET[:default_value]
     oss_accessid: _env:OSS_KEY[:your_access_id]
     oss_accesskey: _env:OSS_SECRET[:your_access_key]```
    ```

3.  Start docker-registry:

    ``` {#codeblock_2np_mne_mlf}
     DOCKER_REGISTRY_CONFIG=［your_config_path］ gunicorn -k gevent -b 0.0.0.0:5000 -w 1 docker_registry.wi:application
    ```


If the problem is not resolved, [open a ticket](https://selfservice.console.aliyun.com/ticket/createIndex.htm).

## When do I need to copy a custom image? {#section_pbs_h4c_ghb .section}

Custom images can only be used in the same region and cannot be used directly across regions. If you need to:

-   Deploy applications in ECS instances in multiple regions.
-   Migrate ECS instances to other regions.
-   Use custom images across regions.

You can achieve the preceding goals by copying custom images. Specifically, you can copy a custom image in the current region to other regions under the same account, and use the custom image to implement the same application environment in other regions.

## Which images can be copied? {#section_j4j_n4c_ghb .section}

Only custom images can be copied. Other images \(public images, Marketplace images, and images shared by others\) cannot be copied.

## Which regions support copying custom images currently? {#section_jcb_44c_ghb .section}

All regions of Alibaba Cloud support copying custom images.

## How long does it take to copy a custom image? {#section_wzx_44c_ghb .section}

The time consumed depends on the network transmission speed and the number of tasks in the queue. Copying a custom image is to copy an image across regions through the network. You need to wait patiently.

## How am I charged when I copy a custom image? {#section_nbz_q4c_ghb .section}

The copy image process includes the following operations:

1.  Copy the snapshot from which a custom image is created from the source region to the destination region.
2.  Create a custom image based on the snapshot in the destination region.

The above process may involve the following fees:

-   Fees for traffic between different regions. Alibaba Cloud has not charged this traffic yet. Please visit the Alibaba Cloud website regularly for announcements.
-   The copied snapshot takes up the snapshot capacity. Currently, snapshot capacity is charged. For more information, see [Snapshot service fee details \(pay after volume\)](../../../../intl.en-US/Pricing/Billing of snapshots.md#).

## What are the limitations of source and destination images during the copy process? {#section_inj_s4c_ghb .section}

During the copy process, the source image cannot be deleted. The copy process can be cancelled, and then the destination image cannot be used to replace a system disk or create an ECS instance.

## How do I copy the images under my Alibaba Cloud account to other regions under other Alibaba Cloud accounts? {#section_kyv_54c_ghb .section}

You need to copy your own images to the destination region and then share the images with the intended Alibaba Cloud accounts. After that, the images are displayed in the shared image list of those accounts.

## Is the copy image operation subject to image capacity limitation? {#section_k14_x4c_ghb .section}

No. There is no limit. However, if the image capacity exceeds 500 GiB, you will be prompted to open a ticket when you click **Copy Image** in the ECS console.

## I copied a custom image to another region where it appears as **Available**, but when I used it to create an instance, it prompts "The specified image is disabled or deleted". Why? {#section_lxo_ujw_fm3 .section}

If you create a custom image from a Marketplace image, and then copy it to other regions, it cannot be used to create an ECS instance. In other words, you cannot create a custom image from a Marketplace image, and then copy that custom image to another region for ECS instance creation.

## How do I migrate data from the international station to China? {#section_oqq_9z9_t00 .section}

You can do this by copying a custom image. For more information, see [Copy custom images](intl.en-US/Images/Custom image/Copy custom images.md#).

## How many images can be shared to me? {#section_xry_y4c_ghb .section}

100.

## How many users can each image be shared to? {#section_pwp_ypc_ghb .section}

50.

## Does using a shared image take up my image quota? {#section_agd_2qc_ghb .section}

No.

## Is there a geographical limitation when creating an instance by using a shared image? {#section_mls_2qc_ghb .section}

Yes. The same resource should be shared in the same region.

## What are the risks of creating an instance with a shared image? {#section_p4w_lqc_ghb .section}

The image owner can view how the image is shared or delete the image. After a shared image is deleted by its owner, the corresponding ECS instances cannot reinitialize the system disk.

Alibaba Cloud does not guarantee the integrity and security of images shared by other accounts. You need to bear the risks when using shared images. Please select the images shared by trusted accounts. After you create an ECS instance by using a shared image, you need to log on to the ECS instance to check the security and integrity of the shared image.

## What are the risks if I share a custom image with other accounts? {#section_r4q_nqc_ghb .section}

There is a risk of data leakage and software disclosure. Before you share a custom image with other accounts, check whether there is sensitive and important data and software in the image. Once you share your image with an account, its owner can use the shared image to create an ECS instance, which can be used to create more custom images. Over this process, the data is spread all over and over again, causing a risk of disclosure.

## Can I share an image from account A with account B? {#section_abm_4qc_ghb .section}

No. Only the owner of an image can share it with other accounts.

## After I share an image with others, can I still create an instance by using that image? {#section_xny_pqc_ghb .section}

Yes. After you share an image to another account, you can still use the image to create an ECS instance. You can also continue to create a custom image based on the ECS instance.

## Can an image created from instance A in a China North region be shared with instance B in a China East region? {#section_b5i_fn9_i06 .section}

-   If instances A and B belong to the same account, you can directly copy the image to the China East region and apply it to instance B. For more information, see [Copy custom images](intl.en-US/Images/Custom image/Copy custom images.md#).
-   If instances A and B do not belong to the same account, you can copy the image to the China East region and share it to the account of instance B. For more information, see [Copy custom images](intl.en-US/Images/Custom image/Copy custom images.md#) and [Share custom images](intl.en-US/Images/Custom image/Share custom images.md#).

## Why is there no option to export an image? {#section_j80_1pu_tv2 .section}

You need to open a ticket to apply for the permission. For more information, see [Export custom images](intl.en-US/Images/Custom image/Export custom images.md#).

## I want to export an image to my local computer for testing. What should I do? {#section_9dl_9cs_oba .section}

Currently, the export format of an image file is defaulted to .raw.tar.gz, which can be decompressed as the .raw format. You can search for the relevant documentation for using images of this format. Alibaba Cloud does not pose any special restrictions on it.

## Can I delete a custom image after I used it to create an ECS instance? {#section_lvj_dht_8a4 .section}

You can **Force Delete** the image. However, after you delete the image, the ECS instance created with it cannot [reinitialize the cloud disk](intl.en-US//Reinitialize a cloud disk.md#).

## Can I delete a custom image from my account after I have shared it with another account? {#section_fqt_49s_s3v .section}

Yes. However, after you delete the shared image, all the ECS instances created with that image cannot reinitialize their system disks. Therefore, we recommend that you delete all the relationships of the custom image before you delete the image.

## What are the impacts after I cancel the sharing of a custom image \(M\) with account A? {#section_qn6_1dm_1tn .section}

You will be unable to query the shared image M through the ECS console or the ECS API. The shared image M cannot be used to create ECS instances or replace system disks under account A. If account A has created ECS instances with the shared image M before the sharing is cancelled, those instances will be unable to reinitialize their system disks.

## When I was deleting an image, it prompts that "the image cannot be deleted because the specified image ID is involved with existing instances". Why? {#section_qe9_38d_hvk .section}

You may have created the image by using a snapshot. If you want to delete the image, you must select **Force Delete**. After you forcibly delete the image, the use of the corresponding instances are not affected, but they cannot reinitialize their cloud disks. For more information, see [Delete custom images](intl.en-US/Images/Custom image/Delete custom images.md#).

## When I try to replace a system disk, can I replace the corresponding image by replacing the system disk if the selected image contains data disks? {#section_053_0tw_h6a .section}

No. If you must use this image, we recommend that you use this image to create a Pay-As-You-Go ECS instance, and create a snapshot for the system disk. Then, use the snapshot to create a custom image that only contains the system disk. Finally, select that custom image when you replace a system disk.

## I want to replace the operating system of my ECS instance with an existing image. What should I do? {#section_69i_52e_jfd .section}

See [Change the operating system](intl.en-US/Images/Change the operating system.md#).

**Note:** We recommend that you create a snapshot to back up data before you proceed.

## Can an image created from an instance under account A be used to replace a disk under account B? {#section_oww_crp_0j9 .section}

You can share the image to account B. For more information, see [Share custom images](intl.en-US/Images/Custom image/Share custom images.md#).

**Note:** If you want to use an image to replace a system disk, the image can only contain a system disk.

## When I am creating an instance with a custom image, why is the configuration cost higher than that of creating an instance with a public image? {#section_k04_yg7_uoa .section}

Any of the following reasons can cause this situation:

-   The custom image contains data disks. When an instance is created with such an image, the cost of the data disks causes the total instance cost to be higher than that of a corresponding public image.
-   The custom image is created from a paid public image \(such as Windows Server, and Redhat Enterprise Linux\).

## How do I buy a Marketplace image? {#section_hxc_rqc_ghb .section}

You can purchase it either separately on the **Image Market**, or on the ECS purchase page during ECS instance creation.

## How long can I use a purchased image? {#section_hqw_prc_ghb .section}

In principle, it can be used indefinitely. However, as a software, an image has its own life cycle. In addition, image vendors only provide services in a limited time period, which is described in the commodity details.

## Is refunding available to the images on the **Image Market**? {#section_gzm_qrc_ghb .section}

Images support refunding without giving a reason in a limited time period according to the Alibaba Cloud market rules. However, refunding is not allowed in the following cases:

-   The purchased image is deployed on an ECS instance within the refund time limit.
-   The purchased image is deployed on an ECS instance before the application for refunding is approved.
-   In other words, you can only apply for refunding when images have not been used.

## After commercialization of the image market, are free images still available on the market? {#section_okl_src_ghb .section}

A certain number of free images are still available on the image market. However, you still need to purchase them \(at the cost of USD 0\) before you can use them.

## I bought an image on the image market in Hangzhou. Can I use it to create an ECS instance or replace a system disk in Beijing? {#section_ndz_src_ghb .section}

No. If you purchase an image on the image market, you can only use it to create an ECS instance or replace a system disk in the same region.

## My ECS instance is created with an image on the image market. Do I need to make further payment when I upgrade or renew my ECS instance? {#section_jwc_fsx_fhb .section}

No.

## My ECS instance is created with an image on the image market. After my ECS instance is released, can I continue to use that image free of charge when I purchase an ECS instance? {#section_yqb_wrc_ghb .section}

Yes.

## I created an ECS instance with an image on the image market and then created a custom image from that instance. Do I need to pay for the image when I create an ECS instance by using this custom image? {#section_pnn_yrc_ghb .section}

Yes. You need to pay the original price of the image \(its price on the image market\).

## If I buy an image from the image market and copy it to another region for ECS instance creation, do I need to pay for the image? {#section_bqm_zrc_ghb .section}

Yes. You need to pay the original price of the image \(its price on the image market\).

## If I share a custom image from the image market to account B for ECS instance creation, does account B need to pay for the image? {#section_ymk_1sc_ghb .section}

Yes. Account B needs to pay the original price of the image \(its price on the image market\).

## Is a fee incurred if I replace a system disk by using an image on the image market or an image that originates from the image market? {#section_uj5_1sc_ghb .section}

It depends. If the image of your ECS instance is just a different version of the image that is used for the replacement, no fee is charged. Otherwise a fee is charged.

## My ECS instance is using an image on the image market. Is a fee incurred if I reset the system disk? {#section_nj4_bsc_ghb .section}

No.

## How do I call ECS APIs to create an ECS instance or replace a system disk by using an image on the image market or a custom or shared image that originates from the image market? {#section_xl1_csc_ghb .section}

1.  Confirm that the used image ID indicates an image that is on the image market or originates from the image market. Call DescribeImages to query the image information.

    If the product ID \(`ProductCode`\) of your image is not empty, it means that your image is on the image market or originates from the image market. For example, if the `ProductCode` of your image is abcd000111, you can access the image item at [http://market.aliyun.com/products/123/abcd000111.html](http://market.aliyun.com/products/123/abcd000111.html).

2.  Select the version and region of the target image and buy the image only.

    An image purchased in a region can only be used in ECS instances in that region. In addition, you can only purchase one image at a time. In other words, if you need to create multiple ECS instances, you need to purchase multiple images.

3.  After the purchase is completed, you can create an ECS instance or replace a system disk.

## If I do not buy an image that is on the image market or originates from the image market, will errors be reported when I call ECS APIs to use that image for ECS instance creation or system disk replacement? {#section_sxt_hsc_ghb .section}

Yes. An error will be reported and the error code is `QuotaExceed.BuyImage`.

## I configured ECS to automatically create instances whose number ranges from 10 to 100. What should I do with images on the image market for this purpose? {#section_nfx_5sc_ghb .section}

If you need to automatically launch n instances of the same type, you need to purchase n images on the image market in advance.

## Do images of the image market support bulk purchase? {#section_clp_ysc_ghb .section}

No.

## If an image on the image market is no longer available for sale \(such as jxsc000010 and jxsc000019\), what should I do to ensure the normal functioning of auto scaling settings? {#section_stt_zsc_ghb .section}

In this case, we recommend that you select an alternative image on the image market.

## Can one product code support images of different regions? {#section_os3_btc_ghb .section}

Yes. The precondition is that the relevant regions already support the image item.

## I bought 100 images with the same product code. Can I use them in all regions? {#section_uzj_ctc_ghb .section}

Currently, images on the image market already have the region attribute. Please purchase images of the corresponding region.

## After I select the "IO Optimized Instance" option, I cannot select images on the image market when purchasing an ECS instance. Why is that and how do I deal with it? {#section_tch_39p_cv5 .section}

 **Phenomenon** 

When I purchase an ECS instance on the Alibaba Cloud official website, I cannot select any images on the image market.

 **Cause** 

This is may be due to that you have selected the **IO Optimized Instance** option when you purchase an ECS instance.

Compared with common ECS instances, IO optimized instances provide better network capabilities between instances and cloud disks, maximizing the storage performance of SSD Cloud Disks. However, not all images support IO optimized instances because the related optimization operations involve network, storage, and internal drivers of images.

 **Solution** 

When you purchase an IO optimized instance, we recommend that you select an official standard image supported by the relevant instance and then deploy the business environment.

If the problem is still not resolved, contact [after-sales technical support](https://selfservice.console.aliyun.com/ticket/createIndex.htm).

## What are Subscription and weekly paid images on the image market? {#section_zxy_n5c_ghb .section}

The Subscription and weekly paid images on the image market refer to the images that are purchased from the Alibaba Cloud market and billed weekly, monthly or yearly. These images are developed and maintained by image providers, who are responsible for both pre-sales consulting and after-sales service. In this topic, such images are collectively referred to as prepaid images.

## Which ECS instances can I use with a prepaid image? {#section_fts_45c_ghb .section}

A prepaid image can only be used with a Subscription or weekly paid instance. In addition, their billing periods should be the same.

## How do I buy a prepaid image? Can I buy it separately? {#section_rfp_s5c_ghb .section}

Currently you cannot purchase a prepaid image separately.

You can purchase a prepaid image in one of the following ways:

-   When you create an ECS instance, select **Subscription** as the billing method, and then select an image from the Marketplace. Finally, select the duration as week, month, or year.

    **Note:** In this case, you need to pay for both the instance and the image. If the instance is created successfully, it means that you have purchased both the instance and the image.

-   If you want to use a prepaid image on an existing Subscription or weekly paid ECS instance, you can replace the operating system with a prepaid image. In this case, you can only select the payment period of the image according to the payment period of the ECS instance. For more information, see [Replace the system disk \(non-public image\)](../../../../intl.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

    **Note:** In this case, you only need to pay for the image.


## How do I pay for prepaid images? {#section_xhj_w5c_ghb .section}

A prepaid image is paid in advance, and its billing period should be the same as that of the corresponding Subscription or weekly paid ECS instances.

The price of an image is decided by its provider.

## Can I use a prepaid image after it expires? How do I continue to use it? {#section_cc4_x5c_ghb .section}

After a prepaid image expires, you can no longer use it if you fail to renew it in time.

You cannot renew a prepaid image separately. If you want to continue using it, you can renew an image during the renewal of the relevant ECS instance.

## After purchasing a prepaid image, can I request a refund if I no longer want to use it? {#section_gwb_z5c_ghb .section}

The availability of a refund is up to the image provider. You can consult the image provider before your purchase.

## How is the fee settled when a refund is made? {#section_hvt_z5c_ghb .section}

If a refund is available, the image provider will make the refund according to your actual usage.

## Can a prepaid image be converted to a Pay-As-You-Go image? {#section_hpg_1vc_ghb .section}

At present, this conversion is not supported. However, we will provide this feature in the future. Please pay attention to the announcement on the Alibaba Cloud official website.

## Can I replace a prepaid image with another image and vice versa? How is the fee calculated? {#section_sqw_1vc_ghb .section}

Yes. You can replace an image by replacing the system disk of an ECS instance. The following scenarios exist regarding replacing an image:

-   Replace other types of images \(such as public images, custom images, and shared images\) with prepaid images. After the replacement, the system calculates the actual cost according to the cost of the image and the remaining payment period of the ECS instance.
-   Replace a prepaid image with an image of another category \(such as public images, custom images, and shared images\). If the vendor allows for refunding, a refund will be made according to your actual usage.
-   Replace one prepaid image \(image A\) with another prepaid image \(image B\). After the replacement, if image A allows for refunding, a refund will be made according to the relevant policy. As for image B, the actual cost will be calculated according to the price of the image and the remaining payment period of the ECS instance.

## Where can I view and manage the prepaid images I purchased? {#section_fmx_fvc_ghb .section}

You can log on to the [ECS console](https://ecs.console.aliyun.com), and then view and manage the prepaid images you purchased in **Custom Images** \> **Image Market**

## Is there a fee for a custom image created with a prepaid image? How will such a custom image be affected if the relevant prepaid image expires? {#section_klq_gvc_ghb .section}

When you use a custom image \(created with a prepaid image\) to create an instance or replace a system disk, you are re-ordering the image on the image market. Therefore, the use of a custom image is not affected no matter whether the original prepaid image expires.

## Why cannot some ECS instances choose the Windows operating system? {#section_ajg_qwc_ghb .section}

When you create an ECS instance by using a Windows operating system, you need to ensure that the instance memory is greater than or equal to 1 GiB. For ECS instances with less than 1 GiB of memory \(for example, 512 MiB\), they can only select Linux images and Windows Server 1709 images.

## Is a fee incurred when an ECS instance uses a operating system? {#section_ttw_qwc_ghb .section}

In mainland China, the Windows Server public images come with a activation code, and no activation fee is charged. In other countries or regions, an activation fee is charged.

Windows Server public images allow at most two [remote connection](../../../../intl.en-US/Instances/Connect to instances/Connect to Windows instances/Connect to a Windows instance.md#) sessions by default. If you need more connections, please purchase the Remote Desktop \(RD\) authorization service from Microsoft separately.

In addition to the Red Hat public images, other Linux public images do not require the license fee.

## Can I install or upgrade my operating system myself? {#section_zhs_twc_ghb .section}

You cannot install or upgrade it yourself. An ECS instance needs to use an image provided by Alibaba Cloud, and you cannot add or upgrade it yourself. However, you can do the following:

-   Replace a system disk and re-select an operating system. For more information, see [Replace the operating system](../../../../dita-oss-bucket/SP_2/DNA0011894323/intl.en-US/Images/Change the operating system.md#).
-   Create an ECS instance by using a custom image that is imported from a local device. For information on how to import an image, see [Import an image](../../../../intl.en-US/Images/Custom image/Import images/Notes for importing images.md#). For information on how to create an ECS instance by using a custom image, see [Create an ECS instance with a custom image](../../../../intl.en-US/Instances/Create an instance/Create an instance by using a custom image.md#)
-   Patch an operating system.

## Do the operating systems have a graphical interface? {#section_ulp_xwc_ghb .section}

In addition to the Windows Server Semi-Annual Channel instances, other Windows operating systems offer a management desktop. For how to use the Windows Server Semi-Annual Channel operating system, see [Manage Windows Server Semi-Annual Channel images and instances](intl.en-US/Images/FAQ/Manage Windows Server Semi-Annual Channel images and instances.md#).

Linux operating systems offer a command line mode, and you can install a graphical desktop as needed. For more information, see [How to install desktop GUI for Linux ECS](https://www.alibabacloud.com/help/faq-detail/41227.htm).

## How do I choose an operating system? {#section_wqy_zwc_ghb .section}

See [How to select a system image](https://www.alibabacloud.com/help/faq-detail/40651.htm).

## Do public images come with the FTP service? {#section_jtv_dxc_ghb .section}

No. You need to configure it yourself. For more information, see [Build an FTP site on a Windows ECS instance](../../../../intl.en-US/Tutorials/Build an FTP site on an ECS instance/Build an FTP site on a Windows ECS instance.md#) and [Build an FTP site on a Linux ECS instance](../../../../intl.en-US/Tutorials/Build an FTP site on an ECS instance/Build an FTP site on a Linux ECS instance.md#).

## Which SUSE versions does Alibaba Cloud support? {#section_mgc_fxc_ghb .section}

Currently, Alibaba Cloud public images support the following SUSE versions:

-   SUSE Linux Enterprise Server 12 SP2 64-bit
-   SUSE Linux Enterprise Server 11 SP4 64-bit

## What services or support are provided by the SUSE operating systems? {#section_jpr_fxc_ghb .section}

The SUSE Linux Enterprise Server \(SLES\) operating systems sold on Alibaba Cloud are synchronized with the SUSE update source regularly. For instances that are created with Alibaba Cloud SLES public images, the support of their operating systems are covered by Alibaba Cloud enterprise-level support service. If you have purchased the enterprise-level support service, you can open a ticket to contact Alibaba Cloud for assistance. The Alibaba Cloud support team will help you fix the problems that occur in the SLES operating systems.

## After an ECS instance is released upon expiration, if an image is manually created for the instance, can I retrieve the data of the previous instance? {#section_uj1_il5_0xb .section}

Yes. You can retrieve the instance data in any of the following ways:

-   Create a new instance by using the previously created image. For more information, see [Create an instance by using a custom image](../../../../intl.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).
-   Replace the system disk for the current instance by using the previously created image. For more information, see [Replace the system disk \(non-public image\)](../../../../intl.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

    **Note:** When you replace a system disk, note the following:

    -   The system disk data of the current instance will be completely lost and restored to the state of the image.
    -   The image must be in the same region as your current instance.

## I have an ECS instance now, and want to buy another ECS instance by using an image of the current ECS instance. What should I do? {#section_d2a_pl9_3vq .section}

You can create a custom image for the current ECS instance and then create an ECS instance by using that custom image. For more information, see [Create a custom image by using an instance](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#) and [Create an instance by using a custom image](../../../../intl.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).

## I purchased a new ECS instance, how do I restore my shared image to this newly purchased ECS instance? {#section_54f_mg4_r2p .section}

Make sure that you have shared the image with the account of the newly purchased instance and choose one of the following methods according to the actual situation.

-   If the shared image and the newly purchased instance are in the same region, you can select the shared image while replacing the system disk. For more information, see [Replace the system disk \(non-public image\)](../../../../intl.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).
-   If the shared image and the newly purchased instance are not in the same region, you need to copy the image to the destination region, and then replace the image by replacing the system disk. For more information, see [Copy custom images](intl.en-US/Images/Custom image/Copy custom images.md#) and [Replace the system disk \(non-public image\)](../../../../intl.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

**Notice:** The following risks are associated with replacing a system disk:

-   The original system disk will be released. Therefore, we recommend that you create a snapshot to back up your data in advance.
-   Replacing a system disk requires stopping the relevant instance, so your business will be interrupted.
-   After a system disk is replaced, you need to redeploy the business environment on the new system disk. Your business may be interrupted for a long time.
-   Replacing a system disk is to re-assign a system disk to your instance, and the disk ID will change. Therefore, a snapshot created from the old system disk cannot be used to roll back the new system disk.

## The operating system of my instance is Windows Server 2008 R2 Enterprise Edition. It now prompts that the operating system is not genuine? What should I do? {#section_dcb_fs7_ljf .section}

You can follow these steps:

1.  Activate Windows. For more information, see [How to activate the VPC-connected Windows instances by using KMS servers](https://www.alibabacloud.com/help/faq-detail/41056.htm).

    **Note:** Disable the firewall in your instance before proceeding.

2.  Log on to the ECS console.
3.  Connect to your instance through the remote connection function in the ECS console. Then, download and install the patch to your instance. For more information, see [How to solve authentication errors caused by CredSSP encryption oracle remediation when connecting to Window instances](https://www.alibabacloud.com/help/faq-detail/71931.htm) \(Microsoft updated the patches and authentication request methods related to the Credential Security Support Provider Protocol \(CredSSP\) in May 2018\).

## I have multiple accounts on Alibaba Cloud, and I want to transfer one instance under account A to account B, or use an image to migrate the environment and applications to an instance under account B. What should I do? {#section_cvk_0gm_ods .section}

You can follow these steps:

1.  Create a custom image by using the instance of account A. For more information, see [Create a custom image by using an instance](intl.en-US/Images/Custom image/Create custom image/Create a custom image by using an instance.md#).
2.  Share the image to account B. For more information, see [Share custom images](intl.en-US/Images/Custom image/Share custom images.md#).
3.  Create an instance under account B by using the shared image. For more information, see [Create an instance by using a custom image](../../../../intl.en-US/Instances/Create an instance/Create an instance by using a custom image.md#).

## Can ECS instances in different VPCs communicate with each other? {#section_lqt_tci_xa6 .section}

Intranet communication can be implemented through Express Connect and Cloud Enterprise Network \(CEN\). For more information, see [Interconnect two VPCs under the same account](../../../../intl.en-US/Peering connections/Interconnect two VPCs under the same account.md#) and [Connect network instances in different regions using same account](../../../../intl.en-US/Quick Start/Connect networks that belong to the same account but different regions.md#).

## How to handle CentOS DNS resolution timeout? {#section_x8y_les_u5u .section}

 **Analysis** 

The DNS resolution mechanism has changed in CentOS 6 and CentOS 7. Therefore, if CentOS 6 \(7\) instances were created before February 22, 2017 or are created with custom images that were created before February 22, 2017, they may be prone to this issue.

 **Solution** 

Follow these steps to fix this problem:

1.  Download the script [fix\_dns.sh](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/59344/cn_zh/1505957231428/fix_dns%20%281%29.sh).
2.  Put the downloaded script in the /tmp directory of the CentOS system.
3.  Run the `bash /tmp/fix_dns.sh` command to execute the script.

 **Script role** 

It judges if the `options`\>`single-request-reopen` configuration exists in the DNS resolution file /etc/resolv.conf. For more information, see [resolv.conf - resolver configuration file](http://man7.org/linux/man-pages/man5/resolv.conf.5.html).

The DNS resolution mechanism of CentOS 6 \(7\) uses the same quintuple to send IPV4 and IPV6 DNS requests, for which purpose the `single-request-reopen` configuration should be enabled. After the configuration is enabled, once two consecutive requests from the same socket are handled, the resolver closes the socket after the first request is sent, and opens a new socket before the second request is sent. After the configuration is made, it takes effect without the need to restart the instance.

 **Script logic** 

1.  Determine if the instance operating system is CentOS:
    -   If it is not CentOS \(such as Ubuntu and Debian\), the script stops working.
    -   If it is CentOS, the script continues working.
2.  Query the configuration of `options` in the /etc/resolv.conf file.
    -   If the configuration of `options` is not available:

        The Aliababa Cloud configuration of `options` \(`options timeout:2 attempts:3 rotate single-request-reopen`\) is used by default.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/147740/156592667646335_en-US.png)

    -   If the configuration of `options` is available:
        -   If the configuration of `single-request-reopen` does not exist, append that item in the configuration of `options`.
        -   If the configuration of `single-request-reopen` exists, the script stops working and no change is made to the configuration of the DNS nameserver.

