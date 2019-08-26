# Isolation of instances within a security group {#concept_nkc_vfy_sfb .concept}

A security group is a virtual firewall that provides Stateful Packet Inspection \(SPI\) and packet filtering. It contains instances in the same region with the same security requirements and mutual trust. Alibaba Cloud provides various access control policies to allow you isolate instances within a security group.

## Intra-group isolation rules {#section_t3f_jky_sfb .section}

-   Network isolation in a security group is implemented between network interfaces, not between instances. If multiple Elastic Network Interfaces \(ENIs\) are bound to an instance, you need to set isolation rules for each ENI.

-   Instances in a security group can access each other by default, which is not changed by the isolation rules.

    Intra-group isolation rules are user-defined access control policies, and are invalid for the default security groups and new security groups. The default access control policy for a security group is: instances in the same security group can access each other over the intranet, while instances in different security groups cannot.

-   Intra-group isolation rules have the lowest priority.

    To isolate instances in a security group, make sure no intercommunication rules apply to them except for the isolation rules. In the following cases, instances can still access each other even though intra-group isolation rules are set:

    -   Intra-group isolation rules are set in a security group, while an Access Control List \(ACL\) that permits intra-group communication between instances is set at the same time.

    -   Intra-group isolation rules are set in a security group, while intra-group intercommunication is configured at the same time.

-   Intra-group isolation rules only apply to the instances in the current security group.


## Modify the access control policy {#section_tmy_scv_tfb .section}

You can use the [ModifySecurityGroupPolic](../../../../reseller.en-US/API Reference/Security groups/ModifySecurityGroupPolicy.md#) interface to modify the access control policy within a security group.

## Case analysis {#section_rdw_v4y_sfb .section}

The following figure shows the relationship between three instances and their security groups.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/61459/154389808331133_en-US.png)

In this example, Group1, Group2, and Group3 are three different security groups. ECS1, ECS2, and ECS3 are three different ECS instances. ECS1 and ECS2 belong to Group1 and Group2. ECS2 and ECS3 belong to Group3.

The intra-group intercommunication policies of the three security groups are as follows:

|Security group|Intra-group intercommunication policy|Instances included|
|:-------------|:------------------------------------|:-----------------|
|Group1|Isolated|ECS1 and ECS2|
|Group2|Interconnected|ECS1 and ECS2|
|Group3|Interconnected|ECS2 and ECS3|

The communication status between instances is as follows:

|Instance|Interconnected or isolated?|Reason|
|:-------|:--------------------------|:-----|
|ECS1 and ECS2|Interconnected|ECS1 and ECS2 belong to both Group1 and Group2. The policy of Group1 is "isolated", while that of Group2 is "interconnected". As intra-group isolation has the lowest priority, ECS1 and ECS2 are interconnected.|
|ECS2 and ECS3|Interconnected|Both ECS2 and ECS3 belong to Group3. The policy of Group3 is "interconnected", so ECS2 and ECS3 are interconnected.|
|ECS1 and ECS3|Isolated|ECS1 and ECS3 belong to different security groups. Instances in different security groups are not interconnected by default. To permit access between instances in two security groups, you can authorize security groups through security group rules.|

