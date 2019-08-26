# Limits {#concept_gvb_h1w_tdb .concept}

This topic describes the service limits of ECS, and how to apply for exceptions to some limits.

## Overview {#section_nxc_2zs_2gb .section}

ECS has the following service limits:

-   You cannot install virtualization software, such as VMware Workstation, or use it for re-virtualization. Only [ECS Bare Metal Instance](reseller.en-US/Instances/Instance type families/ECS bare metal instance type family/EBM Instance overview.md#) and [Super Computing Cluster](../../../../reseller.en-US/Instances/Instance type families/Super Computing Cluster instance type family/Super Computing Clusters.md#) support re-virtualization.
-   ECS does not support sound card applications.
-   External hardware devices, such as hardware dongles, USB flash drives, external hard disks, and hardware tokens, cannot be attached directly. Software verification methods such as two-factor authentication and dynamic passwords can be used.
-   ECS does not support IP address translation services such as SNAT. Instead, it achieves this function using VPNs and proxies.
-   ECS does not support multicast protocols. We recommend that you use unicast instead.
-   Log Service does not support 32-bit Linux ECS instances. For information about regions that support Log Service, see [Endpoints](../../../../reseller.en-US/API Reference/Service endpoint.md#). For information about operating systems that support Log Service, see [Overview](../../../../reseller.en-US/User Guide/Logtail collection/Overview/Overview.md#).

## Instances {#section_tbg_zdx_wdb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Permissions to create instances|To create ECS instances in any mainland China regions, you must first complete real-name authentication|Not applicable|
|Instance types that can be created as pay-as-you-go instances|Instance types with less than 16 vCPUs|Submit a ticket|
|Total number of vCPUs of all pay-as-you-go instances in each region for an account|50 vCPUs You can view the quotas by clicking **Privileges & Quota Management** on the Overview page in the console.

 |Submit a ticket|
|Total number of vCPUs of all preemptible instances in each region for an account|0 vCPUs. Submit a ticket to apply for a quota. A maximum of 50 vCPUs can be allocated. You can view the quotas by clicking **Privileges & Quota Management** on the Overview page in the console.

 |Submit a ticket|
|Total number of launch templates in each region for an account|30|Not applicable|
|Total number of versions of each launch template|30|Not applicable|
|Switch billing methods from pay-as-you-go to subscription|Not supported by the following instance types \(families\): t1, s1, s2, s3, c1, c2, m1, m2, n1, n2, and e3|Not applicable|
|Switch billing methods from subscription to pay-as-you-go| -   Only supported by some accounts \(based on actual ECS usage\)
-   5,000 vCPU hours each month
-   A maximum monthly refund limit is set. For more information about the refund limit, see the Switch to page.

 |Not applicable|

## Block storage {#section_xlb_32x_wdb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Permissions to create pay-as-you-go cloud disks|To create cloud disks in any mainland China regions, you must first complete [real-name authentication](https://www.alibabacloud.com/help/doc-detail/52595.htm)|Not applicable|
|Total number of all pay-as-you-go cloud disks in all regions for an account|Total number of all pay-as-you-go instances in all regions for an account × 5|Submit a ticket|
|Total number of system disks for each instance|1|Not applicable|
|Maximum number of data disks for each instance|16 \(both cloud disks and shared block storage devices\)|Not applicable|
|Number of instances to which each shared block storage device can be attached|8|Not applicable|
|Total number of shared block storage devices in all regions for an account|10|Submit a ticket|
|Basic disk capacity|5 GiB to 2,000 GiB per disk|Not applicable|
|SSD disk capacity|20 GiB to 32,768 GiB per disk|Not applicable|
|Ultra disk capacity|20 GiB to 32,768 GiB per disk|Not applicable|
|Local SSD disk capacity|5 GiB to 800 GiB per disk|Not applicable|
|Total capacity of all local SSD disks for each instance|1,024 GiB per disk|Not applicable|
|Local NVMe SSD disk capacity|1,456 GiB per disk|Not applicable|
|Total capacity of all local NVMe SSD disks for each instance|2,912 GiB per disk|Not applicable|
|Local SATA HDD disk capacity|5,500 GiB per disk|Not applicable|
|Total capacity of all local SATA HDD disks for each instance|154,000 GiB per disk|Not applicable|
|SSD shared block storage device capacity|32,768 GiB per disk|Not applicable|
|Total capacity of all SSD shared block storage devices for each instance|128 TiB per disk|Not applicable|
|Ultra shared block storage device capacity|32,768 GiB per disk|Not applicable|
|Total capacity of all ultra shared block storage devices for each instance|128 TiB per disk|Not applicable|
|ESSD disk capacity|32,768 GiB per disk|Not applicable|
|System disk capacity| -   Windows: 40 GiB to 500 GiB
-   Linux \(excluding CoreOS\) and FreeBSD: 20 GiB to 500 GiB
-   CoreOS: 30 GiB to 500 GiB

 |Not applicable|
|Data disk capacity| -   Basic disk: 5 GiB to 2,000 GiB per disk
-   SSD disk, ultra disk, SSD shared block storage device, or ultra shared block storage device: 20 GiB to 32,768 GiB per disk
-   Local disk: refer to disk type capacities

 |Not applicable|
|Attach new local disks to instances that have existing local disks|Not allowed|Not applicable|
|Change configuration of instances that have local disks|Only bandwidth can be changed|Not applicable|
|Data disk mount points|/dev/xvda|Not applicable|
|Data disk mount points|/dev/xvd\[b-z\]|Not applicable|

**Note:** Block storage capacity is measured in binary units. 1 KiB is 1,024 bytes. 1 MiB is 1,024 KiB. 1 GiB is 1,024 MiB. 1 TiB is 1,024 GiB.

## Snapshots {#section_bxk_n2x_wdb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Number of snapshots that can be created for each cloud disk and shared block storage device|64|Not applicable|

## Images {#section_jnw_r2x_wdb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Total number of custom images in each region for an account|100|Submit a ticket|
|Maximum number of users with whom a single image can be shared|50|Submit a ticket|
|Images supported by instance types|Instance types that have 4 GiB or more memory do not support 32-bit images.|Not applicable|

## Key pairs {#section_dxw_s2x_wdb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Total number of key pairs in each region for an account|500|Not applicable|
|Instance types that support key pairs|All instance types except non-I/O optimized instance types in Generation I|Not applicable|
|Images supporting key pairs|Linux images only|Not applicable|

## Public network bandwidth {#section_og5_t2x_wdb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Public network inbound bandwidth|200 Mbit/s|Not applicable|
|Public network outbound bandwidth| -   Subscription instance: up to 200 Mbit/s
-   Pay-as-you-go instance: up to 100 Mbit/s

 |Not applicable|
|Change the assigned public IP address of an instance|Within six hours after the instance has been created. You can change the public IP address of an instance up to three times.|Not applicable|

## Security groups {#section_mzr_52x_wdb .section}

|Item|Basic security group limits|Advanced security group limits|
|----|---------------------------|------------------------------|
|Total number of security groups in each region for an account|100 You can view the quotas by clicking Privileges & Quota Management on the Overview page in the console. You can open a ticket to apply for an exception to the limit.

 |Same as the basic security group limit|
|Number of classic-type ECS instances that can be included in a classic-type security group|1,000[\*](#)|Classic network is not supported|
|Number of VPC-type ECS instances that can be included in a VPC-type security group|Depends on the [number of private IP addresses in a VPC-type security group](#)|No limit|
|Number of security groups that can contain the same ECS instance|5 You can open a ticket to raise the limit to 10 or 16 security groups.

 |Same as the basic security group limit|
|Number of security groups that can contain the same ENI of an ECS instance|
|Maximum number of rules in a security group \(both inbound and outbound\)|100[\*\*\*](#)|Same as the basic security group limit|
|Maximum number of rules in all security groups that contain the same ENI \(both inbound and outbound\)|500|Same as the basic security group limit|
|Number of private IP addresses in a VPC-type security group|2000[\*\*](#)|No limit|
|Number of ENIs in a VPC-type security group|Depends on the [maximum number of rules in a security group](#)|50,000|
|Public network access port|The default STMP port for outbound traffic is port 25, which is disabled by default. It cannot be enabled by security group rules.|Same as the basic security group limit|

\* If more than 1,000 classic-type instances need access to each other, you can distribute them across multiple security groups and authorize mutual access.

\*\* If you require mutual access between more than 2,000 private IP addresses, you can distribute them across multiple security groups and authorize mutual access.

\*\*\* If you increase the number of security groups that can contain the same ECS instance, the maximum number of rules in a security group will decrease. The product of the number of security groups that can contain the same ECS instance and the maximum number of rules in a security group \(both inbound and outbound\) must be less than or equal to 500. For example, 5 × 100 = 500, 10 × 50 = 500, and 16 × 30 < 500.

## Deployment sets {#section_wcf_hbs_2fb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Total number of deployment sets in each region for an account|2|Not applicable|
|Total number of instances that can be included in a deployment set|Seven instances are allowed in a zone. The number of instances allowed in a region is 7 × number of zones.|Not applicable|
|Instance types that can be created in a deployment set|c5, g5, hfc5, hfg5, r5, se1ne, sn1ne, and sn2ne|Not applicable|

## Cloud Assistant {#section_qkq_mzs_2gb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Total number of Cloud Assistant commands in each region for an account|100|Submit a ticket|
|Total number of Cloud Assistant commands that can be used by an account each day in a region|5,000|Submit a ticket|

## ENIs {#section_gfq_v2x_wdb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Total number of ENIs in each region for an account|100 You can view the quotas by clicking **Privileges & Quota Management** on the Overview page.

 |Submit a ticket|

## Tags {#section_npm_w2x_wdb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Total number of tags that can be bound to an instance|20|Not applicable|

## API calls {#section_glg_x2x_wdb .section}

|Item|Limits|Exception application \(increase limit\)|
|:---|:-----|:---------------------------------------|
|Total number of CreateInstance calls|200 calls per minute|Submit a ticket|

**Note:** For more information about the VPC limits, see [Limits](../../../../reseller.en-US/Product Introduction/Limits.md#).

