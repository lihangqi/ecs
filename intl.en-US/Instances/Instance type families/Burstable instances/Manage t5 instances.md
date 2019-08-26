# Manage t5 instances {#concept_rwx_ll4_cfb .concept}

You can create t5 instances and change their running modes through the console or APIs.

## Create an instance {#section_v55_fx5_ydb .section}

You can create a t5 instance by referring to [Create an instance by using the wizard](../../../../../reseller.en-US/Instances/ECS instance life cycle/Create an instance/Create an instance by using the wizard.md#). When creating a t5 instance, note the following:

-   Network type: Only VPC is supported.

-   Image: 512 MiB is the minimum memory size for a t5 instance. The OS can only be a Linux variant or Windows Server 1709. Operating systems that require a minimum memory of 1 GiB, such as Windows Server 2016, are not supported. For more information about selecting images, see [How to select a system image](https://partners-intl.aliyun.com/help/faq-detail/40651.htm).

-   Running mode of t5 instances: Select the **Enable Unlimited Mode for t5 Instances** check box to create a t5 instance without performance constraints. If it is not selected, a t5 standard instance \(with performance constraints\) is created. You can change the mode after creating a t5 instance.


## Change the running mode of a t5 instance {#section_okz_ny4_cfb .section}

Within the lifecycle of a t5 instance, you can change its running mode through the console or the API [ModifyInstanceAttribute](../../../../../reseller.en-US/API Reference/Instances/ModifyInstanceAttribute.md#).

**Note:** A t5 instance must be in a **Running** state \(`Running`\) status before you can change its mode.

Follow the steps below to change the running mode in the console:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  In the list of instances, find the target instance, and click the instance ID.
5.  In the **Basic Information** part of the Instance details page, click **More**, and then select **Enable Unlimited Mode**. You can also select **Disable Unlimited Mode** to return to the standard mode.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21272/155115154312028_en-US.png)


The following table describes how the running mode of a t5 instance changes according to the operations or its payment status.

|Operation/status|Results|
|:---------------|:------|
|Stop an instance|After restart, t5 instances that are not charged after being stopped will run in the standard mode \(with performance constraints\), while t5 instances that are still charged after being stopped will run in the same mode as before.|
|Restart an instance|After restart, the running mode remains unchanged.|
|Payment failed|The running mode changes to the standard mode. The original mode is restored after the payment is made successfully.|

## View CPU utilization and CPU credits {#section_imz_wx5_ydb .section}

In the ECS console, you can view the CPU information about an instance, such as CPU utilization, consumed CPU credits, accrued CPU credits, excess CPU credits, and advance CPU credits.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  In the instance list, find the target instance and click the instance ID. Alternatively, you can click **Manage** in the **Actions** column.
5.  View the metrics in the **Monitoring Information** area of the Instance Details page.

You can also view the CPU utilization after connecting to an instance remotely:

-   Windows: [Connect to an instance](../../../../../reseller.en-US/Instances/ECS instance life cycle/Connect to instances/Connect to a Windows instance.md#), and then view the CPU utilization in the **Task Manager**.
-   Linux: [Connect to an instance](../../../../../reseller.en-US/Instances/ECS instance life cycle/Connect to instances/Connect to a Linux instance by using a password.md#), and then run the `top` command to view the CPU utilization.

## Change an instance type {#section_ej2_xm4_cfb .section}

In the ECS console, if you find that the CPU utilization remains at the baseline performance level for a long period of time or rarely exceeds the baseline level, your instance type may not meet your needs or may exceed your needs. In either case, you may consider changing the instance type.

You can change the instance type based on the billing method:

-   Subscription instances: You can change the instance type by [upgrading or downgrading instance configurations](../../../../../reseller.en-US/Instances/Change configurations/Overview of configuration changes.md#).
-   Pay-As-You-Go instances: You can change the configurations by [changing the instance type](../../../../../reseller.en-US/Instances/Change configurations/Change configurations of Pay-As-You-Go instances/Change configurations of Pay-As-You-Go instances.md#).

For information about supported instance type families, see [Instance type families that support upgrading instance types](../../../../../reseller.en-US/Instances/Change configurations/Instance type families that support instance type upgrades.md#).

