# IP addresses of a classic network-connected ECS instance {#concept_lky_f3w_ydb .concept}

IP addresses are mainly used for remote access to your instance or to the services deployed on your instance. Currently, for ECS instances of the classic network type, IP addresses are distributed in a unified way and divided into public and private IP addresses.

## Intranet IP addresses {#section_dlg_g3w_ydb .section}

Each classic network-connected ECS instance is assigned an intranet IP address.

**Scenarios**

Intranet IP addresses can be used in the following scenarios:

-   Load balancing
-   Mutual intranet access between ECS instances
-   Mutual intranet access between ECS instances and other cloud services, such as OSS and RDS

Communication traffic through intranet IP addresses within an intranet is free of charge. For more information, see [Intranet](reseller.en-US/Product Introduction/Network and security/Intranet.md#).

**Modify an intranet IP address**

Once a classic network-connected ECS instance is created, you cannot change its intranet IP address.

**Note:** Do not change an intranet IP address within a guest operating system. Otherwise, communication within an intranet is interrupted.

## Public IP addresses {#section_hlg_g3w_ydb .section}

If you purchase bandwidth for Internet access, a public IP address is assigned to your classic network-connected ECS instance. You cannot change the public IP address once it is assigned.

**Scenarios**

A public IP address is used in the following scenarios:

-   Mutual access between an ECS instance and the Internet
-   Mutual Internet access between ECS instances and other Alibaba Cloud services

**Assign a public IP address**

When you create an ECS instance, a public IP address is assigned to it if **Assign public IP** is selected.

For a Subscription instance with no public IP address, you can use the [Upgrade Configuration](../../../../reseller.en-US/User Guide/Instances/Change configurations/Upgrade configurations of Subscription instances.md) or the [Renew for Configuration Downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md) feature to purchase public network bandwidth.

**Note:** 

-   For a Pay-As-You-Go classic network-connected ECS instance with no public IP address, you cannot assign a public IP address after the instance is created.
-   For a classic network-connected ECS instance, you cannot unbind or release its public IP address once the IP address is assigned. If you set the bandwidth to 0 Mbit/s when renewing an instance for configuration downgrade, in the next purchase cycle, the public IP address is retained, but the instance cannot access the Internet.

**Billing**

You are billed for usage of Internet outbound traffic only. For more information, see [Billing of network bandwidth](../../../../reseller.en-US/Pricing/Billing of network bandwidth.md).

## Multicast and broadcast {#section_nlg_g3w_ydb .section}

Intranet IP addresses cannot be used for multicast or broadcast.

