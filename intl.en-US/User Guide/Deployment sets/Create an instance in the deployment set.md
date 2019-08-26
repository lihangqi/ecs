# Create an instance in the deployment set {#RunInstancesInDS .task}

Once you have an available deployment set, you can learn how to create instances in it by following this article.

Only seven instances can be created in a deployment set in one zone. The number of instances that can be created in a region is seven multiplied by the number of the zones. When you create an instance, you can use a launch template or use the bulk creation feature to avoid the inconvenience caused by the restriction of maximum instances per zone. This topic describes how to create an instance in a deployment set using the ECS console. If you are an API user, you can call [RunInstances](../intl.en-US/API Reference/Instances/RunInstances.md#) and specify the DeploymentSetId parameter in the request.

1.  Log on to [ECS console](https://ecs.console.aliyun.com/). 
2.  Select a region. 
3.  In the left-side navigation pane, choose **Networks and Security** \> **Deployment Sets**. 
4.   On the Deployment Sets page, locate the target deployment set. You can click **Create Instance** in the Actions column. Alternatively, you can also select the deployment set and then click **Create Instance** in the **Instances** list that appears. 
5.  In the page that appears, complete the instance configuration on the **Advanced Purchase** tab page. For more information about creating an instance, see [Create an instance by using the wizard](intl.en-US/User Guide/Instances/Create an instance/Create an instance by using the wizard.md#). You need to note these configurations: 
    -   **Basic configurations**:
        -   **Region**: The instance and the target deployment set must be in the same region.

        -   **Zone**: The maximum number of instances in each deployment set zone cannot exceed seven.

        -   **Instance**: The type families of the instance that can be created by the deployment set currently support c5, d1, d1ne, g5, hfc5, hfg5, i2, ic5, r5, se1ne, sn1ne, and sn2ne. For more information about instance types and performance, see [Instance type families](../intl.en-US/Product Introduction/Instance type families.md#).

        -   \(Optional\) You can specify the number of instances for the **Quantity** field, and you need to consider the number of instances that already exist in the current zone of the same deployment set.
    -   \(Optional\) **System Configuration** \> **Sequential Suffix**: After creating instances in bulk, you can add sequential suffixes to the Instance name and host name. The sequential suffix increments from 001 to 999.

    -   **Grouping** \> **Deployment Sets**: Select the target deployment set.

    -   \(Optional\) **Preview** \> **Save as launch template**: Saves the configuration as a launch template that you can use to quickly create an instance the next time. For more information, see [Instance launch template](../intl.en-US/Product Introduction/Instances/Launch templates.md#).

6.  Check the settings you have configured, and then click **Create Instance**. 
7.  In the left-side navigation pane, click **Deployment Sets**. You can view the deployment set that you have created. 

After creating an instance, you can perform the following tasks:

-   View and manage instances in the deployment set. For more information, see the related topics in the User Guide.

-   Move an instance between deployment sets:

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
    2.  In the left-side navigation pane, click **Instances**.
    3.  Select a region.
    4.  Locate the target instance, and make sure that the instance is in the **Stopped** or **Running**status.
    5.  In the **Actions** column, choose **More** \> **Instance Settings** \> **Change Deployment Set**.
    6.  In the Change Deployment Set dialog box that appears, select the target deployment set, and configure the **Force Change** settings:
        -   **Yes**: This option allows the system to move the instance to a new host and to restart the instance in the **Running** or **Stopped** status.
        -   **No**: This option does not allow the system to move the instance to a new host. Instead, the system only attaches the target deployment set to the current host machine. This may cause the change of deployment set to fail.
    7.  Click **OK**.

