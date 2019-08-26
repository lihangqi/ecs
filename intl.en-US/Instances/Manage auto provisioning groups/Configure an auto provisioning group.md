# Configure an auto provisioning group {#concept_744276 .concept}

This topic describes the factors to consider when you configure an auto provisioning group and the process to deploy an instance cluster. In addition, this topic provides configuration solutions for common scenarios.

## Procedure to configure an auto provisioning group {#section_vw0_65u_zwc .section}

You can refer to the following ideas to determine the details of configuring an auto provisioning group. For information about configuration items, see [Create an auto provisioning group](reseller.en-US/Instances/Manage auto provisioning groups/Create an auto provisioning group.md#).

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/236159/156173445348807_en-US.png)

## Process to deploy an instance cluster {#section_yq5_sbg_zme .section}

After an auto provisioning group is started, the instance cluster is automatically deployed based on the group configurations. The deployment process is as follows:

1.  The auto provisioning group tries to fulfill the target capacities of preemptible instances and pay-as-you-go instances.
    -   Preemptible instances:
        -   If **Cost Optimization** is specified as the scale-out policy, the auto provisioning group selects an instance type with the lowest cost and creates instances of that type. If **Instance Types Allowed by Cost Optimization Policy** is set, the auto provisioning group selects a specified number of instance types with the lowest cost and creates instances of those types. For example, if **Instance Types Allowed by Cost Optimization Policy** is set to 2, the auto provisioning group selects the two instance types with the lowest cost and creates instances of those types.
        -   If **Distribution Balancing** is specified as the scale-out policy, the auto provisioning group creates instances of the selected types and then distributes them evenly among specified zones.

            **Note:** Preemptible instances are reclaimed based on instance types, and instance resources in the same instance family are shared. If you select Distribution Balancing, we recommend that you configure different instance families to avoid all instances being reclaimed at the same time and ensure the cluster remains highly available.

    -   Pay-as-you-go instances:
        -   If **Cost Optimization** is specified as the scaling-out policy, the auto provisioning group selects an instance type with the lowest cost and creates instances of that type.
        -   If **Priority-based** is specified as the scale-out policy, the auto provisioning group creates instances based on the configured priorities of the instance types.
2.  If the specified target capacities of preemptible and pay-as-you-go instances do not meet the target capacity requirements of the cluster, the auto provisioning group creates new instances based on **Default Billing Method of Supplemental Instances** to meet the capacity requirements.
3.  If **Continuous Delivery and Maintain Capacity** is selected, the auto provisioning group continuously compares real-time and target capacities. If any of the target capacities has not been met, the auto provisioning group creates instances when resources are available to meet the target capacity.

## Example of machine learning scenarios {#section_qfz_a7u_zsu .section}

Assume that you plan to complete a machine learning task in the next week. The task is used to analyze risk factors for mortgage loans. You have the following requirements for the instance cluster:

-   The minimum computing power of a single node is 8 vCPUs and 60 GiB.
-   The target computing power of the cluster must be 10 times the minimum computing power of a single node.
-   To reduce costs, only preemptible instances can be used. It is acceptable if the instance cluster capacity does not reach the target capacity.
-   Instances must be released after the task is completed.

Considering the preceding requirements, the following configurations are used.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/236159/156173445348841_en-US.png)

The following two solutions can meet capacity requirements:

-   Ten ecs.gn5-c8g1.2xlarge instances
-   Five ecs.gn5-c8g1.4xlarge instances

When using the Cost Optimization policy to create preemptible instances, the auto provisioning group compares the required costs of each solution for the instance cluster. The solution with the lowest cost is then selected to implement a one-time delivery to the cluster. If the actual instance cluster capacity does not reach the target capacity, the auto provisioning group does not create new instances again.

## Example of ticketing website scenarios {#section_lse_fv9_c5r .section}

Assume that you need to build a ticketing website to provide reliable ticketing services at all hours, especially during peak hours, and have the following requirements for the instance cluster:

-   The minimum computing power of a single node is 8 vCPUs and 16 GiB.
-   The target computing power of the cluster must be 30 times the minimum computing power of a single node.
-   The minimum computing power of the cluster must be 20 times the minimum computing power of a single node.
-   The website access experience is optimized based on the minimum computing requirements of the cluster to minimize costs.
-   The cluster must have disaster recover capabilities.

Considering the preceding requirements, the following configurations are used.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/236159/156173445348846_en-US.png)

The Distribution Balancing policy is used to create preemptible instances. To meet the requirements for distribution balancing, the auto provisioning group creates instances in each zone. Additionally, the computing power of the instances created by the auto provisioning group must meet the overall computing power requirements. The following combination is used as an example:

-   One ecs.c5.2xlarge instance, two ecs.c5.4xlarge instances, one ecs.sn1ne.2xlarge instance, and two ecs.sn1ne.4xlarge instances
-   Three ecs.c5.2xlarge instances, one ecs.c5.4xlarge instance, three ecs.sn1ne.2xlarge instances, and one ecs.sn1ne.4xlarge instance

The Cost Optimization policy is used to create pay-as-you-go instances. The following available solutions meet capacity requirements:

-   Twenty ecs.c5.2xlarge instances
-   Ten ecs.c5.4xlarge instances
-   Twenty ecs.sn1ne.2xlarge instances
-   Ten ecs.sn1ne.4xlarge instances

The auto provisioning group compares the costs required to deliver pay-as-you-go instances using each solution, and uses the lowest-cost solution to deliver the instance cluster.

In Continuous Delivery and Maintain Capacity mode, the auto provisioning group continuously compares the real-time capacities and target capacities. If preemptible instances fail to be created or are reclaimed, the auto provisioning group creates instances to meet the capacity requirements when resources are available.

