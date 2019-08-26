# Create deployment sets {#CreateDeploymentSet .task}

A deployment set is a strategy that controls the distribution of instances and enables you to design the disaster tolerance functionality and availability of the business as you create an instance.

You can use the deployment set to spread the Elastic Compute Service \(ECS\) instances involved in your business across different physical servers to guarantee high availability and disaster tolerance at the level of physical machines. For more information, see [Deployment sets](../intl.en-US/Product Introduction/Network and security/Deployment set.md#). This topic describes how to create a deployment set in the ECS management console. If you are an API user, you can use [CreateDeploymentSet](../intl.en-US/API Reference/Deployment sets/CreateDeploymentSet.md#).

1.  Log on to [ECS console](https://ecs.console.aliyun.com/). 
2.  Select a region. 
3.  In the left-side navigation pane, choose **Networks and Security** \> **Deployment Sets**. 
4.  On the Deployment Sets page, click **Create Deployment Set**. 
5.   On the Create Deployment Set page, enter a **Name** and **Description** for the deployment set. Currently, only **High availability** is supported for the **Strategy** option. For more information about the deployment set strategy, see [Deployment set strategy](../intl.en-US/Product Introduction/Network and security/Deployment set.md#). 

After creating a deployment set, you can perform the following tasks:

-   [Create an instance in the deployment set.](intl.en-US/User Guide/Deployment sets/Create an instance in the deployment set.md#)

-   Add an ECS instance to the deployment set:

    1.  Log on to the [ECS console](https://ecs.console.aliyun.com/).
    2.  In the left-side navigation pane, click **Instances**.
    3.  Select a region.
    4.  Locate the target instance, and make sure that the instance is in the **Stopped** or **Running**status.
    5.  In the **Actions** column, choose **More** \> **Instance Settings** \> **Change Deployment Set**.
    6.  In the Change Deployment Set dialog box that appears, select the target deployment set, and configure the **Force Change** settings:
        -   **Yes**: This option allows the system to move the instance to a new host and to restart the instance in the **Running** or **Stopped** status.
        -   **No**: This option does not allow the system to move the instance to a new host. Instead, the system only attaches the target deployment set to the current host machine. This may cause the change of deployment set to fail.
    7.  Click **OK**.

