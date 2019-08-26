# Burstable instances {#concept_n52_3v2_5db .concept}

Burstable instances \(also called t5 instances\) can raise the performance of the CPU when required. Each t5 instance provides a baseline CPU performance. When your t5 instance is running, it accumulates and consumes CPU credits. The instance type determines the rate at which CPU credits are distributed. t5 instances seamlessly increase your CPU performance, without affecting the instance environment or applications.

t5 instances are ideal for scenarios where you do not usually, but occasionally require high CPU performance, such as lightweight web servers, development and testing environments, and a low or mid-performance database.

## How t5 instances work {#section_wc4_lx5_ydb .section}

**Basic concepts**

Before you use t5 instances, you must know the following concepts:

-   **Baseline CPU performance** 

    The instance type of any t5 instance determines its baseline CPU performance, which means each vCPU core of an instance has a maximum usage for normal workloads. For example, when an ecs.t5-lc1m2.small instance is used for normal workloads, the maximum CPU usage is 10%.

-   **CPU credits** 

    Each t5 instance obtains CPU credits at a fixed distribution rate, which is determined by the baseline CPU performance. A CPU credit is a unit of measure for calculating performance, which is determined by the number of vCPU cores, CPU usage, and work time. For example:

    -   1 CPU credit = 1 vCPU core at 100% usage for 1 minute
    -   1 CPU credit = 1 vCPU core at 50% usage for 2 minutes
    -   1 CPU credit = 2 vCPU cores at 25% usage for 2 minutes

        If one vCPU core runs at 100% usage for one hour, it consumes 60 CPU credits.

-   **Initial CPU credits** 

    Each time you create a t5 instance, 30 CPU credits are immediately allocated to it. These initial CPU credits are allocated to t5 instances only once, and at the time of creation. When an instance begins to consume CPU credits, the initial CPU credits are used first.

-   **CPU credit distribution rate** 

    The CPU credit distribution rate is the number of CPU credits that a t5 instance obtains per minute. It is determined by the baseline CPU performance. You can use the following formula to determine the CPU credit distribution rate according to the baseline CPU performance.

    ```
     CPU credit distribution rate = (60 CPU credits * Baseline CPU performance)/60 minutes
    ```

    **Example**: A t5 instance of the ecs.t5-lc1m2.small type provides a baseline CPU performance of 10%, so the CPU credit distribution rate is 0.1 CPU credits per minute, or six CPU credits per hour.

-   **Expiration of CPU credits** 

    Once accumulated, the CPU credits are saved only for 24 hours. The credits are invalid after 24 hours.

-   **CPU credit consumption** 

    When a t5 instance is started, the instance consumes the CPU credits \(first the initial CPU credits, then the accumulated CPU credits\) to raise the CPU usage to meet your business requirements. If you use one vCPU at a certain usage for one minute, the number of the consumed CPU credits can be calculated by using the following formula:

    ```
    CPU credits consumed per minute = 1 CPU credit * Actual CPU usage
    ```

    **Example**: If a t5 instance of the ecs.t5-lc1m2.small type is used at 50% of its computing capability for 1 minute, it consumes 0.5 CPU credits.

-   **CPU credit accumulation** 

    When the CPU usage of a t5 instance is lower than the baseline CPU performance, the instance accumulates CPU credits because the consumption rate is lower than the CPU credit distribution rate. The accumulation speed is calculated by using the following formula:

    ```
    CPU credit accumulation per minute = 1 CPU credit * (Baseline CPU performance - Actual CPU usage) - Expired CPU credits within the minute
    ```


You can view the CPU credits of a t5 instance in the ECS console.

When the accumulated CPU credits are cleared, the actual CPU computing capability of the instance cannot be higher than the baseline CPU performance.

**Example**

A t5 instance of the ecs.t5-lc1m2.small type is used as an example here to introduce how CPU credits are accumulated.

