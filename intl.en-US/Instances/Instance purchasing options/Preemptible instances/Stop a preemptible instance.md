# Stop a preemptible instance {#concept_k4c_5rw_wgb .task}

This topic describes how to stop a preemptible instance and whether it can start successfully after being stopped in different conditions.

Only preemptible instances in a VPC support the [No fees for stopped VPC instances](../reseller.en-US/Pricing/No fees for stopped VPC instances.md#) feature. The network type, bidding mode, and stop mode of an instance combine to determine whether a preemptible instance can restart successfully. The following table provides the details.

|Network type|Bidding mode|Stop mode|Can the stopped instance be restarted?|
|:-----------|:-----------|---------|:-------------------------------------|
|Classic network|SpotWithPriceLimit|Keep Stopped Instances and Continue Billing|During the guaranteed duration, the instance can be restarted successfully. However, after the guaranteed duration, the instance can only be restarted successfully if your bid is not lower than the market price and if the number of resources is sufficient.|
|SpotAsPriceGo|Keep Stopped Instances and Continue Billing|During the guaranteed duration, the instance can be restarted successfully. However, after the guaranteed duration, the instance cannot be restarted if the number of resources is insufficient.|
|VPC|SpotWithPriceLimit|Keep Stopped Instances and Continue Billing|During the guaranteed duration, the instance can be restarted successfully. However, after the guaranteed duration, the instance can only be restarted successfully if your bid is not lower than the market price and if the number of resources is sufficient.|
|Stop/Force Stop \(no fees will be incurred if either of the options is selected\)|During the guaranteed duration, the instance can be restarted successfully as long as the number of resources is sufficient. However, after the guaranteed duration, the instance can only be restarted successfully if your bid is not lower than the market price and if the number of resources is sufficient.|
|SpotAsPriceGo|Keep Stopped Instances and Continue Billing|During the guaranteed duration, the instance can be restarted successfully. However, after the guaranteed duration, the instance cannot be restarted if the number of resources is insufficient.|
|Stop/Force Stop \(no fees will be incurred if either of the options is selected\)|During the guaranteed duration, the instance can be restarted successfully as long as the number of resources is sufficient. However, after the guaranteed duration, the instance cannot be restarted if the number of resources is insufficient.|

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  On the Instances page, find the preemptible instance to be stopped. In the **Actions** column, choose **More** \> **Instance Status** \> **Stop**.
4.  In the Stop Instance dialog box, click **OK**.

**More information**  


[StopInstance](../reseller.en-US/API Reference/Instances/StopInstance.md#)

