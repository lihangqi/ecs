# Deployment set {#DeploymentSet .concept}

A deployment set is a strategy that controls the distribution of instances and enables you to design the capacity and availability of disaster tolerance as you create an instance.

## Deployment strategy {#Strategy .section}

You can use the deployment set to spread the Elastic Compute Service \(ECS\) instances involved in your business across different physical servers to guarantee high availability and capacity for low-level disaster tolerance of the business. When you create an instance in a deployment set, we start the instances separately in the specified regions based on the deployment strategy that you set up. If you have not created a deployment set for the instance, we start instances on different physical servers to ensure the availability of services as much as possible.

Currently, deployment sets support the **high availability** strategy:

-   When you use the high availability strategy, all ECS instances within the deployment set are strictly distributed across different physical servers in the specified region. The high availability strategy applies to application architectures where several ECS instances need to be isolated from each other. The strategy significantly reduces the chances of service being unavailable.

-   Using the high availability strategy, you may not be able to create an ECS instance when you encounter a supply shortage in the region. What's more, a Pay-As-You-Go instance of [no termination fees](../../../../intl.en-US/Pricing/No fees for stopped VPC instances.md#) can cause a restart failure. We recommend that you wait a while and then create or restart an instance again.


## Deployment example {#Example .section}

The following figure is a typical example of improving business reliability with the deployment set, where your four ECS instances are distributed on four different physical servers.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/21423/154382111812046_en-US.png)

If you want to achieve low latency communication between the instances of the deployment set, we recommend that you make sure the network types of the instances are the same. For example, when creating instances, select the same VPC for those instances.

## Billing details {#Billing .section}

No service fees will be charged when you use the deployment set. Your consumption details include only the instances, disks, images, and bandwidth that you are using. For more information, see [Pricing overview](../../../../intl.en-US/Pricing/Pricing overview.md#).

## Limits {#Cautions .section}

Before you use the deployment set, note that:

-   Merging deployment sets is not supported.

-   [Preemptable instances](intl.en-US/Product Introduction/Instances/Preemptible instance.md#) cannot be created in the deployment set.

-   [Dedicated hosts](../../../../intl.en-US/Product Introduction/What is a Dedicated Host.md#) cannot be created in the deployment set.

-   When you create an instance in a deployment set, you can create a maximum of seven ECS instances in one zone. The number of ECS instances that can be created under an Alibaba Cloud region is seven multiplied by the number of zones.

-   The instance type families that can be created in the deployment set includes c5, d1, d1ne, g5, hfc5, hfg5, i2, ic5, r5, se1ne, sn1ne, and sn2ne. For more information about instance types and their performance, see [Instance type families](intl.en-US/Product Introduction/Instance type families.md#).

-   You may fail to create an instance or restart a Pay-As-You-Go instance with no termination fees in the deployment set due to a supply shortage.


## Related operations {#Operations .section}

**Console operations**

-   [Create a deployment set](../../../../intl.en-US/User Guide/Deployment sets/Create deployment sets.md#)

-   [Create ECS instances in a deployment set](../../../../intl.en-US/User Guide/Deployment sets/Create an instance in the deployment set.md#)

-   [Modify the deployment set where the instance is located](../../../../intl.en-US/User Guide/Deployment sets/Create an instance in the deployment set.md#)

-   [Manage deployment sets](../../../../intl.en-US/User Guide/Deployment sets/Manage deployment sets.md#)


**API operations**

-   Create a deployment set: [CreateDeploymentSet](../../../../intl.en-US/API Reference/Deployment sets/CreateDeploymentSet.md#)

-   Add an instance to a deployment set, or move an instance from one deployment set to another: [ModifyInstanceDeployment](../../../../intl.en-US/API Reference/Deployment sets/ModifyInstanceDeployment.md#)

-   Modify deployment set properties: [ModifyDeploymentSetAttributes](../../../../intl.en-US/API Reference/Deployment sets/ModifyDeploymentSetAttributes.md#)

-   Query deployment sets: [DescribeDeploymentSets](../../../../intl.en-US/API Reference/Deployment sets/DescribeDeploymentSets.md#)

-   Delete deployment sets: [DeleteDeploymentSet](../../../../intl.en-US/API Reference/Deployment sets/DeleteDeploymentSet.md#)


