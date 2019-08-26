# Create a launch template {#concept_pzl_ww5_xdb .concept}

This topic describes how to create a launch template and the related notes.

## Limits {#section_kk8_9mz_wt2 .section}

-   Each account can create a maximum of 30 launch templates per region.
-   All parameters are optional when you create a template by using the ECS console. However, if the template that you want to use to create an instance does not have all required parameters \(such as the instance type and image\), you must specify the required parameters at instance creation.
-   A template cannot be modified after it is created.

## Create a launch template in the ECS console {#console .section}

To create a launch template, follow these steps:

1.  Click **Create Template**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13805/15667768515347_en-US.png)

2.  Go to the Launch Template page and complete the basic configurations and advanced configurations.

    **Note:** During your first template creation, the **Clone Template** area is unavailable. If you have already created templates, you can select an existing template and version, and then modify its configurations.

3.  On the Confirm Configuration page, enter a template name and description, and then click **Create Launch Template**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13805/15667768515348_en-US.png)

    **Note:** All parameters are optional when you create a template. However, on the Confirm Configuration page, we recommend that you configure the required parameters so that you can create instances in one click as needed.


Click **View Template** in the Activated dialog box to view the template you have created.

You can also complete this task by calling the [CreateLaunchTemplate](../reseller.en-US/API Reference/Launch templates/CreateLaunchTemplate.md#) API action through Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK.

## Create a launch template on the ECS purchase page {#commonbuy .section}

You can save the configurations of an instance as a template when you create an instance. This facilitates instance creation in the future.

1.  Go to the [ECS product details page](https://partners-intl.aliyun.com/vodafone/product/ecs), and then click **Buy Now**.
2.  Configure the required parameters, and then click **Save as Launch Template**.
3.  In the dialog box that appears, select **New Template**, enter a template name and description, and then click **Save**.

Click **View Template** in the Created dialog box to view the template you have created.