1.  When the instance is created, 30 initial CPU credits are allocated to it. These are the total CPU credits the instance has before it is started. When the instance starts, it consumes CPU credits and is allocated with CPU credits at a rate of 0.1 CPU credits per minute.
2.  During the first minute after the instance starts, if the actual CPU usage is 5%, the CPU credits change as follows:

    -   0.05 initial CPU credits are consumed.
    -   0.1 CPU credits are allocated.
    -   No CPU credits expire.
    Therefore, 0.05 CPU credits are accumulated during this minute.

3.  During the N minute after the instance starts, if the actual CPU usage is 50%, the initial CPU credits have been used up, and 0.1 CPU credits expire, the CPU credits change as follows:

    -   0.5 CPU credits are consumed.
    -   0.1 CPU credits are allocated.
    Therefore, 0.5 CPU credits are consumed during this minute, and no CPU credits are accumulated.

4.  When the accumulated CPU credits are cleared, the maximum actual CPU usage is 10%.

## CPU credits accumulation on a stopped t5 instance {#section_xt5_fx5_ydb .section}

After you stop a t5 instance in the [ECS console](../../../../intl.en-US/User Guide/Instances/Start or stop an instance.md#) or by using the [StopInstance](../../../../intl.en-US/API Reference/Instances/StopInstance.md#) interface, CPU credit changes vary according to the billing method and network type, as shown in the following table.

|Network type|Instance billing method| CPU credits changes after stopping|
|:-----------|:----------------------|:----------------------------------|
|Classic|Either Subscription or Pay-As-You-Go|The existing CPU credits are valid and credits continue to accumulate.|
|VPC|Subscription|
|Pay-As-You-Go with [No fees for stopped instances \(VPC-Connected\)](../../../../intl.en-US/Pricing/No fees for stopped instances (VPC-Connected).md#) disabled|
|Pay-As-You-Go with [No fees for stopped instances \(VPC-Connected\)](../../../../intl.en-US/Pricing/No fees for stopped instances (VPC-Connected).md#) enabled|The existing CPU credits are valid but no more credits are accumulated.|

When you start a stopped instance, CPU credits continue accumulating.

If an instance becomes out-of-service because of an overdue payment or expiration, its CPU credits remain valid, but CPU credit accumulation stops. After the instance is reactivated or renewed, CPU credits start to accumulate again automatically.

## Instance types {#section_c55_fx5_ydb .section}

t5 instances use Intel Xeon processors. The instance types are shown in the following table. In this table:

-   **CPU credits/hour** is the total number of CPU credits allocated to all vCPU cores of a t5 instance per hour.
-   **Average baseline CPU performance** is the average baseline CPU performance of each vCPU core for a t5 instance.

|Instance type|vCPU|CPU credits/hour|Avg baseline CPU performance|Memory \(GiB\)|
|:------------|:---|:---------------|:---------------------------|:-------------|
|ecs.t5-lc2m1.nano|1|6|10%|0.5|
|ecs.t5-lc1m1.small|1|6|10%|1.0|
|ecs.t5-lc1m2.small|1|6|10%|2.0|
|ecs.t5-lc1m2.large|2|12|10%|4.0|
|ecs.t5-lc1m4.large|2|12|10%|8.0|
|ecs.t5-c1m1.large|2|18|15%|2.0|
|ecs.t5-c1m2.large|2|18|15%|4.0|
|ecs.t5-c1m4.large|2|18|15%|8.0|
|ecs.t5-c1m1.xlarge|4|36|15%|4.0|
|ecs.t5-c1m2.xlarge|4|36|15%|8.0|
|ecs.t5-c1m4.xlarge|4|36|15%|16.0|
|ecs.t5-c1m1.2xlarge|8|72|15%|8.0|
|ecs.t5-c1m2.2xlarge|8|72|15%|16.0|
|ecs.t5-c1m4.2xlarge|8|72|15%|32.0|
|ecs.t5-c1m1.4xlarge|16|144|15%|16.0|
|ecs.t5-c1m2.4xlarge|16|144|15%|32.0|

Here, we use ecs.t5-c1m1.xlarge as an example to explain the t5 instance configuration:

-   Each vCPU core has an average baseline computing performance of 15%. Therefore, the total baseline computing performance of a t5 instance of the ecs.t5-c1m1.xlarge type is 60%, which means:

    -   If the instance only uses one vCPU core, this core has a baseline computing performance of 60%.
    -   If the instance only uses two vCPU cores, each core is allocated a baseline computing performance of 30%.
    -   If the instance only uses three vCPU cores, each core is allocated a baseline computing performance of 20%.
    -   If the instance uses all four vCPU cores, each core is allocated a baseline computing performance of 15%.
-   One instance is allocated 36 CPU credits per hour. With four cores, each vCPU core is allocated nine CPU credits per hour.


## Billing method {#section_u55_fx5_ydb .section}

t5 instances support the following billing methods: Pay-As-You-Go and Subscription. For more information on the billing methods, see [Billing method comparison](../../../../intl.en-US/Pricing/Billing method comparison.md#).

## Create an instance {#section_v55_fx5_ydb .section}

See [Create an ECS instance](../../../../intl.en-US/Quick Start for Entry-Level Users/Step 2. Create an instance.md#) to create a t5 instance. When creating a t5 instance, consider the following settings:

-   Region: t5 instances are unavailable in the China North 3 \(Zhangjiakou\), Asia Pacific SE 3 \(Kuala Lumpur\), Asia Pacific NE 1 \(Tokyo\), US East 1 \(Virginia\), and Middle East 1 \(Dubai\) regions. For details of the zones in other regions that support t5 instances, see the [ECS purchase page](https://ecs-buy.aliyun.com/wizard/#/prepay/cn-hangzhou).

-   Network type: Only VPC is supported.

-   Image and instance type: The minimum t5 instance memory configuration of 512 MiB only supports Linux. To create a Windows instance, the minimum memory is 1 GiB. For more information on image selection, see [How to select a system image](https://www.alibabacloud.com/help/faq-detail/40651.htm).


## Manage t5 instances {#section_imz_wx5_ydb .section}

**View CPU usage**

You can view CPU usage in the following ways:

-   In the ECS console, go to the **Monitoring Information** section of the Instance Details page to view the instance CPU usage.

-   Remotely connect to the ECS instance to view CPU usage.


**View CPU usage in the ECS console**

To view CPU usage in the ECS console, follow these steps:

1.  Log on to the [ECS console](https://ecs.console.aliyun.com/#/home).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  Find a t5 instance, and click the instance ID or in the **Actions** column, click **Manage**.
5.  In the **Monitoring Information** section, view CPU usage information.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9554/15342272125110_en-US.png)


**Remotely connect to the instance to view CPU usage**

The methods vary according to the operating system:

-   Windows: [Connect to the instance](../../../../intl.en-US/User Guide/Connect to instances/Connect to a Windows instance.md#) and view the information in the **Task Manager**.

-   Linux: [Connect to the instance](../../../../intl.en-US/User Guide/Connect to instances/Connect to a Linux instance by using a password.md#) and run the `top` command to view the CPU usage.


**Change configurations**

In the ECS console, if you see that the CPU usage is at the baseline level of CPU performance for an extended period or it never exceeds the baseline level, your current instance type is either insufficient for your needs or exceeds your needs. In these cases, consider changing the instance type.

You can change the instance type based on the billing method:

-   For a Subscription instance, you can change the instance type. For more information, see [Change configurations](../../../../intl.en-US/User Guide/Instances/Change configurations/Overview of configuration changes.md#). You can change the specification of an instance to any type in the t5 instance type family, any enterprise-level instance type families, or any type within the xn4, n4, mn4, or e4 type family.

-   For a Pay-As-You-Go instance, you can [change the instance type](../../../../intl.en-US/User Guide/Instances/Change configurations/Change configurations of Pay-As-You-Go instances.md#).


**View CPU credits**

Log on to the [ECS console](https://ecs.console.aliyun.com/#/home) and go to the Instance Details page to view the accumulated and consumed CPU credits of a t5 instance.

-   View the accumulated CPU credits of a t5 instance:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9554/15342272125111_en-US.png)

-   View the consumed CPU credits of a t5 instance:

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9554/15342272125112_en-US.png)


