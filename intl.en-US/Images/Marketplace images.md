# Marketplace images {#concept_spg_mct_xdb .concept}

This topic provides an overview of Alibaba Cloud Marketplace images and the related operations. You can use Marketplace images to obtain a pre-installed running environment or application on an ECS instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9711/15646239494649_en-US.png)

## Background information {#section_dg1_ah2_hso .section}

Alibaba Cloud Marketplace offers a variety of pre-installed, secure images and related services that are provided by independent software vendors \(ISVs\). These images integrate software and functions such as Hypertext Preprocessor \(PHP\) and control panel into operating systems.

**Note:** After you create an ECS instance from a Marketplace image, the system may send you a message stating that your license has expired. In this case, contact your image provider for technical support.

## Purchase a Marketplace image {#section_cyt_pd3_kjj .section}

1.  Select a region.
2.  On the Instances page, click **Create Instance** to go to the ECS purchase page.
3.  Complete basic configurations.

    Note that in the **Image** section you need to click **Marketplace Image** and then **Select from image market \(including operating system\)**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9711/156462395032602_en-US.png)

4.  In the dialog box that is displayed, select the image you need, or enter keywords in the search bar to search for the image.
5.  Complete the other configurations as prompted and click **Create Order**. Then, you can create an ECS instance according to[Step 2. Create an instance](../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).

## Create an ECS instance from a Marketplace image {#section_aei_7mn_tw1 .section}

1.  Log on to the [Alibaba Cloud Marketplace](https://partners-intl.aliyun.com/marketplace/vodafone/).
2.  Select the image you need, and click **Deploy Now**.
3.  Optional. If you have not logged on to the Alibaba Cloud console, log on before you can proceed.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9711/15646239504653_en-US.png)

4.  Finish the other configurations as prompted and click **Create Order**. Then, create an ECS instance according to [Step 2. Create an instance](../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#).

    **Note:** On the Pay page that is displayed after you click Create Order, you must confirm and pay off the required fees before you can create the ECS instance from the image.

    After you purchase a Marketplace image, you can go to the [Account Overview](https://partners-intl.console.aliyun.com/#/billing) to view your bill.


## Change the system disk of an ECS instance by using a Marketplace image {#section_yr8_1td_lge .section}

To change the image of an ECS instance you have purchased to a Marketplace image, you must change the system disk of this ECS instance.

**Note:** After you change the image, the data on the system disk is lost. Therefore, we recommend that you back up the data before you change the system disk. For more information, see [Create a snapshot](../reseller.en-US/Snapshots/Use snapshots/Create a snapshot.md#).

To change the system disk, you need to navigate to theReplace System Disk page, select **Marketplace Image** in the **Image Type** section, click **Select from image market \(including operating system\)** in the **Image Name** section, and then in the displayed **Image market** dialog box select the image you need. For more information, see [Replace the system disk \(non-public image\)](../reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk (non-public image).md#).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9711/15646239504654_en-US.png)

