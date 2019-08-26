# No fees for stopped instances \(VPC-Connected\) {#concept_js1_1fd_5db .concept}

## Overview {#section_kvc_4qk_zdb .section}

The No fees for stopped instances \(VPC-Connected\) feature means you do not have to pay for a VPC-Connected Pay-As-You-Go instance after you stop it either in the ECS console, by using the StopInstance interface, or by using Alibaba Cloud CLI.

**Note:** If you stop the instance in other ways, for example, in the OS, the instance is still billed even if the No fees for stopped instances \(VPC-Connected\) feature is enabled.

## Applicable resources {#section_lvc_4qk_zdb .section}

The No fees for stopped instances \(VPC-Connected\) feature is only applicable to VPC-Connected Pay-As-You-Go instances.

This No fees for stopped instances \(VPC-Connected\) feature is not applicable to the following ECS resources:

-   All instances with local disks, including but not limited to d1ne, d1, i2, i1, gn5, and ga1 instances.

-   Cloud disks attached to the instances \(including system disks and data disks\), Internet bandwidth, elastic IP \(EIP\) addresses, and images. After the **No fees for stopped instances \(VPC-Connected\)** feature is enabled, billing of these resources continues when the instance is stopped. For more information about billing, see [Pay-As-You-Go](intl.en-US/Pricing/Pay-As-You-Go.md#), [Cloud disk pricing](https://www.alibabacloud.com/product/ecs), [Billing of network bandwidth](intl.en-US/Pricing/Billing of network bandwidth.md#), [Bandwidth pricing](https://www.alibabacloud.com/product/ecs), and [EIP pricing](../../../../intl.en-US/.md#).

-   New VPC-Connected Pay-As-You-Go instances that are in a **Stopped** status after they are created, but before they enter a **Running** status.

-   Instances that are stopped because of overdue payment. In this case, billing also stops. The computing resources and public IP address will be released too. You can [reactivate your instance](../../../../intl.en-US/User Guide/Instances/Reactivate an instance.md#) and its related resources only after the overdue payment is cleared. Billing of all resources resumes after your instance is successfully reactivated.

-   Pay-As-You-Go instances in classic networks. After such an instance enters the **Stopped** status, Alibaba Cloud continues to bill the instance and its related resources. The public and private IP addresses of the instance remain unchanged after the instance is started.


## Other effects {#section_qvc_4qk_zdb .section}

The **No fees for stopped instances \(VPC-Connected\)** feature has the following effects on your instance when the feature is enabled and the instance is stopped:

-   The CPU and RAM are released, so you may be unable to start your instance next time. If this happens, try again after some time.

-   If the instance has been assigned a public IP address, the address is released. After you [start your instance](../../../../intl.en-US/User Guide/Instances/Start or stop an instance.md#) in the ECS console or by using the [StartInstance](../../../../intl.en-US/API Reference/Instances/StartInstance.md#) interface, your instance is assigned a new public IP address. However, its private IP address remains unchanged.

-   When a t5 instance is stopped, the existing CPU credits are valid but credit accumulation stops. When it starts, CPU credits continue to accumulate.


When you perform the following operations, the instance must be in a stopped status until the operation is complete:

-   [Replace the system disk](../../../../intl.en-US/User Guide/Cloud disks/Replace the system disk (public image).md#) \([ReplaceSystemDisk](../../../../intl.en-US/API Reference/Disk/ReplaceSystemDisk.md#)\)
-   [Roll back a disk](../../../../intl.en-US/User Guide/Cloud disks/Roll back a cloud disk.md#) \([ResetDisk](../../../../intl.en-US/API Reference/Disk/ResetDisk.md#)\)
-   [Reinitialize a disk](../../../../intl.en-US/User Guide/Cloud disks/Reinitialize a cloud disk.md#) \([ReInitDisk](../../../../intl.en-US/API Reference/Disk/ReInitDisk.md#)\)
-   Other O&M operations

You can perform any of the following actions to make sure that your instance starts successfully:

-   Log on to the [ECS console](https://ecs.console.aliyun.com/#/home) to disable the **No fees for stopped instances \(VPC-Connected\)** feature. For more information about the procedure, see [Disable the feature](#disable).

-   If you are using APIs or Alibaba Cloud CLI, set `StoppedMode = KeepCharging` in the [StopInstance](../../../../intl.en-US/API Reference/Instances/StopInstance.md#) interface.


## Enable the feature {#default .section}

You must manually enable the **No fees for stopped instances \(VPC-Connected\)** feature. Once the feature is enabled, it applies to all VPC-Connected Pay-As-You-Go instances in all the regions under your account.

If the feature is enabled and you want to keep fees for a VPC-Connected Pay-As-You-Go instance when you stop it, you can select the **Keep Instance with Fees** option when you stop the instance.

If you already have one or more VPC-Connected Pay-As-You-Go instances in use, this feature is not automatically enabled.

To enable the feature, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
2.  In the left-side navigation pane, click **Overview**.
3.  In the upper-right corner of the **Overview** page, click **Settings**.
4.  Toggle **Enable "No Fees for Stopped Instances" for VPC-Connected Instances in All Regions**, read the note in the dialog box, and then click **No Fees for stopped instances \(VPC-Connected\)**.
5.  Click **OK**.

After the feature is enabled, you can disable it as needed. For more information, see [Disable the feature](#).

## Disable the feature {#disable .section}

You can disable the **No fees for stopped instances \(VPC-Connected\)** feature as needed. This operation takes effect for all the VPC-Connected Pay-As-You-Go instances in all the regions under your account, and so you should proceed with caution.

After the feature is disabled:

-   The VPC-Connected Pay-As-You-Go instances in all the regions under your account are still billed even after they are stopped.

-   An instance currently in a **Stopped** status is not billed. After it is started:

    -   A new public IP address is assigned if it had one before it was stopped.
    -   The EIP address remains unchanged if it is not unbound before the instance was stopped.
-   When an instance enters a newly **Stopped** status:

    -   The instance is still billed.
    -   If it has been assigned a public IP address, the address is retained and remains unchanged.

To disable the feature, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
2.  In the left-side navigation pane, click **Overview**.
3.  In the upper-right corner of the **Overview** page, click **Settings**.
4.  Disable **Enable "No Fees for Stopped Instances" for VPC-Connected Instances in All Regions**, read the note in the dialog box, and then click **I Agree**.
5.  Click **OK**.

