# Create an SCC instance {#concept_vrp_mr1_ydb .concept}

This topic describes how to create a Super Computing Cluster \(SCC\) instance.

Super Computing Cluster \(SCC\) is based on the ECS Bare Metal instance type. By utilizing the high-speed interconnectivity of RDMA \(Remote Direct Memory Access\) technology, SCC greatly improves network performance and increases the acceleration ratio of large-scale clusters. SCC offers all the advantages of ECS Bare Metal instances, and provides high-quality network performance featuring high bandwidth and low latency. For more information, see [ECS Bare Metal instance and Super Computing Clusters](../../../../reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/EBM Instance overview.md#).

## Procedure {#section_h2m_pr1_ydb .section}

You can create an SCC instance by following the instructions described in [Create an ECS Instance](reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#).

However, the following configurations must be considered:

-   **Region**: Select the region and zone according to the table [Regions and zones where SCC instances are available](reseller.en-US/Instances/Instance type families/Super Computing Cluster instance type family/Create an SCC instance.md#section_ycz_mnl_jhb). Note that the purchase page displays the latest region and zone information, which may differ from information provided in this topic.
-   **Network Type**: Only VPC is supported.
-   **Instance Type**: Currently, the instance type families scch5, sccg5, and sccgn6 are available.
-   **Image**: Select **Public Image**. Currently, only a custom Linux CentOS 7.5 image for SCC is supported.

    **Note:** The custom image supports the RDMA RoCE driver and OFED stack. You can use the RDMA functions through IB verbs programming or implement RDMA communication through MPI.

     ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9637/15667773245118_en-US.png)

-   **Storage**: SCC supports up to 16 data disks. You can [add a data disk](reseller.en-US/Block Storage/Block storage/Create a cloud disk/Create a Pay-As-You-Go cloud disk.md#) during or after instance creation, and then [mount the data disk](reseller.en-US/Block Storage/Block storage/Attach a cloud disk.md#).

## Regions and zones where SCC instances are available {#section_ycz_mnl_jhb .section}

The following table shows the regions and zones where SCC instances are available.

|Instance type family|Region and zone|
|--------------------|---------------|
|scch5|China \(Shanghai\) Zones D and B|
|sccg5|China \(Shanghai\) Zones D and B|
|sccgn6| -   China \(Shanghai\)
-   China \(Beijing\)
-   China \(Zhangjiakou\)

 |

## What to do next {#section_g2m_pr1_ydb .section}

If you not only need to use the RDMA feature, but also need to use the HPC scheduler and the cluster scaling service, you can create an SCC instance by creating an SCC cluster through the [E-HPC console](https://partners-intl.console.aliyun.com/#/ehpc).

**Note:** For more information about the availability of SCC instances, see [Regions and zones where SCC instances are available](reseller.en-US/Instances/Instance type families/Super Computing Cluster instance type family/Create an SCC instance.md#section_ycz_mnl_jhb). Note that only the Subscription billing method is supported.

