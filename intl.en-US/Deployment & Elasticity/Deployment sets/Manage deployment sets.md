# Manage deployment sets {#ManageDS .concept}

After creating a deployment set, you can modify the deployment set name and description, or remove deployment sets that are no longer required to ensure that the usage limit is not exceeded.

## Edit deployment set information {#ModifyAttributes .section}

To change the name or description of a deployment set in the ECS console, follow these steps:

1.  Find the deployment set that needs to be modified.
2.  Edit the information using either of the following methods:
    -   Hover the cursor over the **Deployment Set Name** column, click the ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21512/156620114912136_en-US.png) icon that appears, and then enter the deployment set name and description.
    -   In the **Actions** column of the target deployment set, click **Modify Information**, and enter the deployment set name and description.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21512/156620114912138_en-US.png)

3.  Click **OK**.

You can also call the [ModifyDeploymentSetAttributes](../intl.en-US/API Reference/Deployment sets/ModifyDeploymentSetAttribute.md#) API operation to modify the deployment set name and description.

## Delete deployment sets {#DeleteDS .section}

**Note:** If a deployment set already includes an instance, you cannot delete the deployment set.

To delete one or more deployment sets in the ECS console, follow these steps:

1.  Select one or more deployment sets that need to be deleted, hover the cursor over the **Actions** menu, and then click **Delete**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21512/156620114912139_en-US.png)

2.  Click **OK** to delete the deployment set.

You can use the [DeleteDeploymentSet](../intl.en-US/API Reference/Deployment sets/DeleteDeploymentSet.md#) API operation to delete deployment sets.

