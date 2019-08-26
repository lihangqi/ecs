# Limitations {#concept_gvb_h1w_tdb .concept}

When using ECS, note the following limitations:

-   ECS instances do not support virtual application installation or revirtualization \(such as installation of VMware\). Currently, only [ECS Bare Metal Instance and Super Computing Clusters](../../../../reseller.en-US/Product Introduction/Instances/ECS Bare Metal Instance and Super Computing Clusters.md#) supports revirtualization.
-   ECS instances do not support sound card applications.
-   You cannot mount external hardware devices directly \(such as hardware dongles, USB drives, external hard drives, and the USB security keys issued by banks\). Instead, use a software protection dongle or two-step verification with dynamic passwords.
-   ECS does not support IP packet address translation services such as SNAT. Instead, use a VPN or proxy.
-   ECS does not support multicast protocols. If multicasting services are required, we recommend that you use point-to-point unicast instead.
-   Currently, Log Service does not support 32-bit Linux ECS instances. For information about regions that support Log Service, see [Service endpoint](../../../../reseller.en-US/API Reference/Service endpoint.md#). For information about operating systems that support Log Service, see [Overview](../../../../reseller.en-US/User Guide/Logtail collection/Overview.md#) .

In addition to the preceding limitations, the following table details further limitations of ECS and states whether you can submit a ticket to request changing the limitation.

## ECS instances {#section_tbg_zdx_wdb .section}

|Item|Limitation|Can I open a ticket to raise the limitation?|
|:---|:---------|:-------------------------------------------|
|Instance types for which you can create Pay-As-You-Go instances|Instance types with less than 16 vCPUs|Yes|
|Default quota of launch templates in each region for one account|30|No|
|Default quota of versions of one launch template|30|No|
|Switch from Pay-As-You-Go to Subscription|The following instance types \(families\) are not supported: t1, s1, s2, s3, c1, c2, m1, m2, n1, n2, e3|No|

## Block storage {#section_xlb_32x_wdb .section}

|Item|Limitation|Can I open a ticket to raise the limitation?|
|:---|:---------|:-------------------------------------------|
|Create Pay-As-You-Go cloud disks|Complete real-name registration before creating cloud disks in any mainland China regions|No|
|Default quota of Pay-As-You-Go cloud disks in all regions for one account|Number of Pay-As-You-Go instances in all regions under the user account × 5|Yes|
|Quota of system disks for one instance|1|No|
|Quota of data disks for one instance|16 \(including cloud disks and Shared Block Storage\) |No|
|Quota of instances to which one shared block storage can be attached|8|No|
|Quota of shared block storage in all regions for one account |10|Yes|
|Capacity of one Basic Cloud Disk|5 GiB-2,000 GiB|No|
|Capacity of one SSD Cloud Disk|20 GiB-32,768 GiB|No|
|Capacity of one Ultra Cloud disk |20 GiB-32,768 GiB|No|
|Capacity of one local SSD disk|5 GiB-800 GiB|No|
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
-   Local disk: Dependent on specific disks

 |No|
|Attach a new local disk to an instance with local disks|This feature is not supported|No|
|Change configuration of an instance with local disks|Only bandwidth changes allowed|No|
|System disk mount points|/dev/xvda|No|
|Data disk mount points|/dev/xvd\[b-z\]|No|

## Snapshots {#section_bxk_n2x_wdb .section}

|Item|Limitation|Can I open a ticket to raise the limitation?|
|:---|:---------|:-------------------------------------------|
|Quota of snapshots|Number of elastic block storage devices × 64|No|

## Images {#section_jnw_r2x_wdb .section}

|Item|Limitation|Can I open a ticket to raise the limitation?|
|:---|:---------|:-------------------------------------------|
|Quota of custom images in all regions for one account|100 \(increases with membership levels\)|Yes|
|Maximum number of users with whom a single image can be shared|50|Yes|
|Usage of images on instance types|32-bit images are not supported on an instance with 4 GiB or more RAM.|No|

## Key pairs {#section_dxw_s2x_wdb .section}

|Item|Limitation|Can I open a ticket to raise the limitation?|
|:---|:---------|:-------------------------------------------|
|Quota of key pairs in all regions for one account|500|No|
|Instance types supporting key pairs|All instance types except for non-I/O optimized instance types in Generation I|No|
|Images supporting key pairs|Linux images only|No|

## Internet bandwidth {#section_og5_t2x_wdb .section}

|Item|Limitation|Can I open a ticket to raise the limitation?|
|:---|:---------|:-------------------------------------------|
|Maximum inbound Internet bandwidth|200 Mbit/s|No|
|Change the assigned public IP address for one instance|The instance has existed for less than six hours. You can change the public IP address of an instance three times.|No|

## Security group {#section_mzr_52x_wdb .section}

|Item|Limitation|Can I open a ticket to raise the limitation?|
|:---|:---------|:-------------------------------------------|
|Quota of instances/IP for one security group| -   Security groups for classic network instances: 1,000 classic network instances
-   Security groups for VPC instances: 2,000 private IP \(shared by primary and secondary network cards\)

 |No|
|Quota of authorization rules for one security group|100|No|
|Quota of security groups in a region for an account| 100 \(increases with membership levels\)

 |Yes|
|Quota of security groups to which each elastic network interface belongs for one instance|5|Yes|
|Port|For the outbound Internet traffic, the default STMP port is 25, which is disabled by default and cannot be enabled through security group rules.|Yes. For more information, see [Request for enabling TCP port 25 .](https://partners-intl.aliyun.com/help/doc-detail/56130.htm)|

## ENI {#section_gfq_v2x_wdb .section}

|Item|Limitation|Can I open a ticket to raise the limitation?|
|:---|:---------|:-------------------------------------------|
|Quota of ENIs in one region for one account| 100 \(increases with membership levels\)

 |Yes|

## Label {#section_npm_w2x_wdb .section}

|Item|Limitation|Can I open a ticket to raise the limitation?|
|:---|:---------|:-------------------------------------------|
|Quota of tags that can be bound to one instance|20|No|

## API {#section_glg_x2x_wdb .section}

|Item|Limitation|Can I open a ticket to raise the limitation?|
|:---|:---------|:-------------------------------------------|
|Quota of CreateInstance calls|200 times per minute|Yes|

**Note:** For more information about limitations of VPC products, see [Limits](../../../../reseller.en-US/Product Introduction/Limits.md#).

