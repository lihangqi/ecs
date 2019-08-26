# Revoke a secondary private IP address {#concept_csv_ncm_ggb .concept}

This topic describes how to revoke a secondary private IP address from an Elastic Network Interface \(ENI\).

## Limits {#section_rk2_ddm_ggb .section}

The primary private IP address cannot be revoked.

## Prerequisites {#section_bq5_gdm_ggb .section}

-   At least one secondary private IP addresses is assigned to the target ENI.
-   The target ENI is in the `Available` or `InUse` state.
-   If the secondary private IP addresses to be revoked is assigned to the primary ENI, the instance to which the primary ENI is attached must be in the `Running` or `Stopped` state.

## Procedure {#section_pzj_qcm_ggb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Network & Security** \> **ENI**.
3.  On the Network Interfaces page, locate the target ENI, and then click **Manage Secondary Private IP Address** in the **Actions** column.
4.  In the Manage Secondary Private IP Address dialog box, click **Unassign** once or multiple times if additional IP addresses need to be revoked.
5.  Click **Modify**.

Related API: [UnassignPrivateIpAddresses](../reseller.en-US/API Reference/Elastic network interfaces/UnassignPrivateIpAddresses.md#)

## What to do next {#section_bg2_xmp_3gb .section}

If your application requirements change, you can assign multiple secondary private IP address to an ENI. For more information, see [Assign a secondary private IP address](reseller.en-US/Network/Elastic Network Interfaces/Assign a secondary private IP address.md#).

