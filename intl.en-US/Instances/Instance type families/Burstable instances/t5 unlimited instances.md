# t5 unlimited instances {#concept_abd_vlm_cfb .concept}

t5 unlimited instances can maintain high CPU performance for any period of time, without being limited to the baseline CPU performance.

## Concepts {#section_n5l_mq4_cfb .section}

In addition to the [basic concepts](reseller.en-US/Instances/Instance type families/Burstable instances/Basic concepts.md#), you also need to understand the following concepts before using t5 unlimited instances:

-   **Advance credits** 

    The credits that are used in advance but should be obtained within the next 24 hours.

-   **Excess credits**

    After the credits for the next 24 hours are used up, additional credits incur fees that are billed by the hour.


When a t5 unlimited instance runs out of its CPU credit balance, advance credits are used first to address the requirement of high CPU performance. When the CPU usage is lower than the baseline, the earned CPU credits are used to pay down \(offset\) the advance credits.

## Billing rules {#fees .section}

-   **Fees are not charged in the following cases:**
    -   The hourly t5 instance price automatically covers all interim spikes in usage if the average CPU utilization of the instance is at or below the baseline over a 24-hour period or the instance lifetime, whichever is shorter. You do not have to pay additional fees.

    -   An instance earns a maximum number of credits in a 24-hour period. For example, a t5-lc1m1.small instance can earn a maximum of 144 credits in a 24-hour period. When the advance credits are less than that maximum, no additional fees are charged.

-   **Fees are charged in the following cases:**
    -   If the consumed advance credits exceed the maximum credits \(that is, excess credits generated\), fees are charged at the end of the time period.

    -   If advance credits are used and the instance is stopped or released before the advance credits are cleared, a one-off fee is charged for the advance credits.

    -   If excess credits are used after advance credits are used up, additional fees are charged.

    -   If a t5 instance is changed from unlimited mode to standard mode, the fees for advance credits are charged immediately, and the accrued credits remain unchanged.

        The fees charged are shown in the following table:

        |Region|Windows instance \(USD/credit\)|Linux instance \(USD/credit\)|
        |:-----|:------------------------------|:----------------------------|
        |Mainland China|0.0008|0.0008|
        |Other regions|0.0016|0.0008|


## Examples {#section_u4w_vr4_cfb .section}

Use a t5-lc1m1.small unlimited instance \(purchased in US West 1 region\) as an example. The following describes how its CPU credits change.

1.  After a Linux instance is created, it is allocated 30 initial CPU credits. When the instance starts, it is able to spend 144 credits in advance, which are the maximum of CPU credits for the next 24 hours. Therefore, there are 174 CPU credits when the instance starts.
2.  After the instance starts, assuming the CPU utilization is 50%, the instance consumes 0.5 initial CPU credits per minute, while 0.1 CPU credits are allocated in the meantime. As a result, CPU credits continue to decrease.
3.  After the instance has been running for N minutes, assuming the accrued CPU credits are used up, the advance credits are spent to maintain high CPU performance.
4.  After the instance has been running for N + X minutes, assuming the 144 advance credits are used up, excess credits are used to maintain high CPU performance.
5.  After the instance has been running for N + X + Y minutes, assuming 50 excess credits are used and the CPU utilization drops to 5% \(below the baseline\), the instance begins to earn 0.1 credits per minute, which are used to pay down \(offset\) the consumed advance credits. When the advance credits are restored to 144, credits begin to accrue to the instance \(0.1 credits per minute\).

**Consumption details**

At the end of the N + X + Y minutes, if excess credits are no longer used, fees are charged.

During the above time period, the Linux instance uses 50 excess credits. The additional fee is: 0.0016 USD/credit x 50 credits = 0.08 USD.

