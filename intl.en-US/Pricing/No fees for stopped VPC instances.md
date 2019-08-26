# No fees for stopped VPC instances {#concept_js1_1fd_5db .concept}

For Pay-As-You-Go VPC instances, you can enable the feature of no fees for stopped instances. After this feature is enabled, vCPUs, memory, and Internet addresses will incur no fees when a VPC instance is stopped, but the cloud disks are still charged.

## Definition {#section_kvc_4qk_zdb .section}

The **No fees for stopped instances \(VPC-Connected\)** feature means you do not have to pay for the vCPUs, memory, and Internet addresses of a Pay-As-You-Go VPC instance that is stopped in the [ECS console](../reseller.en-US/Instances/Manage instances/Start or stop an instance.md#), by using the [StopInstance](../reseller.en-US/API Reference/Instances/StopInstance.md#) API, or by using [Alibaba Cloud CLI](https://partners-intl.aliyun.com/help/product/29991.htm). Its cloud disks, however, are still charged.

## Description of applicability {#section_lvc_4qk_zdb .section}

-   This feature applies to the following conditions. In other words, resources that meet the following conditions are **not charged**.

    |Item|Description|
    |:---|:----------|
    |Billing method|Pay-As-You-Go|
    |Network type|VPC|
    |Resources|vCPUs, memory, and Internet addresses \(released for a stopped VPC instance\)|

    **Note:** If you stop an instance in the ECS console, by using the API, or by using Alibaba Cloud CLI, vCPUs and memory of the instance are not billed. But if you stop an instance in its OS, the instance is still billed even if the feature is enabled.

-   This feature does not apply to the following conditions. In other words, resources that meet the following conditions are **charged**.

    |Item|Description|
    |:---|:----------|
    |Local-disk instances|All instances with local disks, including but not limited to the d1, d1ne, ga1, gn5, i1 and i2 instance type families.|
    |Cloud disks attached to the instances \(including system disks and data disks\), elastic IP \(EIP\) addresses, bandwidth, and images|After this feature is enabled, billing of these resources continues when the instance is in the **No Fees for Stopped Instances \(VPC-Connected\)** mode. For more information about billing, see [Pay-As-You-Go](reseller.en-US/Pricing/Pay-As-You-Go.md#), cloud disk pricing, [billing of network bandwidth](reseller.en-US/Pricing/Billing of Internet bandwidth.md#), bandwidth pricing, and [EIP pricing](../../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#).|
    |Instances being started|New Pay-As-You-Go VPC instances that are entering the **Running** status \(`Running`\) from the **Stopped** status \(`Stopped`\) during their first startup. You can create such instances in the [ECS console](../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#) or by using the [CreateInstance](../reseller.en-US/API Reference/Instances/CreateInstance.md#) API.|
    |Instances that are stopped due to overdue payment|In this case, billing also stops. The computing resources and Internet addresses are released too. Billing of all resources resumes after your instance is successfully [reactivated](../reseller.en-US/Instances/Manage instances/Reactivate an instance.md#).|
    |Pay-As-You-Go instances in classic networks|After such an instance enters the **Stopped** status, Alibaba Cloud continues to bill the instance and its related resources. The Internet and private IP addresses of the instance remain unchanged after the instance is restarted.|


## Impacts {#section_qvc_4qk_zdb .section}

This feature has the following impacts on your instance when it is enabled and the instance is stopped:

-   The vCPU and memory are released, so you may be unable to start your instance next time. If this happens, try again after some time. You can also try again after [changing configurations of Pay-As-You-Go instances](../reseller.en-US/Instances/Change configurations/Change configurations of Pay-As-You-Go instances/Change configurations of Pay-As-You-Go instances.md#).

-   If the instance is assigned an Internet address, the address is released. After you start your instance in the [ECS console](../reseller.en-US/Instances/Manage instances/Start or stop an instance.md#) or by using the [StartInstance](../reseller.en-US/API Reference/Instances/StartInstance.md#) API, your instance is assigned a new Internet address. However, its private IP address remains unchanged.

    **Note:** If you do not want to change the Internet address, you can stop the instance after [converting the Internet address to an EIP address](../reseller.en-US/Network/Change IPv4 addresses/Convert public IP address to EIP address.md#).

-   When a burstable performance instance is stopped, the existing CPU credits are valid but credit accrual stops. When it starts, CPU credits continue to accrue. For more information, see [Overview of burstable performance instances](../reseller.en-US/Instances/Instance type families/Burstable performance instances/Overview.md#).


For such operations as [replace the system disk](../reseller.en-US/Block Storage/Block storage/Change the operating system/Replace the system disk by using a public image.md#) \([ReplaceSystemDisk](../reseller.en-US/API Reference/Disk/ReplaceSystemDisk.md#)\), [roll back a disk](../reseller.en-US/Block Storage/Block storage/Roll back a cloud disk.md#) \([ResetDisk](../reseller.en-US/API Reference/Disk/ResetDisk.md#)\), [reinitialize a disk](../reseller.en-US/Block Storage/Block storage/Reinitialize a cloud disk/Reinitialize a cloud disk.md#) \([ReInitDisk](../reseller.en-US/API Reference/Disk/ReInitDisk.md#)\), you need to stop the instance and restart it in a short time. You can perform any of the following actions to make sure that your instance starts successfully:

-   Log on to the ECS console. On the Overview page, turn off **No Fees for Stopped Instances \(VPC-Connected\)**. For more information, see [Disable the feature](#).
-   Log on to the ECS console. When you stop an instance, select the **Keep Instance with Fees** check box.
-   If you are using APIs or Alibaba Cloud CLI, set `StoppedMode = KeepCharging` in the [StopInstance](../reseller.en-US/API Reference/Instances/StopInstance.md#) API.

## Enable the feature {#default .section}

Method 1: Enable the feature for all instances

You must manually enable the **No fees for stopped instances \(VPC-Connected\)** feature. Once the feature is enabled, it applies to all Pay-As-You-Go VPC instances in all the regions under your account. If the feature is enabled and you want to keep fees for a Pay-As-You-Go VPC instance when you stop it, you can select the **Keep Instance with Fees** option when you stop the instance.

**Note:** If you already have one or more Pay-As-You-Go VPC instances in use, this feature is not automatically enabled. After you fully understand and confirm that the feature does not result in uncontrollable impacts on your systems or applications, you can log on to the ECS console to enable it.

To enable the **No fees for stopped instances \(VPC-Connected\)** feature, follow these steps:

1.  In the left-side navigation pane, click **Overview**.
2.  In the **Common Settings** area, click **Custom Settings**.
3.  Toggle **No Fees for Stopped Instances \(VPC-Connected\)** on, read the note in the displayed box, and then click **OK**.
4.  Click **OK**.

Method 2: Enable the feature for a single instance

When you [stop a single instance](../reseller.en-US/Instances/Manage instances/Start or stop an instance.md#), select the **No Fees for stopped instances \(VPC-Connected\)** check box in the displayed box.

## Disable the feature {#disable .section}

Method 1: Disable the feature for all instances

**Note:** After this feature is disabled:

-   This operation takes effect for all the Pay-As-You-Go VPC instances in all the regions under your account. Please proceed with caution.
-   For an instance that is **Stopped** \(`Stopped`\), it is still not billed if the **Stop mode** is **No fees for stopped instances**. After it is started,

    -   A new Internet address is assigned if it had one before it was stopped.
    -   The EIP address remains unchanged if it is not unbound before the instance was stopped.

To disable the feature, follow these steps:

1.  In the left-side navigation pane, click **Overview**.
2.  In the **Common Settings** area, click **Custom Settings**.
3.  Toggle **No Fees for Stopped Instances \(VPC-Connected\)** off, read the note in the displayed box, and then click **OK**.
4.  Click **OK**.

Method 2: Disable the feature for a single instance

When you [stop an instance](../reseller.en-US/Instances/Manage instances/Start or stop an instance.md#), select the **Keep Instance with Fees** check box in the displayed box.

