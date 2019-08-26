# Overview of configuration changes {#concept_anb_bbf_5db .concept}

You can change the configurations of an instance and its Internet bandwidth after it is created.

## Upgrade or downgrade instance configurations {#ChangeType .section}

You can only upgrade or downgrade the configurations of vCPU and memory \(that is, [instance type family](../../../../reseller.en-US/Product Introduction/Instance type families.md#)\) simultaneously by changing the instance type. Depending on the method of billing applied to your instance, you can change an instance type as follows:

-   Subscription:
    -   Upgrade: See [upgrade configurations](reseller.en-US/User Guide/Instances/Change configurations/Upgrade configurations of Subscription instances.md#). The new configurations take effect after you [restart the instance](reseller.en-US/User Guide/Instances/Restart an instance.md#) in the console or by using the [RebootInstance](../../../../reseller.en-US/API Reference/Instances/RebootInstance.md#) interface.
    -   Downgrade: See [renewsal for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#) . You can downgrade the configuration of an instance when you renew the instance. The new configuration takes effect after you [restart the instance](reseller.en-US/User Guide/Instances/Restart an instance.md#) in the ECS console within the first seven days of the new billing cycle.
-   Pay-As-You-Go: See [change configurations of Pay-As-You-Go instances](reseller.en-US/User Guide/Instances/Change configurations/Change configurations of Pay-As-You-Go instances.md#). You must stop the instance to use this feature.

    **Note:** Stopping an instance disrupts services. Exercise caution when performing this action.


## Adjust Internet bandwidth {#ChangeBandwidth .section}

You can adjust the Internet bandwidth of an instance. The methods vary according to your business needs and the billing method of the instance. The following table lists the methods.

|Billing method |Supports permanent upgrade?|Is it effective immediately? |Available feature |Description|
|:--------------|:--------------------------|:----------------------------|:-----------------|:----------|
|Subscription|Yes|Yes|[Upgrade configurations of Subscription instances](reseller.en-US/User Guide/Instances/Change configurations/Upgrade configurations of Subscription instances.md#)|Only applicable to VPC-Connected ECS instances to which no EIP addresses are attached, or classic network-connected ECS instances. The Internet and intranet IP addresses remain unchanged after you upgrade your configurations.|
|Subscription|Yes|Effective from next billing cycle|[Renew for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)|Adjust bandwidth in the new billing cycle. When the Internet bandwidth is set to 0 Mbit/s, the Internet IP address of a VPC-Connected instance is released in the new billing cycle, but that of a classic network-connected ECS instance is retained.|
|Pay-As-You-Go or Subscription|Yes|Yes|[Change EIP Internet bandwidth](reseller.en-US/User Guide/Instances/Change configurations/Change EIP Internet bandwidth.md#)|Only applicable to VPC-Connected instances to which [EIP addresses](https://partners-intl.aliyun.com/help/doc-detail/27714.htm) are bound. You can adjust the Internet bandwidth on an EIP address at any time.|

## Assign a public IP address {#AllocatePublicIp .section}

Assign a public IP address to an ECS instance while [creating it](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#). If you skip it, you can even assign after an ECS instance is created. However, the feature is only available for Subscription instances. For more information, see the following table.

|Feature|Is it effective immediately?|Description|
|:------|:---------------------------|:----------|
|[Upgrade configurations of Subscription instances](reseller.en-US/User Guide/Instances/Change configurations/Upgrade configurations of Subscription instances.md#)|Yes|Only applicable to VPC-Connected ECS instances to which no EIP addresses are attached, or classic network-connected ECS instances. Set the Internet bandwidth to a non-zero value to assign a public IP address.|
|[Renew for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)|Effective from next billing cycle|

