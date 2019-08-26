# Instance type families that support instance type upgrades {#concept_mdh_2rb_1fb .concept}

This article describes the instance type families that support instance type upgrades.

## Restrictions {#section_sxr_zhb_1fb .section}

Upgrading instance types has the following impacts:

-   Classic network instances:

    -   For [phased-out instance types](https://help.aliyun.com/knowledge_detail/55263.html), when a non-I/O optimized instance is upgraded to an I/O optimized instance, changes are made to the private IP address, the driver name, and the software authorization code. For Linux instances, Basic Cloud Disks \(`cloud`\) are recognized as `xvda` or `xvdb`, while Ultra Cloud Disks \(`cloud_efficiency`\) and SSD Cloud Disks \(`cloud_ssd`\) are recognized as `vda` or `vdb`.

    -   For [available instance types](../../../../reseller.en-US/Product Introduction/Instance type families.md#), changes are made to the private IP address of the instance.

-   VPC instances:

    For [phased-out instance types](https://help.aliyun.com/knowledge_detail/55263.html), when a non-I/O optimized instance is upgraded to an I/O optimized instance, changes are made to the driver name and the software authorization code. For Linux instances, Basic Cloud Disks \(`cloud`\) are recognized as `xvda` or `xvdb`, while Ultra Cloud Disks \(`cloud_efficiency`\) and SSD Cloud Disks \(`cloud_ssd`\) are recognized as `vda` or `vdb`.


## Instance type families that support upgrading instance types {#section_ehm_smb_1fb .section}

**Note:** Each instance type is available only in specific zones. Before upgrading an instance type, check if the target instance type \(family\) is available in the current zone.

In the following table, the target instance type families apply to both Subscription and Pay-As-You-Go instances.

|Source instance type family|Target instance type family|
|:--------------------------|:--------------------------|
|g5, r5, c5, ic5| -   g5, r5, c5, ic5
-   sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, re4, t5, n4, mn4, xn4, e4

 |
|sn1ne, sn2ne, se1ne| -   sn1ne, sn2ne, se1ne
-   c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, e4

 |
|se1| -   se1
-   sn1, sn2, n1, n2, e3, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, e4

 |
|n4, mn4, xn4, e4| -   n4, mn4, xn4, e4
-   sn1, sn2, se1, n1, n2, e3, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5

 |
|re4| -   re4
-   sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, t5, n4, mn4, xn4, e4, ecs.se1.14xlarge

 |
|hfc5, hfg5| -   hfc5, hfg5
-   sn1ne, sn2ne, se1ne, c4, cm4, ce4, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, e4

 |
|gn4|gn4|
|gn5i|gn5i|
|gn6v|gn6v|
|t5| -   t5
-   sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, n4, mn4, xn4, e4

 |
|t1, s1, s2, s3, m1, m2, c1, c2| -   t1, s1, s2, s3, m1, m2, c1, c2
-   sn1, sn2, se1, n1, n2, e3, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, e4

 |
|n1, n2, e3| -   n1, n2, e3
-   sn1, sn2, se1, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, e4

 |
|sn1, sn2| -   sn1, sn2
-   se1, n1, n2, e3, sn1ne, sn2ne, se1ne, c4, cm4, ce4, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, e4

 |
|c4, ce4, cm4| -   c4, ce4, cm4
-   sn1ne, sn2ne, se1ne, hfc5, hfg5, g5, r5, c5, ic5, re4, t5, n4, mn4, xn4, e4

 |

