# Create an f3 instance {#concept_myr_2m1_ydb .concept}

This article describes how to create an f3 instance.

## Procedure {#section_csy_fm1_ydb .section}

For more information about how to create an f3 instance, see [create an instance by using the wizard](reseller.en-US/User Guide/Instances/Create an instance/Create an instance by using the wizard.md#). However, the following configurations are recommended:

-   **Billing Method**: Select **Pay-As-You-Go** or **Subscription**.

    **Note:** f3 instances are not available as preemptible instances.

-   **Region**: Select **China East 2 \(Shanghai\)**.
-   **Instance Type**: Select **Heterogeneous Computing** \> **FPGA Compute**, and then select your required instance type.
-   **Image**: Click **Shared Image**, and then select the specified image.

    **Note:** A Xilinx image is available for use \(recommended\). The image is only available as a Shared image. To obtain the image, open a ticket.

-   **System Disk**: Allocate a 200 GiB Ultra Disk for the system image.
-   **Network**: Select **VPC**.

## Best practices {#section_hsy_fm1_ydb .section}

[Use OpenCL on an f3 instance](../../../../reseller.en-US/Best Practices/FaaS instances best practices/Use OpenCL on an f3 instance.md#)

[Use RTL compiler on an f3 instance](../../../../reseller.en-US/Best Practices/FaaS instances best practices/Use RTL compiler on an f3 instance.md#)

