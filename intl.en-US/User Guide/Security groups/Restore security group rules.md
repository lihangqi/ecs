# Restore security group rules {#concept_ec2_bg1_ydb .concept}

Restoring security group rules indicates the process of completely or partially restoring the rules in the original security group to those of a target security group. Specifically:

-   **Completely restoring** means moving the rules that do not exist in the target security group from the original security group and adding the rules that only exist in the target security group to the original security group. After restoration, rules in the original security group are identical with those in the target security group.
-   **Partially restoring** means adding the rules that only exist in the target security group to the original security group and ignoring the rules that only exist in the original group.

## Limits {#section_en2_ng1_ydb .section}

Restoring security group rules has the following limits:

-   The original security group and the target security group must be in the same region.
-   The original security group and the target security group must be of the same network type.
-   If any system-level security group rules, of which the priority is 110, exist in the target security group, they are not created during restoration. After restoration, the rules in the original security group may be different from what is expected. If you need the system-level security group rules, you have to manually create the rules and set their priority to 100.

## Scenario {#section_egc_4g1_ydb .section}

If you want to apply new security group rules to an ECS instance that is running an online business application, you can clone the former security group as a backup, and then modify the rules inside. If the new security group rules affect the online business application, you can restore the rules fully or partially.

## Prerequisite {#section_nqx_4g1_ydb .section}

You must own at least one security group of the same network type in the same region.

## Procedure {#section_lzx_wg1_ydb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, select **Networks and Security** \> **Security Groups**.
3.  Select a region.
4.  Find the security group you want to restore rules for as the original security group, and in the **Actions** column, click **Restore Rules**.
5.  In the Restore Rules dialog box, follow these steps:
    1.  Select the **Target Security Group**: Select a security group as the target security group that must have different rules from the original security group.
    2.  Select a restore **Method**:
        -   If you want the original security group to have the same rules as the target security group, select **Completely Restore**.
        -   If you only want to add the rules that only exist in the target security group to the original security group, select **Partially Restore**.
    3.  In the **Preview** area, preview the restoration result:
        -   Rules highlighted in green only exist in the target security group. No matter whether you select **Completely Restore** or **Partially Restore**, these rules are added to the original security group.
        -   Rules highlighted in red are the rules that do not exist in the target security group. If **Completely Restore** is selected, the system removes these rules from the original security group. If **Partially Restore** is selected, the rules are retained in the original security group.
    4.  Click **OK**.

The Restore Rules dialog box is closed automatically after successful creation. On the **Security Grougs** page, find the original security group you restored the rules for. In the **Actions** column, click **Add Rules** to enter the Security Group Rules page to view the updated security group rules.

