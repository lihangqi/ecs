# Overview of configuration changes {#concept_anb_bbf_5db .concept}

You can change the configurations of an instance and its Internet bandwidth after the instance is created.

## Upgrade or downgrade instance configurations {#ChangeType .section}

You must upgrade or downgrade the configurations of vCPUs and memory simultaneously by changing the instance type \([instance type family](../../../../reseller.en-US/Instances/Instance type families.md#)\). The following table provides the configuration change methods suitable for the billing method applied to your instance.

**Note:** Before changing instance configurations, you need to check [instance type families that support instance type upgrades](reseller.en-US/Instances/Change configurations/Instance type families that support instance type upgrades.md#) and confirm the target configuration supported by a specific instance type family.

|Billing method|Configuration upgrade method|How does the change take effect?|Configuration downgrade method|How does the change take effect?|
|:-------------|:---------------------------|:-------------------------------|:-----------------------------|:-------------------------------|
|Subscription|[Upgrade configurations of Subscription instances](reseller.en-US/Instances/Change configurations/Upgrade configurations/Upgrade configurations of Subscription instances.md#)|The new configurations take effect after you [restart the instance](reseller.en-US/Instances/Manage instances/Restart an instance.md#) in the ECS console or by calling the API action [RebootInstance](../../../../reseller.en-US/API Reference/Instances/RebootInstance.md#).| -   [Renew for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)
-   [On-demand configuration downgrade](reseller.en-US/Instances/Change configurations/Downgrade configurations/Downgrade configurations of Subscription instances.md#) \(Whether this feature is supported is determined by your ECS instance resource usage.\)

 | -   Renew for configuration downgrade: The new configurations take effect after you [restart the instance](reseller.en-US/Instances/Manage instances/Restart an instance.md#) in the ECS console within the first seven days of the new billing cycle.
-   On-demand configuration downgrade: The new configurations take effect after you restart the instance in the ECS console or by calling the API action[RebootInstance](../../../../reseller.en-US/API Reference/Instances/RebootInstance.md#).

 |
|Pay-As-You-Go|[Change configurations of Pay-As-You-Go instances](reseller.en-US/Instances/Change configurations/Change configurations of Pay-As-You-Go instances/Change configurations of Pay-As-You-Go instances.md#)|The new configurations take effect after you restart the instance.|[Change configurations of Pay-As-You-Go instances](reseller.en-US/Instances/Change configurations/Change configurations of Pay-As-You-Go instances/Change configurations of Pay-As-You-Go instances.md#)|The new configurations take effect after you restart the instance.|

## Adjust Internet bandwidth {#ChangeBandwidth .section}

You can adjust the Internet bandwidth of an instance. The methods vary according to your business needs and the billing method of the instance. The following table lists the methods.

|Billing method|Supports permanent upgrade?|Does the change take effect immediately?|Feature|Description|
|:-------------|:--------------------------|:---------------------------------------|:------|:----------|
|Subscription|Yes|Yes|[Upgrade configurations of Subscription instances](reseller.en-US/Instances/Change configurations/Upgrade configurations/Upgrade configurations of Subscription instances.md#)|Only applicable to VPC-connected ECS instances to which no EIP addresses are attached or classic network-connected ECS instances. The public and private IP addresses remain unchanged after you increase Internet bandwidth of the instance.|
|Subscription|Yes|Effective from next billing cycle|[Renew for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)|You can adjust the Internet bandwidth when you renew the instance. When the Internet bandwidth is reduced to 0 Mbit/s, the public IP address of a VPC-connected instance is released in the new billing cycle, but the public IP address of a classic network-connected ECS instance is retained.|
|Pay-As-You-Go or Subscription|Yes|Yes|[Change EIP Internet bandwidth](reseller.en-US/Instances/Change configurations/Change configurations of Pay-As-You-Go instances/Change EIP Internet bandwidth.md#)|Only applicable to VPC-connected instances to which [EIP addresses](https://partners-intl.aliyun.com/help/doc-detail/27714.htm) are attached. You can adjust the Internet bandwidth on an EIP address at any time during the current lifecycle of the instance.|

## Assign a public IP address {#AllocatePublicIp .section}

You can assign a public IP address to an ECS instance when you create the instance. If no public IP addresses are assigned at instance creation, you can assign a public IP address after an ECS instance is created \(the instance must be a Subscription instance\). For more information, see the following table.

|Feature|Does the change take effect immediately?|Description|
|:------|:---------------------------------------|:----------|
|[Upgrade configurations of Subscription instances](reseller.en-US/Instances/Change configurations/Upgrade configurations/Upgrade configurations of Subscription instances.md#)|Yes|Only applicable to VPC-connected ECS instances to which no EIP addresses are attached, or classic network-connected ECS instances. Set the Internet bandwidth to a non-zero value to assign a public IP address.|
|[Renew for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)|Effective from next billing cycle|

