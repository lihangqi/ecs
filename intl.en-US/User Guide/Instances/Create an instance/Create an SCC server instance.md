# Create an SCC server instance {#concept_vrp_mr1_ydb .concept}

Super Computing Cluster \(SCC\) is based on the ECS Bare Metal \(EBM\) instance product. Utilizing the high-speed interconnectivity of RDMA \(Remote Direct Memory Access\) technology, SCC greatly improves network performance and increases the acceleration ratio of large-scale clusters. SCC has all the advantages of EBM instances, and provides high-quality network performance featuring high bandwidth and low latency. For more information, see [ECS Bare Metal instance and Super Computing Clusters](../../../../reseller.en-US/Product Introduction/Instances/ECS Bare Metal Instance and Super Computing Clusters.md#).

This article describes how to create an SCC instance. For more information about instance creation, see [create an image by using the wizard](reseller.en-US/User Guide/Instances/Create an instance/Create an instance by using the wizard.md#).

The following configurations are recommended for SCC instances:

-   **Region**: Currently, only **China East 2 \(Shanghai\)** **Zone D** and **Zone B** support SCC instances.
-   **Instance Type**: Instance type families scch5 and sccg5 are available. For more information about instance types, see [instance type families](../../../../reseller.en-US/Product Introduction/Instance type families.md#scch5).
-   **Image**: Select **Public Image**. Currently, only a custom Linux CentOS 7.5 image for SCC is supported.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9637/15429600425118_en-US.png)

-   **Storage**: SCC support up to 16 data disks. You can add a data disk during or after instance creation, and then [mount the data disk](reseller.en-US/User Guide/Cloud disks/Attach a cloud disk.md#). 
-   **Network**: Only VPC is supported.

