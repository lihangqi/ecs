# Manage t5 instances {#concept_rwx_ll4_cfb .concept}

You can use the console or the API to create t5 instances and change their instance types.

## Create an instance {#section_v55_fx5_ydb .section}

You can create a t5 instance following [creating an instance by using the wizard](../../../../reseller.en-US/User Guide/Instances/Create an instance/Create an instance by using the wizard.md#). When creating a t5 instance, consider the following settings:

-   Network type: Only VPC is supported.

-   Image: 512 MiB is the minimum memory size for a t5 instance, and you can select only the Linux or Windows Server 1709 operating system. Operating systems that require a minimum memory of 1 GiB, such as Windows Server 2016, are not supported. For more information about selecting images, see [how to select a system image](https://partners-intl.aliyun.com/help/faq-detail/40651.htm).

-   t5 instance type: Select the **Enable Unlimited Mode for T5 Instances** check box to create a t5 instance without performance constraints. If it is not selected, a t5 standard instance is created. You can change the mode after creating a t5 instance.


## Change the running mode of a t5 instance {#section_okz_ny4_cfb .section}

Within the lifecycle of a t5 instance, you can change its running mode between **Standard** and U**nlimited** in real time through the console or the API [ModifyInstanceAttribute](../../../../reseller.en-US/API Reference/Instances/ModifyInstanceAttribute.md#).

**Note:** The t5 instance must be in a **Running** state \(`Running`\) before you can change its mode.

Follow the steps below to change the running mode in the console:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  In the list of instances, find the target instance, and click the instance ID.
5.  In the **Basic Information** part of the Instance details page, click **More**, and then select **Switch credit specification mode** to change to the "Unlimited" mode. You can select **Switch credit specification mode** again to change back to the "Standard" mode.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21272/154259850212028_en-US.png)


The following table describes how the running mode of a t5 instance changes according to the operations or its payment status:

|Operation/status|Results|
|:---------------|:------|
|Stop the instance|The default mode is "Standard" after it is started again.|
|Reboot the instance|The running mode remains unchanged after the reboot.|
|Payment failed|The running mode changes to "Standard". The original mode is restored after the payment is successful.|

## View CPU utilization and CPU credits {#section_imz_wx5_ydb .section}

In the ECS console, you can view the CPU information about an instance such as CPU utilization, consumed CPU credits, accrued CPU credits, excess CPU credits, and advance CPU credits.

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  In the instance list, find the target instance. Then click the instance ID or click **Manage** in the **Actions** column.
5.  View the metrics in the **Monitoring Information** area of the Instance Details page.

You can also view the CPU usage after connecting to the instance remotely:

-   Windows: [Connect to the instance](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#), and then view the CPU usage in the **Task Manager**.
-   Linux: [Connect to the instance](../../../../reseller.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#), and then run the `top` command to view the CPU usage.

## Change the instance type {#section_ej2_xm4_cfb .section}

In the ECS console, if you find that the CPU usage remains at the baseline performance level for a long period of time or rarely exceeds the baseline level, your instance type may not meet your needs or may exceed your needs. In either case, you may consider changing the instance type.

You can change the instance type based on the billing method:

-   Subscription instances: You can change the instance type by [upgrading or downgrading instance configurations](../../../../reseller.en-US/User Guide/Instances/Change configurations/Overview of configuration changes.md#).
-   Pay-As-You-Go instances: You can change the configurations by [changing the instance type](../../../../reseller.en-US/User Guide/Instances/Change configurations/Change configurations of Pay-As-You-Go instances.md#).

For the target instance type families, see [instance type families that support upgrading instance types](../../../../reseller.en-US/User Guide/Instances/Change configurations/Instance type families that support instance type upgrades.md#).

