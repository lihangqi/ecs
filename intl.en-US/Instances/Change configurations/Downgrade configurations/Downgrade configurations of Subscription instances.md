# Downgrade configurations of Subscription instances {#concept_52574_zh .concept}

This topic describes how to downgrade configurations of Subscription instances, including the memory size and the number of vCPUs. The changes take effect immediately after an instance is restarted.

## Limits {#section_olg_wp1_1gb .section}

-   Whether you can downgrade the configurations of a Subscription instance is determined by your ECS instance resource usage.
-   You can downgrade configurations of only one instance at a time.
-   You can change the instance configurations only to lower-level configurations. Changes to configurations of the same level or a higher level are not allowed.
-   You can only downgrade the configurations of each instance a maximum of three times. Configuration downgrade operations include instance configuration downgrades, bandwidth configuration downgrades, and cloud disk billing method adjustments.
-   The time interval between two downgrade operations must be at least 5 minutes.

## Prerequisites {#section_okd_yp1_1gb .section}

The configurations of an instance can be downgraded only if the instance meets the following conditions:

-   The billing method is Subscription.
-   The instance is in the **Stopped** state.
-   The instance works properly. That is, the instance cannot be in an abnormal state, such as overdue, outdated, locked, or to be released.
-   The instance cannot have any ongoing configuration downgrade renewal process.

## Procedure {#section_htb_zp1_1gb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  Find the target instance. In the **Actions** column, choose **More** \> **Change Configuration**.
4.  In the displayed dialog box, select **Configuration downgrade** and **Instance Type**.
5.  Select a desired instance type, confirm the refund amount, and read and confirm that you agree with the *ECS Service Terms* .
6.  Click **Downgrade Now**.

## What to do next {#section_rws_ktf_1gb .section}

Restart the instance for the new configurations to take effect.

