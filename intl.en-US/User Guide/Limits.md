# Limits {#concept_gvb_h1w_tdb .concept}

When using ECS, note the following limitations:

-   ECS does not support virtual application installation or revirtualization \(such as installation of VMware\). Currently, only [ECS Bare Metal Instance and Super Computing Clusters](../../../../../reseller.en-US/Product Introduction/Instances/ECS Bare Metal Instance and Super Computing Clusters.md#) support revirtualization.
-   ECS does not support sound card applications.
-   ECS does not support external hardware devices directly \(such as dongles, USB drives, or external hard drives\). Instead, it supports a software protection dongle or two-step verification with dynamic passwords.
-   ECS does not support IP address translation services such as SNAT. Instead, it supports a VPN or proxy.
-   ECS does not support multicast protocols. If multicasting services are required, we recommend that you use point-to-point unicast instead.
-   Currently, Log Service does not support 32-bit Linux ECS instances. For information about regions that support Log Service, see [Service endpoint](../../../../../reseller.en-US/API Reference/Service endpoint.md#). For information about operating systems that support Log Service, see [Overview](../../../../../reseller.en-US/User Guide/Logtail collection/Overview/Overview.md#).

In addition to the preceding limits, the following table details further limits of ECS and states whether you can open a ticket to request changing the limits.

## ECS instances {#section_tbg_zdx_wdb .section}

|Item|Limitation|Can I open a ticket to change the limitation?|
|:---|:---------|:--------------------------------------------|
|Instance types for which you can create Pay-As-You-Go instances|Instance types with less than 16 vCPUs|Yes|
|Default quota of launch templates in each region for one account|30|No|
|Default quota of versions of one launch template|30|No|
|Switch from Pay-As-You-Go to Subscription|The following instance types \(families\) are not supported: t1, s1, s2, s3, c1, c2, m1, m2, n1, n2, and e3.|No|
|Switch from Subscription to Pay-As-You-Go| -   Depends on the membership level
-   5,000 vCPUs × hours for each month. The quota increases with membership levels.
-   Maximum refund limit per month \(varies with the membership level\).

 |No|

## Block storage {#section_xlb_32x_wdb .section}

|Item|Limitation|Can I open a ticket to change the limitation?|
|:---|:---------|:--------------------------------------------|
|Default quota of Pay-As-You-Go cloud disks in all regions for one account|Number of Pay-As-You-Go instances in all regions under the user account × 5|Yes|
|Default quota of system disks for one instance|1|No|
|Default quota of data disks for one instance|16 \(including cloud disks and Shared Block Storage\)|No|
|Default quota of instances to which one Shared Block Storage can be attached|8|No|
|Default quota of Shared Block Storage in all regions for one account|10|Yes|
|Capacity of one Basic Cloud Disk|5 GiB−2,000 GiB|No|
|Capacity of one SSD Cloud Disk|20 GiB−32,768 GiB|No|
|Capacity of one Ultra Cloud disk|20 GiB−32,768 GiB|No|
|Capacity of one local SSD disk|5 GiB−800 GiB|No|
|Capacity of local SSD disks for one instance|1,024 GiB|No|
|Capacity of one local NVMe SSD disk|1,456 GiB|No|
|Capacity of local NVMe SSD disks for one instance|2,912 GiB|No|
|Capacity of one local SATA HDD disk|5,500 GiB|No|
|Capacity of local SATA HDD disks for one instance|154,000 GiB|No|
|Capacity of one SSD Shared Block Storage|32,768 GiB|No|
|Capacity of SSD Shared Block Storage for one instance|128 TiB|No|
|Capacity of one Ultra Shared Block Storage|32,768 GiB|No|
|Capacity of Ultra Shared Block Storage for one instance|128 TiB|No|
|Capacity of one ESSD disk|32,768 GiB|No|
|Capacity of one system disk| -   Windows: 40 GiB−500 GiB
-   Linux \(excluding CoreOS\) and FreeBSD: 20 GiB−500 GiB
-   CoreOS: 30 GiB−500 GiB

 |No|
|Capacity of one data disk| -   Basic Cloud Disk: 5 GiB−2,000 GiB
-   SSD Cloud Disk/Ultra Cloud Disk/SSD Shared Block Storage/Ultra Shared Block Storage: 20 GiB−32,768 GiB
-   Local disk: dependent on specific disks

 |No|
|Attach a new local disk to an instance with local disks|This feature is not supported.|No|
|Change configuration of an instance with local disks|Only bandwidth changes are allowed.|No|
|System disk mount points|/dev/xvda|No|
|Data disk mount points|/dev/xvd\[b-z\]|No|

**Note:** Block storage capacity is measured in binary units. 1 KiB is *1,024 bytes*. 1 MiB is 1,024 KiB. 1 GiB is 1,024 MiB. 1 TiB is 1,024 GiB.

## Snapshots {#section_bxk_n2x_wdb .section}

|Item|Limitation|Can I open a ticket to change the limit?|
|:---|:---------|:---------------------------------------|
|Quota of snapshots|Each cloud disk and Shared Block Storage can have up to 64 snapshots|No|

## Images {#section_jnw_r2x_wdb .section}

|Item|Limitation|Can I open a ticket to change the limit?|
|:---|:---------|:---------------------------------------|
|Quota of custom images in one region for one account|100 \(increases with membership levels\)|Yes|
|Maximum number of users with whom a single image can be shared|50|Yes|
|Usage of images on instance types|32-bit images are not supported on an instance with 4 GiB or more RAM.|No|

## Key pairs {#section_dxw_s2x_wdb .section}

|Item|Limitation|Can I open a ticket to change the limit?|
|:---|:---------|:---------------------------------------|
|Quota of key pairs in one region for one account|500|No|
|Instance types supporting key pairs|All instance types except non-I/O optimized instance types in Generation I|No|
|Images supporting key pairs|Linux images only|No|

## Internet bandwidth {#section_og5_t2x_wdb .section}

|Item|Limitation|Can I open a ticket to change the limit?|
|:---|:---------|:---------------------------------------|
|Change the assigned Internet address for one instance|The instance has existed for less than six hours. You can change the Internet address of an instance three times.|No|

## Security groups {#section_mzr_52x_wdb .section}

|Item|Limitation|Can I open a ticket to change the limit?|
|:---|:---------|:---------------------------------------|
|Quota of security groups in one region for an account| 100 \(increases with membership levels\)

 |Yes|
|Quota of instances/IP addresses for one security group| -   Security groups for classic network instances: 1,000 classic network instances
-   Security groups for VPC instances: 2,000 private IP addresses \(shared by primary and secondary network cards\)

 |No|
|Quota of security groups to which each Elastic Network Interface \(ENI\) belongs for one instance|500|No|
|Quota of security groups to which each Elastic Network Interface \(ENI\) belongs for one instance|5|Open a ticket to raise the upper limit to 10 or 16|
|Quota of rules for one security group|100|No It decreases as the security group quota increases. For detailed restrictions, see [Security groups](../../../../../reseller.en-US/Product Introduction/Network and security/Security groups.md#)|
|Port|For the outbound Internet traffic, the default STMP port is 25, which is disabled by default and cannot be enabled through security group rules.|Open a ticket to enable it. For more information, see [Request for enabling TCP port 25.](https://partners-intl.aliyun.com/help/doc-detail/56130.htm)|

## Deployment sets {#section_wcf_hbs_2fb .section}

|Item|Limit|Can I open a ticket to change the limit?|
|:---|:----|:---------------------------------------|
|Quota of deployment sets in one region for an account|2|No|
|The number of instances that can be included in a deployment set|Seven instances are allowed in one zone. The number of instances allowed in one region equals the number of zones × 7.|No|
|Instance types that can be created in a deployment set|c5, g5, hfc5, hfg5, r5, se1ne, sn1ne, and sn2ne|No|

## ENIs {#section_gfq_v2x_wdb .section}

|Item|Limit|Can I open a ticket to change the limit?|
|:---|:----|:---------------------------------------|
|Quota of ENIs in one region for one account| 100 \(increases with membership levels\)

 |Yes|

## Tags {#section_npm_w2x_wdb .section}

|Item|Limit|Can I open a ticket to change the limit?|
|:---|:----|:---------------------------------------|
|Quota of tags that can be bound to one instance|20|No|

## API {#section_glg_x2x_wdb .section}

|Item|Limit|Can I open a ticket to change the limit?|
|:---|:----|:---------------------------------------|
|Quota of CreateInstance calls|200 times per minute|Yes|

**Note:** For the limits of VPC products, see [Limits](../../../../../reseller.en-US/Product Introduction/Limits.md#).

