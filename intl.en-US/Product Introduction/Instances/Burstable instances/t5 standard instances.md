# t5 standard instances {#concept_fl1_tl4_cfb .concept}

t5 standard instances are ideal for scenarios where you do not usually, but occasionally require high CPU performance, such as lightweight Web servers, development and testing environments, and low or mid-performance databases.

If the instance has accrued few credits, its performance gradually declines to the baseline level within 15 minutes, so that the instance performance does not drop dramatically when the accrued CPU credits are used up. When the accrued CPU credits are used up, the actual CPU performance of the t5 instance cannot be higher than the baseline CPU performance.

## Fees {#section_ccj_hjp_cfb .section}

There is no additional fee except the cost of creating an instance.

## Examples {#section_hhw_wcn_cfb .section}

Take a t5 standard instance of the ecs.t5-lc1m2.small type as an example. The following describes how its CPU credits change:

1.  When the instance is created, 30 initial CPU credits are allocated to it. That is, the total CPU credits are 30 before it is started. After it is started, CPU credits accrue at the rate of 0.1 credits per minute. Meanwhile, the credits are consumed during its running.
2.  During the first minute, if the CPU usage is 5%, 0.05 initial CPU credits are consumed, while 0.1 CPU credits are allocated. Therefore, 0.05 CPU credits are accrued.
3.  After the instance has started for N minutes, if the CPU usage is 50%, 0.5 CPU credits are consumed while 0.1 CPU credits are allocated within one minute. Therefore, 0.4 CPU credits are consumed during this one minute.
4.  When the accrued CPU credits are used up, the maximum CPU usage is 10%.

