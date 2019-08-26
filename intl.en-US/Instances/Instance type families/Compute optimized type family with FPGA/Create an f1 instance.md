# Create an f1 instance {#concept_tq5_r31_ydb .concept}

This topic describes how to create an f1 instance.

## Prerequisites {#section_w1f_cj1_ydb .section}

You must use an image that is pre-installed with the Intel development environment to create an f1 instance. To obtain the image, open a ticket.

## Procedure {#section_m1m_s31_ydb .section}

Follow the steps described in [create an ECS instance](../../../../reseller.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#). The following configurations must be selected:

-   **Region**: Select **China \(Hangzhou\)** \> **Zone F**.
-   **Instance Type**: Select **Heterogeneous Computing** \> **Compute Optimized Type with FPGA**, and then select the appropriate f1 instance type.
-   **Image**: Select **Shared Image**, and then select the shared image.

    **Note:** You must use an image that is pre-installed with the Intel development environment to create an f1 instance. This image is not available in the Alibaba Cloud Marketplace directly. To obtain the image, please find quartus17.0, vcs2017.3, dcp sdk in the opt directory.

-   **Network Type**: Select **VPC**, and select a created VPC and VSwitch.

After an f1 instance is created, [connect to the instance](reseller.en-US/Instances/Connect to instances/Overview.md#) and run the following command to check whether the licence is configured.

``` {#codeblock_p88_owd_jhh}
echo $LM_LICENSE_FILE #Check whether the variable is set.
```

## Best practices {#section_q1m_s31_ydb .section}

See best practices of f1 instances:

-   [Use OpenCL on an f1 instance](https://partners-intl.aliyun.com/help/doc-detail/61410.htm)
-   [Use f1 RTL \(Register Transfer Level\)](https://partners-intl.aliyun.com/help/doc-detail/61412.htm)

