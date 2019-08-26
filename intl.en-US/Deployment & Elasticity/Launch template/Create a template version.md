# Create a template version {#concept_nhb_3y5_xdb .concept}

One launch template can have multiple versions. This topic describes how to create a template version and change the default template version.

## Limits {#section_vim_s5a_l3t .section}

-   The default version number of a newly created template is 1, and you can create additional versions based on this template.

    **Note:** The version number increments automatically as you create a new version. You cannot customize the version number, but you can set any of the template versions as the default version.

-   Each template can have a maximum of 30 versions.
-   All parameters are optional when you create a template version. However, if the version that you want to use to create an instance does not have all required parameters \(such as the instance type and image\), you must specify the required parameters at instance creation.
-   A template version cannot be modified after it is created.

## Prerequisites {#section_s44_z1v_xdb .section}

You have already [created a launch template](reseller.en-US/Deployment & Elasticity/Launch template/Create a launch template.md#).

## Create a template version by using the ECS console {#console .section}

To create a template version, follow these steps:

1.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Launch Templates**.
2.  Select a template ID to view its version information, and then click **New Version**. You can also click **New Version** in the **Actions** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13806/15667767605351_en-US.png)

3.  On the Launch Template page, set the parameters.

    **Note:** You can also go to the **Clone Template** area, select an existing template and version, and then set the parameters.

4.  On the Confirm Configuration page, click **New Template Version**, and then select a template to save the version.
5.  Click **Create Launch Template**.
6.  In the dialog box that appears, click **View New Version** to view the version you have created.

## Create a template version on the ECS purchase page {#commonbuy .section}

1.  Go to the [ECS product details page](https://partners-intl.aliyun.com/vodafone/product/ecs), and then click **Buy Now**.
2.  On the **Custom Launch** page, configure the parameters.
3.  On the Preview page, click **Save as Launch Template**.
4.  In the dialog box that appears, click **New Template Version**, and then select a template to save the version.
5.  In the Created dialog box, click **View New Version** to view the version you have created.

## Change the default template version {#section_n3m_2bv_xdb .section}

You can set a commonly used template version as the default version to facilitate instance creation. To change the default template version, following these steps:

1.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Launch Templates**.
2.  Select a template ID to view its version information.
3.  Find the version you want to set as default, and then click **Set as Default** in the **Actions** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13806/15667767605352_en-US.png)


You can also complete this task by calling the [ModifyLaunchTemplateDefaultVersion](../reseller.en-US/API Reference/Launch templates/ModifyLaunchTemplateDefaultVersion.md#) API action through the Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK.

