# Delete a launch template and a specified template version {#concept_msh_ky5_xdb .concept}

This topic describes how to delete a launch template and a specified template version.

**Note:** When you delete a launch template, all versions of the template are also deleted.

## Delete a specified template version {#section_nqw_4cv_xdb .section}

1.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Launch Templates**.
2.  Select the target template ID to view the version information.
3.  In the **Version Information** area, find the version you want to delete and, in the **Actions** column, click **Delete**.

    **Note:** You cannot delete the default template version. If the version you want to delete is the default version, change it to a non-default version, and then delete it. If you no longer need any versions of a single template, delete the template.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13808/15667886065359_en-US.png)

4.  Click **OK**.

You can also complete this task by calling the [DeleteLaunchTemplateVersion](../reseller.en-US/API Reference/Launch templates/DeleteLaunchTemplateVersion.md#) API action through the Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK.

## Delete a launch template {#section_ppv_pcv_xdb .section}

1.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Launch Templates**.
2.  Find the template you want to delete, and click **Delete** in the **Actions** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13808/15667886065361_en-US.png)

3.  Click **OK**.

You can also complete this task by calling the [DeleteLaunchTemplate](../reseller.en-US/API Reference/Launch templates/DeleteLaunchTemplate.md#) API action through the Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK.

