# Create a template {#concept_pzl_ww5_xdb .concept}

You can create a launch template using the following methods:

-   [Create a launch template in the ECS console](#console) if you want to create launch templates first, and then create instances using a specific launch template in one click.

-   [Create a launch template on the ECS buy page](#commonbuy) to create an instance and save its configuration information as a launch template.


**Note:** 

-   Each account can create a maximum of 30 launch templates per region.
-   All parameters are optional when you create a template using the ECS console. However, if the template that you want to use to create an instance does not have all required parameters \(such as an image\), then you must specify the required parameters at instance creation.
-   A template cannot be modified after it is created.

## Create a template in the ECS console {#console .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Launch Templates**, and then click **Create Template**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13805/15429604265347_en-US.png)

3.  Go to the Launch Template page and complete the basic configurations and advanced configurations.

    **Note:** During your first template creation, the **Clone Template** area is unavailable. If you have already created templates, you can select an existing template, and version, and then modify its configurations.

4.  On the Confirm Configuration page, enter a template name and description, and then click **Create Launch Template**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13805/15429604265348_en-US.png)

    **Note:** All parameters are optional when you create a template. However, on the Confirm Configuration page, we recommend that you configure the required parameters so that you can create instances in one click as needed.


Click **View Template** in the Activated dialog box to view the template you have created.

## Create a template on the ECS buy page {#commonbuy .section}

1.  Go to the ECS product details page, and then click **Buy Now**.
2.  Configure the required parameters, and then click **Save as launch template**..
3.  In the dialog box that appears, select **Create Template**, enter a template name and description, and then click **Save**.

Click **View Template** in the Activated dialog box to view the template you have created.

