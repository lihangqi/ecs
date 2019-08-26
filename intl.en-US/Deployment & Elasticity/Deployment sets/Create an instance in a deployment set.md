# Create an instance in a deployment set {#RunInstancesInDS .task}

This topic describes how to create an instance in a deployment set by using the ECS console.

A maximum of seven instances can be created for a deployment set in a zone. The number of instances that can be created in a region is seven multiplied by the number of zones. When you create an instance, you can use a launch template or use the bulk creation feature to facilitate instance creation.

You can also call the API action [RunInstances](../reseller.en-US/API Reference/Instances/RunInstances.md#) and specify the DeploymentSetId parameter in the request to complete this task.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Deployment Sets**.
3.  In the upper-left corner, select the target region. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/123261/156341327350161_en-US.png)

4.  On the Deployment Sets page, find the target deployment set and click **Create Instance** in the **Actions** column. Alternatively, you can click the deployment set and then click **Create Instance** in the **Instances** list that is displayed.![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21509/156341327312127_en-US.png)


5.  On the displayed page, complete the instance configuration on the **Custom Launch** tab page. For more information, see [Create an instance by using the wizard](reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#). Note the following configurations when you create an instance: 
    -   **Basic configurations** 
        -   **Region**: The instance and the target deployment set must be in the same region.

        -   **Zone**: A maximum of seven instances can be created for a deployment set in a zone.

        -   **Instance Type**: Only instances of the following types can be created by using the deployment set: c5, d1, d1ne, g5, hfc5, hfg5, i2, ic5, r5, se1ne, sn1ne, and sn2ne. For information about instance types and their performance, see [Instance type families](../reseller.en-US/Instances/Instance type families.md#).

        -   \(Optional\) **Purchased Instances**: You can specify the number of instances you want to create. This configuration must be based on the number of instances that already exist in the current zone of the same deployment set.
    -   **System configurations** 

        \(Optional\) After creating instances in bulk, you can add sequential suffixes to the instance name and host name. The sequential suffix ranges from 001 to 999.

    -   **Grouping** 

        **Deployment Set**: Select the target deployment set.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21509/156341327412135_en-US.png)

    -   **Preview** 

        \(Optional\) **Save as Launch Template**: You can save your configurations as a launch template that you can use to quickly create an instance the next time. For more information, see [Instance launch template](../reseller.en-US/Deployment & Elasticity/Launch template/Launch templates.md#).

6.  Check the settings you have made, and then click **Create Instance**.
7.  In the left-side navigation pane, choose **Deployment & Elasticity** \> **Deployment Sets** to view the deployment set that you have created.

After creating an instance, you can perform the following tasks:

-   View and manage instances in the deployment set. For more information, see instance-related topics.


