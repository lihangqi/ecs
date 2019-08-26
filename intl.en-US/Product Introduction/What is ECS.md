# What is ECS {#concept_rhf_xgv_tdb .concept}

This article gives a brief introduction to what ECS is, and the resources and services that it involves.

Elastic Compute Service \(ECS\) is a type of computing service that features elastic processing capabilities. ECS has a simpler and more efficient management mode than physical servers. You can create instances, change the operating system, and add or release any number of ECS instances at any time to fit your business needs. An ECS instance is a virtual computing environment that includes CPU, memory, and other basic computing components. An instance is the core component of ECS and is the actual operating entity offered by Alibaba Cloud. Other resources, such as disks, images, and snapshots, can only be used in conjunction with an ECS instance.

Use the [ECS Learning Path](https://www.alibabacloud.com/getting-started/learningpath/ecs) as a mentor to become an ECS expert!

The following figure illustrates the concept of an ECS instance. You can use the [ECS console](https://ecs.console.aliyun.com/#/home) to configure the instance type, disks, operating system, and other affiliated resources for your ECS instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9543/4795_en-US.png)

## Basic concepts {#section_jkn_4qj_ydb .section}

Know the basic concepts before you proceed to use ECS:

-   [Region and zone](https://www.alibabacloud.com/help/doc-detail/40654.htm): A physical location where a data center is located.
-   [ECS instance](intl.en-US/Product Introduction/Instance/What are ECS instances.md#): A virtual computing environment that includes CPU, memory, operating system, bandwidth, disks, and other basic computing components.
-   [Instance type](intl.en-US/Product Introduction/Instance type families.md#): The specification of an ECS instance, including the number of vCPU cores, memory, networking performance. An instance type determines the compute capability of an ECS instance.
-   [Images](intl.en-US/Product Introduction/Images.md#): A running environment template for ECS instances. It generally includes an operating system and preinstalled software.
-   [Block storage](intl.en-US/Product Introduction/Block storage/What is block storage.md#): Block level storage products for your ECS, including [Elastic block storage](intl.en-US/Product Introduction/Block storage/Elastic block storage.md#) based on the distributed storage architecture and [local disks](intl.en-US/Product Introduction/Block storage/Local disks.md#) located on the physical server that an ECS instance is hosted on.
-   [Snapshots](intl.en-US/Product Introduction/Snapshots/What are ECS snapshots.md#): A copy of data on an elastic block storage device at a given time point.
-   [Network types](intl.en-US/Product Introduction/Network and security/Network types.md#): Alibaba Cloud provides two network types, including
    -   Virtual Private Cloud \(VPC\): A private network established in Alibaba Cloud. VPCs are logically isolated from other virtual networks in Alibaba Cloud. For more information, see [What is VPC](../../../../intl.en-US/VPC product introduction/What is VPC.md#).
    -   Classic network: A network majorly deployed in the public infrastructure of Alibaba Cloud.
-   [Security groups](intl.en-US/Product Introduction/Network and security/Security groups.md#): A logical group that groups instances in the same region with the same security requirements and mutual trust. A security group works as a virtual firewall for the ECS instances inside it.
-   [SSH key pairs](intl.en-US/Product Introduction/Network and security/SSH key pairs.md#) : A secure authentication method to remotely log on to Linux instances. The public key is placed in a Linux instance, and you can use the private key to log on to the instance by using SSH commands or related tools. Besides, you can use a [password](../../../../intl.en-US/User Guide/Connect/Connect to a Linux instance by using a password.md#) to log on to a Linux instance.
-   IP address: When an ECS instance is created, a private IP address is assigned to it for [intranet communication](intl.en-US/Product Introduction/Network and security/Intranet.md#). If the instance needs Internet access, a public IP address is assigned.
-   [EIP address \(EIP\)](https://www.alibabacloud.com/help/product/61789.htm): A public IP address resource that you can purchase and possess independently. You can bind an EIP address to a VPC-Connected ECS instance.
-   [ECS console](https://ecs.console.aliyun.com/#/home): The Web application for managing ECS instances.

## Related services {#section_ogy_tqj_ydb .section}

[Alibaba Cloud marketplace](https://www.alibabacloud.com/marketplace) is an online market. You can purchase software infrastructure, developer tools, and business software provided by third-party partners. You can become a marketplace service provider.

Auto Scaling enables you to dynamically scale your computing capacity up or down to meet the workload of your ECS instances according to scaling policies you specify, and to reduce the need of manual provision.  For more information, see [What is Auto Scaling](https://www.alibabacloud.com/help/product/25855.htm).

Container Service enables you to manage the lifecycle of containerized applications by using Docker and Kubernetes. For more information, see [What is Container Service](https://www.alibabacloud.com/help/product/25972.htm).

Server Load Balancer distributes the incoming traffic among multiple ECS instances according to the configured forwarding rules. For more information, see [What is Server Load Balancer](https://www.alibabacloud.com/help/product/27537.htm).

CloudMonitor manages ECS instances, system disks, Internet bandwidth, and other resources. For more information, see [What is CloudMonitor](https://www.alibabacloud.com/help/product/28572.htm).

Server Guard \(Server Security\) provides real-time awareness and defense against intrusion events, which safeguards the security of your ECS instances. For more information, see [What is Server Guard](https://www.alibabacloud.com/help/product/28449.htm).

Anti-DDoS Basic prevents and mitigates DDoS attacks by routing traffic away from your infrastructure. Alibaba Cloud Anti-DDoS Pro safeguards your ECS instances under high volume DDoS attacks. For more information, see [What is Anti-DDoS Basic](https://www.alibabacloud.com/help/doc-detail/28399.htm) and [What is Anti-DDoS Pro](https://www.alibabacloud.com/help/doc-detail/28464.htm).

Alibaba Cloud SDK enables you to access to Alibaba Cloud services and to manage your applications based on the language of your choice. For more information, see [Developer Resources](https://www.alibabacloud.com/support/developer-resources).  You can use [OpenAPI Explorer](https://api.aliyun.com/) to debug ECS API and generate the SDK Demo.

## Operations {#section_lsd_yqj_ydb .section}

Alibaba Cloud provides an intuitive operation interface for you to manage your ECS instances. You can log on to the [ECS console](https://ecs.console.aliyun.com/#/home) to operate ECS instances. For more information, see [User Guide](../../../../intl.en-US/User Guide/Quick reference.md#).

You can use API to manage your ECS instances. For more information, see [API References](../../../../intl.en-US/API Reference/Introduction.md#).  You can also use Alibaba Cloud CLI to call API to manage ECS instances. For more information, see [Alibaba Cloud Command Line Interface](https://www.alibabacloud.com/help/zh/product/29991.htm).

## Pricing and billing {#section_vq5_brj_ydb .section}

ECS supports both Subscription and Pay-As-You-Go as billing methods. For more information, see [Billing methods](../../../../intl.en-US/Pricing/Pricing overview.md#).

For the price information, see the [Pricing](https://www.alibabacloud.com/product/ecs) page.

