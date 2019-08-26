# Attach an ENI when creating an instance {#concept_twf_4jj_zdb .concept}

You can attach an ENI when creating an ECS instance in the ECS console. For more information about instance creation, see [create an instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#). This document focuses on the notes for attaching an ENI during ECS instance creation.

Note the following configurations when attaching an ENI during ECS instance creation:

-   Basic configurations:
    -   Region: ENIs are supported in all regions.
    -   Instance type: Select an instance type that supports ENI. The selected instance type must be I/O optimized.
    -   Image: Only the following types of image can automatically recognize ENIs without any additional configuration. For other images, you must configure the ENI to enable the created instance to recognize it.
        -   Centos 7.3 64-bit
        -   Centos 6.8 64-bit
        -   Windows Server 2016 Data Center Edition 64-bit
        -   Windows Server 2012 R2 Data Center Edition 64-bit
    -   Networking:
        -   Network: Select **VPC**, and then select a created VPC and a VSwitch.
        -   ENI: Click **Add ENI** to attach an ENI, and then select a VSwitch for the ENI.

            **Note:** 

            -   You are only allowed to attach a maximum of two ENIs when creating an instance in the console. One of them is the primary ENI, which is attached automatically, and the other one is a secondary ENI.
            -   After the instance is started, you can attach more secondary ENIs to the instance based on the instance type in the console or by using the [AttachNetworkInterface](../../../../reseller.en-US/API Reference/Elastic network interfaces/AttachNetworkInterface .md) API.

If you want to keep the secondary ENI that is created in this way, detach it from the instance before you release the instance.

