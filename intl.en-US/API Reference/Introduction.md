# Introduction {#EcsApiWelcome .concept}

This topic provides the API reference of Alibaba Cloud Elastic Compute Service  \(ECS\). If you are familiar with Web service and one or more programming languages, we recommend that you use APIs to manage your ECS resources or develop applications.  For more information, see [API overview](reseller.en-US/API Reference/API overview.md#).

## Limits {#section_un5_qbh_vdb .section}

We set limits on the number and specification for the ECS instance, disk, security group, snapshot, and network bandwidth that you can create. For more information, see [Limits](../../../../reseller.en-US/User Guide/Limits.md#). Whenever the API description, optional parameter values, and available specifications conflict with the resource or specification limits described in the [Limits](../../../../reseller.en-US/User Guide/Limits.md#), the Limits topic always takes the precedence.

## Methods {#section_vn5_qbh_vdb .section}

We allow HTTP or HTTPS requests, and so are the methods GET or POST. You can make a request by using the following approaches:

-   \(Recommended\) Programming language-specific ECS [SDK](https://github.com/aliyun)

-   Alibaba Cloud CLI

-   Alibaba Cloud [API Explorer](https://api.aliyun.com/)

-   [API URL request](reseller.en-US/API Reference/Getting started/Request structure.md#)


In particular, you can skip the authentication process by using the SDK, CLI, and API Explorer.  It is easier for you to get started by using the language-specific SDK instead of making a request over HTTP or HTTPS.

**Note:** When you call API in the Alibaba Cloud CLI and SDK, remove the period \(.\) from the request parameters. For example, use `SystemDiskCategory` instead of `SystemDisk.Category`.

However, you must complete the authentication process for every request if you make an API URL request over the HTTP or HTTPS protocol. For more information, see [Digital signature](reseller.en-US/API Reference/Getting started/Digital signature.md#) and [Create an AccessKey](../../../../reseller.en-US/General Reference/Create an AccessKey.md#).

## Glossary { .section}

|Item|Abbreviation|Meaning|
|:---|:-----------|:------|
|Region|Region|A specific data center established by Alibaba Cloud in which you can run your business. To decrease network latency, we have linked the regions all over the world. However, the region cannot be changed once an ECS resource is create in it.|
|Availability Zone|Zone|Zone for short. An area with independent power grids and networks in a specified region. Each region has one or more zones. The network latency for ECS resources within a specific zone is reduced.|
|Instance|Instance|A virtual computing environment that includes CPU, memory, operating system, bandwidth, disks, and other basic computing components. An ECS instance is an independent virtual machine, and is the core element of ECS. For more information, see [Instance type families](../../../../reseller.en-US/Product Introduction/Instance type families.md#).|
|Image|Image|A running environment template for an instance. It includes an operating system and preinstalled software. You can use an image either to create an instance or change the system disk of an instance.|
|Disk|Disk|The storage device of instances.|
|Security group|Security group|An instance-related security group. An instance must belong to at least one security group. The security policies of a security group apply to all instances in the group.|
|Snapshot|Snapshot|A restore point created for a disk. It contains the disk data at a specified time and can be used to restore disk data or create custom images.|
|Tag|Tag|Consists of a key-value pair. You can assign tags to ECS resources for fast listing and filtering.|
|IP address|IP address|The Internet or intranet IP address of an instance.|

