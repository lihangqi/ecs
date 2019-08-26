# ECS instance life cycle {#concept_zg1_gv2_5db .concept}

The life cycle of an ECS instance begins when it is created and ends when it is released.

## Instance status {#section_p4f_dk5_ydb .section}

During this process, an instance may undergo several status changes as explained in the following table.

|Status|Status attribute|Description|Corresponding API status|Viewable in the console|
|:-----|:---------------|:----------|:-----------------------|:----------------------|
|Preparing|Intermediate|After an instance is created, it remains in this status before running. If an instance is in this status for a long time, an exception occurs.|Pending|No|
|Starting|Intermediate|An instance is in this status when it is either started or restarted in the console or by using an API before it is running. If an instance is in this status for a long time, an exception occurs.|Starting|Yes|
|Running|Stable|The instance is operating normally and can accommodate your business needs.|Running|Yes|
|Stopping|Intermediate|An instance is in this status after the stop operation is performed in the console or by using an API but before it actually stops. If an instance is in this status for a long time, an exception occurs.|Stopping|Yes|
|Stopped|Stable|The instance has been stopped properly. In this status, the instance cannot accommodate external services.|Stopped|Yes|
|Expired|Stable|A yearly or monthly subscribed instance is in this status if it expires because it has not been timely renewed. A Pay-As-You-Go instance is in this status only when you have an overdue payment. After an ECS instance expires, it continues running for 15 days, and the data on its disks is retained for additional 15 days, after which the instance will be released and the data will be permanently removed. In this status, the instance cannot accommodate external services.|Stopped|Yes|
|Expiring|Stable|A Subscription instance is in this status for 15 days before it expires.  After it is [renewed](https://www.alibabacloud.com/help/doc-detail/62604.htm), the instance is in the **Running**status.|Stopped|Yes|
|Locked|Stable|An instance is in this status because of an overdue account or security risks.  To unlock the instance, [open a ticket](https://workorder-intl.console.aliyun.com/#/ticket/createIndex).|Stopped|Yes|
|Release pending|Stable|A Subscription instance is in this status after you apply for a refund before it expires.|Stopped |Yes|

## API status changes {#section_apf_dk5_ydb .section}

The following figure illustrates API status changes of an instance within its life cycle.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9551/5105_en-US.png)

