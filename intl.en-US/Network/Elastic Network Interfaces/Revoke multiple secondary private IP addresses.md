# Revoke multiple secondary private IP addresses {#concept_csv_ncm_ggb .concept}

You can revoke one or more secondary private IP addresses assigned to an Elastic Network Interface \(ENI\) when the ENI no longer needs them.

## Limits {#section_rk2_ddm_ggb .section}

-   The primary private IP address cannot be revoked.
-   You can only attach an ENI to a VPC ECS instance in the same VPC.
-   A single VPC security group can contain a maximum of 2,000 private IP addresses \(shared by the primary and secondary ENIs\).

## Prerequisites {#section_bq5_gdm_ggb .section}

-   You have assigned multiple secondary private IP addresses to your ENI.
-   The ENI is in `Available` or `InUse` status.
-   When you revoke secondary private IP addresses assigned to the primary ENI, the instances attached to the primary ENI must be in `Running` or `Stopped` state.

## Procedure {#section_pzj_qcm_ggb .section}

1.  Use the [DescribeNetworkInterfaces](../../../../../reseller.en-US/API Reference/Elastic network interfaces/DescribeNetworkInterfaces.md#) API to query the assigned secondary private IP addresses.
2.  Use the [UnassignPrivateIpAddresses](../../../../../reseller.en-US/API Reference/Elastic network interfaces/UnassignPrivateIpAddresses.md#) API to revoke the assigned secondary private IP addresses.

## What to do next {#section_bg2_xmp_3gb .section}

If you want to increase the usage of your instance or implement a failover transfer, you can [Assign multiple secondary private IP addresses](reseller.en-US/Network/Elastic Network Interfaces/Assign multiple secondary private IP addresses.md#) to an ENI.

