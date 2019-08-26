# Create a template version {#concept_nhb_3y5_xdb .concept}

One template can have multiple versions. The default version number of a newly created template is 1, and you can create additional versions based on this template. The version number increments automatically as you create a new version. You cannot customize the version number, but you can set any of the template versions as the default version.

**Note:** 

-   Each template can have a maximum of 30 versions.
-   All parameters are optional when you create a template version.
-   A template version cannot be modified once you have created it.

You can create a template version using the following methods:

-   [Create an instance using the ECS console](#console) to create versions of a template for future use.

-   [Create an instance on the ECS buy page](#commonbuy) to create an instance, save its configurations, and create versions of a template.


## Prerequisite {#section_s44_z1v_xdb .section}

You have already [created a template](reseller.en-US/User Guide/Instances/Launch template/Create a template.md#).

## Create an instance using the ECS console {#console .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Launch Template**.
3.  Select a template ID to view its configurations, and then click **New Version**. You can also click **New Version** in the **Actions** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13806/15429610925351_en-US.png)

4.  On the Launch Template page, set the parameters.

    **Note:**  You can also go to the **Clone Template** area, select an existing template and version, and then set the parameters.

5.  On the Confirm Configuration page, select **Create New Version**, and then select a template to save the version.
6.  Click **Create Launch Template**.
7.  In the dialog box that appears, click **View New Version** to view the version you have created.

## Create an instance on the ECS buy page {#commonbuy .section}

1.  Go to the ECS product details page, and then click **Buy Now**.
2.  On the ECS buy page, configure the parameters.
3.  On the Preview page, click **Save as launch template**.
4.  In the dialog box that appears, click **Create New Version**, and then select a template to save the version.
5.  In the Activated dialog box, click **View New Version** to view the version you have created.

## Change the default version {#section_n3m_2bv_xdb .section}

1.  In the ECS console, select a template ID that has multiple versions.
2.  Locate the version you want to set as default, and then click **Set as Default** in the **Actions** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13806/15429610925352_en-US.png)


