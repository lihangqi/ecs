# Basic concepts {#concept_n52_3v2_5db .concept}

Burstable instances \(also called t5 instances\) provide a baseline level of CPU performance with the ability to burst above the baseline. Each t5 instance provides a baseline CPU performance and earns CPU credits at a specified rate based on instance types. A t5 instance consumes CPU credits to meet service requirements once it is started. When the required performance is higher than the baseline, the instance consumes more CPU credits to seamlessly increase CPU performance without affecting the environment or applications on the instance.

t5 instances come with two running modes: [Standard](reseller.en-US/Instances/Instance type families/Burstable instances/t5 standard instances.md#) and [Unlimited](reseller.en-US/Instances/Instance type families/Burstable instances/t5 unlimited instances.md#).

## Concepts {#section_wc4_lx5_ydb .section}

-   **Baseline CPU performance** 

    Each t5 instance type provides a baseline level of CPU performance,

    -   which means that each vCPU core has a usage limit under normal workloads. For example, when the ecs.t5-lc1m2.small standard instance runs under normal workloads, the maximum CPU usage is 10%. More credits will be consumed to burst above that baseline. After the credits are used up, the maximum CPU usage is 10%.

    -   By contrast, t5 unlimited instances are not restricted by the baseline and can maintain high CPU performance for any time period. However, fees are charged for excess credits.

-   **CPU credits** 

    Each t5 instance earns CPU credits at a fixed rate based on the baseline CPU performance. One CPU credit represents the computing performance, which is related to the number of vCPU cores, CPU usage, and running time. For example:

    -   One CPU credit = One vCPU core running at 100% usage for 1 minute

    -   One CPU credit = One vCPU core running at 50% usage for 2 minutes

    -   One CPU credit = Two vCPU cores running at 25% usage for 2 minutes

        To support a vCPU core running at 100% usage for an hour, 60 CPU credits are required.

-   **Initial CPU credits** 

    Every time you create a t5 instance, each vCPU core of the instance is immediately allocated 30 CPU credits, which are called initial CPU credits. Initial CPU credits are allocated only upon instance creation. Additionally, they are consumed first when the instance starts to spend credits.

-   **CPU credit acquisition rate** 

    t5 instances acquire CPU credits on a per-minute basis. The CPU credit acquisition rate indicates CPU credits acquired by a t5 instance per unit time \(minute\). It is determined by the baseline CPU performance. The calculation formula is as follows:

    ```
    CPU credit acquisition rate = Baseline CPU performance x number of vCPUs
    ```

    **Example**: Use the ecs.t5-c1m2.xlarge instance as an example. Its average baseline CPU performance is 15%, so the CPU credit acquisition rate is 0.6 CPU credit per minute, that is, 36 CPU credits per hour.

-   **CPU credit consumption** 

    A t5 instance consumes CPU credits once it is started. Initial CPU credits are consumed first. The formula for calculating the consumed CPU credits per minute is as follows:

    ```
    CPU credits consumed per minute = One CPU credit x actual CPU performance
    ```

    **Example**: Use the ecs.t5-lc1m2.small instance as an example. It consumes 0.2 CPU credit when it runs at 20% CPU usage for one minute.

-   **Accrued CPU credits** 

    When the CPU usage of a t5 instance is lower than the baseline CPU performance, the instance accrues CPU credits because the CPU credit consumption rate is lower than the CPU credit acquisition rate. Otherwise, the instance consumes CPU credits overall. The CPU credit accrual rate is determined by the difference between the actual CPU load and the baseline performance. It can be calculated using the following formula:

    ```
    CPU credits accrued per minute = One CPU credit x (baseline CPU performance - actual CPU performance)
    ```

    You can [view the accrued and consumed CPU credits](reseller.en-US/Instances/Instance type families/Burstable instances/Manage t5 instances.md#section_imz_wx5_ydb) on the ECS console.

-   **Max. CPU credit balance** 

    CPU credits increase when the CPU credit acquisition rate is higher than the CPU credit consumption rate. The accrued credits do not expire on a running instance. However, there is an upper limit for the credits that can be accrued by an instance, namely, the maximum CPU credit balance. The upper limit varies with instance types.

    Taking ecs.t5-lc2m1.nano as an example, the maximum CPU credit balance is 144. When the CPU credit balance reaches 144, accrual pauses. When the balance is lower than 144, accrual restarts.


## How stopping an instance impacts CPU credits {#section_xt5_fx5_ydb .section}

After you stop a t5 through the [view CPU utilization and CPU credits](reseller.en-US/Instances/Instance type families/Burstable instances/Manage t5 instances.md#section_imz_wx5_ydb) feature or the [StopInstance API](../../../../reseller.en-US/API Reference/Instances/StopInstance.md#), CPU credits change according to the billing method and network type, as shown in the following table.

|Network type|Billing method|How CPU credits change after the instance is stopped|
|:-----------|:-------------|:---------------------------------------------------|
|VPC|Subscription|The existing CPU credits are valid, and the credit accrual continues.|
|Pay-As-You-Go \(with the [no fees for stopped VPC instances](../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#) function disabled\)|
|Pay-As-You-Go \(with [no fees for stopped VPC instances](../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#) function enabled\)|CPU credits accrued before the stoppage become invalid. The instance acquires initial CPU credits again after it is restarted.|

The instance continues to accrue CPU credits after it is restarted.

If a Pay-As-You-Go instance has overdue payment or a Subscription instance expires, its CPU credits remain valid, but no new CPU credits will be accrued. After you [reactivate](../../../../reseller.en-US/Instances/Manage instances/Reactivate an instance.md#) or [renew](../../../../reseller.en-US/Pricing/Renew instances/Renewal overview.md#) the instance, it automatically accrues CPU credits.

## Instance types {#section_c55_fx5_ydb .section}

t5 instances use Intel Xeon processors. The following table lists instance types. In this table:

-   **CPU credits/hour** indicates the total CPU credits allocated to all vCPU cores of a t5 instance per hour.
-   **Average baseline CPU performance** indicates the average baseline CPU performance of each vCPU core of a t5 instance.

|Instance type|vCPU|Average baseline CPU performance|Initial CPU credits|CPU credits/hour|Max. CPU credit balance|Memory \(GiB\)|
|:------------|:---|:-------------------------------|:------------------|:---------------|:----------------------|:-------------|
|ecs.t5-lc2m1.nano|1|10%|30|6|144|0.5|
|ecs.t5-lc1m1.small|1|10%|30|6|144|1.0|
|ecs.t5-lc1m2.small|1|10%|30|6|144|2.0|
|ecs.t5-lc1m2.large|2|10%|60|12|288|4.0|
|ecs.t5-lc1m4.large|2|10%|60|12|288|8.0|
|ecs.t5-c1m1.large|2|15%|60|18|432|2.0|
|ecs.t5-c1m2.large|2|15%|60|18|432|4.0|
|ecs.t5-c1m4.large|2|15%|60|18|432|8.0|
|ecs.t5-c1m1.xlarge|4|15%|120|36|864|4.0|
|ecs.t5-c1m2.xlarge|4|15%|120|36|864|8.0|
|ecs.t5-c1m4.xlarge|4|15%|120|36|864|16.0|
|ecs.t5-c1m1.2xlarge|8|15%|240|72|1,728|8.0|
|ecs.t5-c1m2.2xlarge|8|15%|240|72|1,728|16.0|
|ecs.t5-c1m4.2xlarge|8|15%|240|72|1,728|32.0|
|ecs.t5-c1m1.4xlarge|16|15%|480|144|3,456|16.0|
|ecs.t5-c1m2.4xlarge|16|15%|480|144|3,456|32.0|

**Examples**

-   The following uses the ecs.t5-c1m1.xlarge instance as an example.

    -   For each vCPU core, the average baseline performance is 15%. Therefore, the total baseline performance of the instance is 60% \(4 vCPU x 15%\). Details are as follows:

        -   When the instance uses only one vCPU core, this core provides the baseline performance of 60%.
        -   When the instance uses two vCPU cores, each core is allocated the baseline performance of 30%.
        -   When the instance uses three vCPU cores, each core is allocated the baseline performance of 20%.
        -   When the instance uses all four vCPU cores, each core is allocated the baseline performance of 15%.
        **Note:** When the business needs arise, CPU credits are consumed to improve the CPU performance. The performance of each vCPU core can increase to 100%.

    -   An instance acquires 36 CPU credits per hour, which means that each vCPU core acquires nine CPU credits per hour.

-   The following uses the ecs.t5-c1m2.4xlarge instance as an example.

    -   For each vCPU core, the average baseline performance is 15%. Therefore, the total baseline computing performance of the instance is 240% \(16 vCPU x 15%\). Details are as follows:

        -   When the instance uses only one vCPU core, this core provides the baseline performance of 100%.
        -   When the instance uses two vCPU cores, each core is allocated the baseline performance of 100%.
        -   When the instance uses three vCPU cores, each core is allocated the baseline performance of 80%.
        -   When the instance uses all 16 vCPU cores, each core is allocated the baseline performance of 15%.
        **Note:** When the business needs arise, CPU credits are consumed to improve the CPU performance. The performance of each vCPU core can increase to 100%.

    -   An instance acquires 144 CPU credits per hour, which means that each vCPU core acquires nine CPU credits per hour.


## Billing methods {#section_u55_fx5_ydb .section}

t5 instances support both the Pay-As-You-Go and Subscription billing methods. For differences between the billing methods, see [billing method comparison](../../../../reseller.en-US/Pricing/Billing method comparison.md#).

