# What is ECS? {#EcsWelcome .concept}

Elastic Compute Service \(ECS\) is a high-performance, stable, reliable, and scalable IaaS-level service provided by Alibaba Cloud. It is more convenient and efficient compared with physical servers. You can immediately acquire ECS instances and scale computing resources on-demand. ECS provides a variety of instance types that suit various business needs and help boost business growth.

  

## Why ECS? {#section_wj3_jyp_jhb .section}

ECS provides the following benefits:

-   You do not have to purchase hardware or construct data centers up front.
-   Instances are delivered within minutes, enabling rapid deployment and reducing time to market.
-   You can make use of resources in data centers and BGP grids around the world.
-   You can scale and release resources based on actual business needs.
-   Provides heterogenous computing servers such as GPU, FPGA, bare metal servers, and general x86 servers.
-   You can use ECS to access other Alibaba Cloud services over the internal network, reducing traffic costs.
-   Provides a host of security solutions, such as virtual firewalls, permission control, internal network isolation, virus protection, and traffic throttling.
-   Provides a performance monitoring framework and proactive O&M systems.
-   Provides standardized APIs to improve ease of use and applicability.

For more benefits, see [Benefits of ECS](reseller.en-US/Product Introduction/Benefits of ECS.md#) and [Scenarios](reseller.en-US/Product Introduction/Scenarios.md#).

## Architecture {#section_vwb_qk2_ghb .section}

ECS comprises the following major components:

-   [Instance](../../../../reseller.en-US/Instances/What are ECS instances?.md#): a virtual computing environment that includes basic computing components such as CPU, memory, operating system, bandwidth, and disks. The computing performance, memory specifications, and applicable scenarios of an instance are determined by its [instance type](../../../../reseller.en-US/Instances/Instance type families.md#). The performance of an instance is determined by its vCPUs, memory capacity, and network performance.
-   [Image](../../../../reseller.en-US/Images/Image overview.md#): provides the operating system, initial application data, and pre-installed software for instances. Multiple Linux operating systems and Windows Server operating systems are supported.
-   [Block storage](../../../../reseller.en-US/Block Storage/What is block storage?.md#): a block storage device which features high performance and low latency. Distributed storage architecture-based [cloud disks](../../../../reseller.en-US/Block Storage/Block storage/Cloud disk overview.md#), and physical storage-based [local disks](../../../../reseller.en-US/Block Storage/Local disks.md#) can be used.
-   [Snapshot](../../../../reseller.en-US/Snapshots/Snapshot overview.md#): a stateful data file of a cloud disk or shared block storage at a certain point in time. It is often used to back up and restore data, and to create custom images.
-   [Security group](../../../../reseller.en-US/Security/Security groups/Security group overview.md#): a logical group of instances located in the same region that have the same security requirements and require access to each other. A security group works as a virtual firewall for the ECS instances inside it.
-   [Network](../../../../reseller.en-US/Network/Network types.md#):
    -   [VPC](../../../../reseller.en-US/Product Introduction/What is VPC?.md#): a logically isolated private cloud network. You can configure a private IP address range, a route table, and a gateway for a VPC.
    -   Classic network: all classic instances are primarily built on a shared infrastructure network of Alibaba Cloud, which is planned and managed in a centralized manner.

The following figure shows the architecture of ECS components. For more information about the functional components in the figure, see the related documentation.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9543/156618577948636_en-US.png)

## Pricing {#section_vq5_brj_ydb .section}

ECS supports multiple billing methods, such as subscription, pay-as-you-go, reserved instances \(beta phase\), and preemptible instances. For more information, see [Pricing overview](../../../../reseller.en-US/Pricing/Billing overview.md#).

## Management tools {#section_lsd_yqj_ydb .section}

After registering an Alibaba Cloud account, you can create, use, or release an ECS instance in any region by using the following methods provided by Alibaba Cloud:

-   ECS console: a Web service page used to manage ECS instances. For more information, see [Quick reference](../../../../reseller.en-US/Quick Start for Entry-Level Users/Quick reference.md#).
-   ECS APIs: RPC APIs that support GET and POST requests. For more information, see [API Reference](../../../../reseller.en-US/API Reference/Introduction.md#). The following developer tools can be used to call ECS APIs:
    -   [CLI](../../../../reseller.en-US/Product Introduction/What is Alibaba Cloud CLI?.md#): a flexible and scalable management tool based on Alibaba Cloud APIs. You can use CLI to encapsulate Alibaba Cloud native APIs to develop custom features.
    -   [OpenAPI Explorer](https://api.aliyun.com/): allows you to retrieve APIs, call APIs, and dynamically generate SDK example code.
    -   [Alibaba Cloud SDK](https://partners-intl.aliyun.com/vodafone/support/developer-resources): provides SDKs for multiple programming languages such as Java, Python, and PHP.
-   [Resource Orchestration Service](../../../../reseller.en-US/Product Introduction/What is ROS?.md#): automatically creates and configures Alibaba Cloud resources based user-defined templates.
-   [Terraform](../../../../reseller.en-US/Deployment & Elasticity/Terraform/What is Terraform?.md#): an open-source tool that uses configuration files to call computing resources on Alibaba Cloud and other platforms that support Terraform. Terraform also implements version control.

## Deployment tips {#section_qde_v9o_iur .section}

Before you purchase an ECS instance, consider the following factors:

-   Regions and zones

    A region represents an Alibaba Cloud data center. The region and zone determine the physical location of an ECS instance. After an instance is created, its [metadata](../../../../reseller.en-US/Instances/Manage instances/User-defined data and metadata/Metadata.md#) is established and its region cannot be changed. Select a region and zone based on the target geographical location, availability of Alibaba Cloud services, application availability requirements, and whether internal network communication is required. For example, if you want to access both ECS and [ApsaraDB for RDS](../../../../reseller.en-US/Product Introduction/What is ApsaraDB for RDS?.md#), the RDS instance and ECS instance must be in the same region. For more information, see [Regions and zones](../../../../reseller.en-US/General Reference/Regions and zones.md#).

-   High availability

    To ensure business consistency and continuity, we recommend that you use [snapshots](../../../../reseller.en-US/Snapshots/Snapshot overview.md#) to back up data, and use multi-zone deployment, [deployment sets](../../../../reseller.en-US/Deployment & Elasticity/Deployment sets/Deployment set.md#), and [Server Load Balancer \(SLB\)](../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#) for disaster recovery.

-   Network planning

    We recommend that you use [VPC](../../../../reseller.en-US/Product Introduction/What is VPC?.md#) to plan your own private IP addresses. VPC supports all new features and new instance types. It also supports business system isolation and multi-region system deployment.

-   Security solutions

    You can use ECS security groups to control inbound and outbound access policies and the port listening status of ECS instances. For applications deployed on ECS, you can use free [Anti-DDoS Basic](../../../../reseller.en-US/Security/Anti-DDoS Basic.md#). Alibaba Cloud Security is also available.

    -   For example, you can use Anti-DDoS Pro to ensure the stability and reliability of source sites. For more information, see [Anti-DDoS Pro documentation](../../../../reseller.en-US/Anti-DDoS Pro Service/Product Introduction/What is Anti-DDoS Pro.md#).
    -   Server Guard can be used to safeguard the security of ECS instances. For more information, see [Server Guard documentation](../../../../reseller.en-US/.md#).

## Related services {#section_cdb_tqj_ydb .section}

Together with ECS, you can select the following Alibaba Cloud services:

-   [Auto Scaling](../../../../reseller.en-US/Product Introduction/What is Auto Scaling?.md#) automatically adjusts the number of ECS instances based on business and policy changes.
-   [Container Service](../../../../reseller.en-US/Product Introduction/What is Container Service.md#) manages application lifecycles on groups of ECS instances.
-   [Server Load Balancer \(SLB\)](../../../../reseller.en-US/Product Introduction/What is Server Load Balancer?.md#) distributes traffic among multiple ECS instances.
-   [CloudMonitor](../../../../reseller.en-US/Product Introduction/Overview.md#) develops monitoring solutions for instances, system disks, and public network bandwidth.
-   [ApsaraDB for RDS](../../../../reseller.en-US/Product Introduction/What is ApsaraDB for RDS?.md#) provides database services accessible over internal networks to ECS instances, reduces network latency, access fees, and delivers top-notch performance. ApsaraDB for RDS supports multiple database engines, including MySQL, SQL Server, PostgreSQL, PPAS, and MariaDB.
-   [Alibaba Cloud Marketplace:](https://partners-intl.aliyun.com/marketplace/vodafone/) a platform to purchase software infrastructure, business software, website construction, hosted O&M, security, data & APIs, and solutions provided by third-party partners. You can also provide software programs and services as a service provider. For more information, see [Alibaba Cloud Marketplace documentation](https://partners-intl.aliyun.com/help/product/30488.htm).

