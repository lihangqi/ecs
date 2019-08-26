# Manage deployment sets {#ManageDS .concept}

After creating a deployment set, you can modify the deployment set name and description, or remove deployment sets that are no longer required to ensure that the usage limit is not exceeded.

## Edit deployment set information {#ModifyAttributes .section}

To change the name or description of a deployment set in the ECS console, follow these steps:

1.  Log on to [ECS console](https://ecs.console.aliyun.com/).
2.  Select a region.
3.  In the left-side navigation pane, choose **Networks and Security** \> **Deployment Sets**.
4.  Locate the deployment set that needs to be modified.
5.  Edit the information using either of the following methods:
    -   Hover the cursor over the **Deployment Set Name** column, click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21512/154382177712136_en-US.png) icon that appears, and then enter the deployment set name and description.
    -   In the Actions column of the target deployment set, click **Edit**, and enter the deployment set name and description.
6.  Click **OK**.

You can also use the [ModifyDeploymentSetAttributes](../intl.en-US/API Reference/Deployment sets/ModifyDeploymentSetAttributes.md#) API operation to modify the deployment set name and description.

## Delete deployment sets {#DeleteDS .section}

**Note:** If a deployment set already includes an instance, you cannot delete the deployment set.

To delete one or more deployment sets in the ECS console, follow these steps:

1.  Log on to [ECS console](https://ecs.console.aliyun.com/).
2.  Select a region.
3.  In the left-side navigation pane, select the **Network and Security** \> **Deployment Sets**.
4.  Select one or more deployment sets that need to be deleted, hover the cursor over the **Actions** menu, and then click **Delete Deployment Set**.
5.  Click **OK** to delete the deployment set.

You can use the [DeleteDeploymentSet](../intl.en-US/API Reference/Deployment sets/DeleteDeploymentSet.md#) API operation to delete deployment sets.

