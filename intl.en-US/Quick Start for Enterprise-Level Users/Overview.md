# Overview {#concept_dkx_rn3_wdb .concept}

## Quick start process {#section_wyp_sn3_wdb .section}

When purchasing and using Elastic Compute Service \(ECS\) instances, as an enterprise-level user, you must finish the following operations:

-   [Select configurations](reseller.en-US/Quick Start for Enterprise-Level Users/Select configuration.md#).
-   [Estimate costs](reseller.en-US/Quick Start for Enterprise-Level Users/Estimate costs.md#).
-   [Plan networks](reseller.en-US/Quick Start for Enterprise-Level Users/Plan networks.md#).
-   [Configure a security group](reseller.en-US/Quick Start for Enterprise-Level Users/配置安全组.md#).
-   [Automatic snapshot policies](reseller.en-US/Quick Start for Enterprise-Level Users/Automatic snapshot policies.md#).
-   [Image migration](reseller.en-US/Quick Start for Enterprise-Level Users/Image migration.md#).
-   [Implement high availability by using Server Load Balancer](reseller.en-US/Quick Start for Enterprise-Level Users/Implement high availability by using Server Load Balancer.md#).

## Target readers {#section_zyp_sn3_wdb .section}

The Quick Start is a reference for anyone who wants to know how to:

-   Select configurations for ECS instances.
-   Estimate costs of a large-sized instance and specific configuration.
-   Perform network planning for a specific solution.
-   Configure the security group information for each instance.
-   Select and develop better snapshot policies.
-   Complete image migration.

## Locate resources {#section_bzp_sn3_wdb .section}

|Procedure|Interface|Parameter|Target data|
|:--------|:--------|:--------|:----------|
|1. Query regions.|[DescribeRegions](../../../../reseller.en-US/API Reference/Regions/DescribeRegions.md#)|N/A|Region ID \(RegionId\)|
|2. Query zones.|[DescribeZones](../../../../reseller.en-US/API Reference/Regions/DescribeZones.md#)|Region ID|Zone ID \(ZoneId\)|
|3. Determine the billing method.|[DescribeZones](../../../../reseller.en-US/API Reference/Regions/DescribeZones.md#)|Billing method/Bidding policy|[ZoneType](../../../../reseller.en-US/API Reference/Data type/ZoneType.md#)|
|4. Query resource combinations.|[DescribeZones](../../../../reseller.en-US/API Reference/Regions/DescribeZones.md#)|RegionId/Billing method|[ZoneType](../../../../reseller.en-US/API Reference/Data type/ZoneType.md#)|

This document is applicable only to operations performed in the console. If you are an API user, see [API references](../../../../reseller.en-US/API Reference/Introduction.md#).

