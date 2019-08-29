# View resource overview {#concept_w2q_qhj_ygb .concept}

This topic describes how to view resource statistics on the Resource Overview page. The Resource Overview page displays the statistics for instance and storage resources. You can use the statistics to analyze and manage your resources.

## Limits {#section_nzw_mkh_1hb .section}

The Instance Overview page can be accessed by using an Alibaba Cloud account or a RAM user account. The Storage Overview page can be accessed only by using an Alibaba Cloud account.

## View instance statistics {#section_h1s_wwd_zgb .section}

1.  Use an Alibaba Cloud account or a RAM user account to log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  On the **Overview** page, click **Resource Overview**.
3.  On the **Instance Overview** page, select a region to view the instances in that region.

    You can view grouped instance statistics by clicking **Grouped By Network Type** or **Grouped by Tag**. You can also download the instance statistics by clicking the download icon in the upper-right corner of the Instance Overview page. The following instance statistics are collected:

    |Dimension|Description|
    |---------|-----------|
    |Status|View the number of instances in different states. You can click a state to go to the Instances page where the instances in that state are displayed.|
    |Instances expiring within 30 days|View the instances that will expire within 30 days. The 30 days are further divided into four time periods for you to better schedule instance renewal.|
    |Billing method|View the number of instances that use different billing methods. You can click a billing method to go to the Instances page where the instances using that billing method are displayed.|
    |Instance type|View the proportion of each instance family category and the proportion of each instance family under each category.You can view the proportions level by level, from instance family category to instance type to instance specifications. You can click an instance type to go to the Instances page where the instances of that instance type are displayed.

|
    |Zone|View the number of instances in each zone of the specified region. You can click a zone to go to the Instances page where the instances in that zone are displayed.|
    |Instances created last 30 days|View the number of instances created in the last 30 days.|
    |Instance image distribution|View the proportion of images used by instances.|


## View storage statistics {#section_s4t_1j2_zgb .section}

1.  Use an Alibaba Cloud account to log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  On the **Overview** page, click **Resource Overview**.
3.  On the **Resource Overview** page, click **Storage Overview** to view the storage statistics under this account.

    The following storage statistics are collected:

    |Dimension|Description|
    |---------|-----------|
    |Disk information overview|View the category, number, size, average size, the number in use, and mounting status of system disks and data disks.|
    |Stress data for the last 7 days|View the read/write stress distribution in the last seven days, measured in IOPS or bit/s. The number of disks in each read/write stress range is displayed. You can click Per vm to view the read/write stress data for all the disks that are attached to each ECS instance.|
    |Top devices in the last 7 or 30 days|You can view the top number of disks with the highest IOPS or bit/s and their trends in the last 7 or 30 days. You can also view the top number of ECS instances whose disks have the highest IOPS or bit/s.|
    |Zone distribution|View the number of disks and total disk size in each zone.|
    |Disk size distribution by zone|View the proportion of the size of each disk in each zone.|
    |Disk category distribution|View the number of disks in and the total disk size of each disk category.|
    |Disk size distribution by category|View the proportion of the size of each disk in each disk category.|


