# IP addresses of VPC-Connected ECS instances {#concept_olx_cjw_ydb .concept}

Each VPC-Connected ECS instance can communicate within an intranet by using a private IP address or over the Internet by using a public IP address.

## Private IP addresses {#section_zkh_djw_ydb .section}

Each VPC-Connected ECS instance is assigned a private IP address when it is created. That address is determined by the VPC and the CIDR block of the VSwitch to which the instance is connected.

## Scenarios {#section_alh_djw_ydb .section}

A private IP address can be used in the following scenarios:

-   Load balancing
-   Communication among ECS instances within an intranet
-   Communication between an ECS instance and other cloud products \(such as OSS and RDS\) within an intranet

For more information, see [Intranet](reseller.en-US/Product Introduction/Network and security/Intranet.md#).

## Modify a private IP address {#section_clh_djw_ydb .section}

To meet your business needs, you can modify the private IP address of a VPC-Connected ECS instance in the ECS console. For more information, see [Change the private IP of an ECS instance](../../../../reseller.en-US/User Guide/Instances/Change IP addresses/Change the private IP of an ECS instance.md#).

## Public IP addresses {#section_dlh_djw_ydb .section}

VPC-Connected ECS instances support two public IP address types:

-   NatPublicIp, which is assigned to a VPC-Connected ECS instance, can be released only, and cannot be unbound from the instance.
-   Elastic public IP \(EIP\). For more information, see [What is an EIP address](../../../../reseller.en-US/Product Introduction/What is Elastic IP Address?.md#).

When a VPC-Connected ECS instance accesses the Internet, its public IP address is mapped to its private IP address through network address translation \(NAT\). 

You cannot find a network interface for Internet access by running commands within the operating system.

## Scenarios {#section_flh_djw_ydb .section}

NatPublicIp and EIP are applicable to different scenarios:

-   NatPublicIp: If you want to assign a public IP address to a VPC-Connected ECS instance when creating the instance and do not want to retain the public IP address when the instance is released, you can use a NatPublicIp address.

-   EIP: If you want to keep a public IP address and bind it to any of your VPC-Connected ECS instances in the same region, you can use an EIP address.


## Obtain a public IP address {#section_qnq_hsr_zdb .section}

-   NatPublicIp: When creating a VPC-Connected ECS instance, if you select **Assign a public IP**, a NatPublicIp is assigned to the instance when it is created.

-   EIP: You can apply for an EIP address and bind it to a VPC-Connected ECS instance. In this case, do not assign a NatPublicIp to an instance. For more information, see [Apply for an EIP address](../../../../reseller.en-US/User Guide/Create an EIP.md#).


## Release a public IP address {#section_hbl_4sr_zdb .section}

-   NatPublicIp: When a NatPublicIp address is assigned to an instance, you can only release the IP address, but cannot unbind it. Only a NatPublicIp address that is assigned to a Subscription instance can be released. For more information, see [Renew for configuration downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#).
-   EIP: If you do not need an EIP address, unbind it from a VPC-Connected ECS instance and release it in the EIP console. For more information, see [Unbind and release an EIP address](../../../../reseller.en-US/User Guide/Unbind and release an EIP.md#).

## Billing {#section_llh_djw_ydb .section}

You are billed for outbound Internet traffic usage only. For more information, see [Billing of network bandwidth](../../../../reseller.en-US/Pricing/Billing of network bandwidth.md#).

