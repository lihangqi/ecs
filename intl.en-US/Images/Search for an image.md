# Search for an image {#concept_s5x_hp2_ghb .concept}

This topic describes how to search for a specific image through the ECS console or by calling the related API action.

## Use the ECS console {#section_592_3xr_ju6 .section}

You can search for a specific image on the Images page of the ECS console.

 **Procedure** 

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the top navigation bar, select a region.
3.  In the left-side navigation pane, choose **Instances & Images** \> **Images**.
4.  Click the tab of a specific image type.
5.  In the drop-down list, select a search item such as image name, image ID, or snapshot ID.
6.  Enter one or more keywords in the search bar.

    For an ID search, you must enter an exact keyword item. For an image name search, you can enter partial keyword items \(such as `win` to return Windows public image results\).

7.  Click Search.

## Call an API action {#section_94k_aht_jmk .section}

You can call DescribeImages to search for an image through the API Explorer or [Alibaba Cloud CLI](Alibaba Cloud CLI../../SP_525/DNICMS19100401/EN-US_TP_136264.dita#concept_rc3_qrc_bhb). The following procedure uses the API Explorer as an example.

1.  Log on to the [API Explorer](https://api.aliyun.com/#/?product=Ecs&api=DescribeImages).
2.  In the drop-down list of **RegionId**, select the target region.
3.  Optional. Specify other parameters, such as **ImageName** and **ImageId**.

    **Note:** The naming rules of image IDs are as follows:

    -   Public image: The image ID is named by the version, architecture, language, and release date of the operating system. For example, the image ID of a 64-bit Windows Server 2008 R2 Enterprise Edition \(English version\) is win2008r2\_64\_ent\_sp1\_en-us\_40G\_alibase\_20190318.vhd.
    -   Custom image and Marketplace image: The image ID starts with an `m`.
    -   Shared image: The image ID is the same as the ID of the source custom image.
4.  Click **Submit Request**.
5.  Click the **Debugging Result** tab.

    If the required image is found, detailed information of the image, such as the image ID, image description, and operating system type is displayed on the **Debugging Result** tab. For more information, see [DescribeInstances](../reseller.en-US/API Reference/Instances/DescribeInstances.md#).


## What to do next {#section_0sc_460_5vs .section}

After you find the required image, you can:

-   [Create an instance by using the wizard](../reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#).
-   [Share custom images](reseller.en-US/Images/Custom image/Share custom images.md#).
-   [Copy custom images](reseller.en-US/Images/Custom image/Copy custom images.md#).
-   [EN-US\_TP\_9712.md\#](reseller.en-US/Images/Custom image/Export custom images.md#).
-   [Delete custom images](reseller.en-US/Images/Custom image/Delete custom images.md#).
-   [Modify custom images](reseller.en-US/Images/Custom image/Modify custom images.md#).

