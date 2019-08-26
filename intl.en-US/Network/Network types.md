# Network types {#concept_nfj_dz2_5db .concept}

Alibaba Cloud provides classic network and Virtual Private Cloud \(VPC\) network types.

## Virtual Private Cloud \(VPC\) {#section_ix4_gfw_ydb .section}

VPCs are logically isolated networks established in Alibaba Cloud. You can customize the topology and IP addresses in a VPC. We recommend that the VPC network type is used if have high network security requirements.

For more information about VPC, see [Virtual Private Cloud](../../../../../intl.en-US/Product Introduction/What is VPC?.md#) documentation.

## Classic network {#section_jx4_gfw_ydb .section}

A classic network is deployed in the public infrastructure of Alibaba Cloud, which is responsible for its planning and management. We recommend that the classic network type is used if your business requirements are high in terms of network usability.

**Note:** If you purchased an ECS instance after 17:00 \(UTC+8\) on June 14, 2017, you cannot choose the classic network type.

## VPC vs. Classic networks {#section_kx4_gfw_ydb .section}

The following table describes key network functions and indicates whether they are supported within VPCs and classic networks.

|Items|VPC|Classic network|
|:----|:--|:--------------|
|Two-layer logic isolation|Supported|Not supported|
|Custom private network blocks|Supported|Not supported|
|Private IP addresses|Unique within one VPC. Replicable between VPCs.|Unique in the global Classic network|
|Communicate within or between private networks|Able to communicate within a VPC, but isolated between VPCs|Able to communicate in one region and under one account|
|Tunneling|Supported|Not supported|
|Custom router|Supported|Not supported|
|Routing table|Supported|Not supported|
|Switches|Supported|Not supported|
|SDN|Supported|Not supported|
|Self-built NAT gateway|Supported|Not supported|
|Self-built VPN|Supported|Not supported|

