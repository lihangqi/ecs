# Preemptible instances {#concept_t3p_gv2_5db .concept}

Preemptible instances are a type of on-demand instances.

When you create a preemptible instance, you can set a maximum price per hour to bid for a specified instance type. If your bid is higher than or equal to the current market price, your instance is created and billed according to the current market price. You can hold a preemptible instance without interruption for at least one hour. After one hour, your bid is compared with the market price. When the market price exceeds your bid or the resource stock is insufficient, the instance is automatically released.

**Note:** After an instance is released, its data cannot be recovered. We recommend that you [create a snapshot](../../../../../reseller.en-US/User Guide/Snapshots/Create a snapshot.md#) for an instance to back up its data before releasing it.

## Scenarios {#section_fdc_jt5_ydb .section}

Preemptible instances are ideal for stateless applications, such as scalable Web services, figure rendering, big data analysis, and massively parallel computing. Furthermore, applications that require a higher level of distribution, scalability, and fault tolerance capabilities, benefit from preemptible instances in terms of costs and throughput.

You can use preemptible instances for the following scenarios:

-   Real-time analysis
-   Big data
-   Geological surveys
-   Image coding and media coding
-   Scientific computing
-   Scalable Web sites and Web crawlers
-   Image and media coding
-   Testing

Preemptible instances are not suitable for stateful applications, such as databases, because it is difficult to store application states if the instance is released because of a failed bid or other reasons.

## Life cycle {#section_a1v_5kd_yfb .section}

The following figure shows the life cycle of a preemptible instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9552/15504553315106_en-US.png)

## Bidding modes {#section_hdc_jt5_ydb .section}

You can bid for a preemptible instance only once. Moreover, you can bid in either of the following bidding modes:

-   **SpotAsPriceGo**

    This mode means you always set the real-time market price as the bidding price. Moreover, there is an upper limit for your bidding price, namely the price of the corresponding Pay-As-You-Go instance type.

    If you use the [ECS purchase page](../../../../../reseller.en-US/User Guide/Instances/Create an instance/Create a preemptible instance.md#) to create an instance, select **Use Automatic Bid**. If you use the [RunInstances](../../../../../reseller.en-US/API Reference/Instances/RunInstances.md#) interface to create an instance, set the `SpotStrategy` parameter to `SpotAsPriceGo`.

-   **SpotWithPriceLimit**

    This mode means you must set the highest price you are willing to pay for a specified instance type.

    If you use the [ECS purchase page](../../../../../reseller.en-US/User Guide/Instances/Create an instance/Create a preemptible instance.md#) to create an instance, select **Set Custom Maximum Price \(Per Instance/Hour\)**. If you use the [RunInstances](../../../../../reseller.en-US/API Reference/Instances/RunInstances.md#) interface to create an instance, set the `SpotStrategy` parameter to `SpotWithPriceLimit`.

    Currently, the maximum bid of a preemptible instance is the price of a Pay-As-You-Go instance of the same configuration. When creating a preemptible instance, you can set a price according to the displayed price range, business features, and the estimated future price fluctuation. When the market price is lower than or equal to your bid, and the resource stock is sufficient, the instance can be created. If your bid takes into account the estimated future price fluctuation, you can hold the instance even after the one-hour [guaranteed duration](#). Otherwise, your instance may be automatically released at any time after that duration.


## Guaranteed duration {#valid .section}

When a preemptible instance is created, it has a guaranteed duration of one hour, namely, the first hour after it is created. During this period, the instance will not be released because of stock shortage, and you can run services on the instance as normal. Beyond the guaranteed duration, the market price and stock is checked every five minutes. If the market price at any given point of time is higher than your bid or the instance type stock is insufficient, your preemptible instance will be automatically released.

## Price and billing {#section_mdc_jt5_ydb .section}

Preemptible instance price and billing considerations:

-   **Price** 

    The preemptible instance price applies to the instance type only, including vCPUs and memory, but does not include system disks, data disks, or network bandwidth.

    Instead, system disks and data disks are billed according to the [Pay-As-You-Go](../../../../../reseller.en-US/Pricing/Pay-As-You-Go.md#) billing method. Network bandwidth is billed according to the bandwidth billing rules of Pay-As-You-Go instances. For more information, see [Billing of Internet bandwidth](../../../../../reseller.en-US/Pricing/Billing of Internet bandwidth.md#).

-   **Billing method** 

    Preemptible instances are billed by the second. When a preemptible instance is created successfully, the market price is an hourly rate and you only need to divide it by 3,600 to get the price per second.

    The cost incurred from creating a preemptible instance to releasing it is accurate to two decimal places. An accrued cost of less than USD 0.01 is not charged.

-   **Billing duration** 

    Instances are billed according to the actual period of use. The actual period of use is the duration from instance creation to instance release. After an instance is released, it is no longer billed. If you stop an instance by using [StopInstance](../../../../../reseller.en-US/API Reference/Instances/StopInstance.md#) or in the [ECS console](../../../../../reseller.en-US/User Guide/Instances/Start or stop an instance.md#), the instance continues to be billed.

-   **Market price** 

    During creation of a preemptible instance, it runs when your bid is higher than the current market price and the resource stock is sufficient.

    In the first hour of its running, the instance is billed according to the initial market price. After that, it is billed according to the real-time market price.


The market price of a preemptible instance fluctuates according to the changes in the demand and supply of a given instance type. Therefore, we recommend that you pay attention to and evaluate the market price fluctuations to ensure you can take advantage of lower computing costs and increased throughput when purchasing preemptible instances.

## Quota {#section_l24_3tk_zdb .section}

For more information about the preemptible instance quota, see [Limits](../../../../../reseller.en-US/User Guide/Limits.md#).

## Create a preemptible instance {#section_pdc_jt5_ydb .section}

You can purchase a preemptible instance by using the [RunInstances](../../../../../reseller.en-US/API Reference/Instances/RunInstances.md#) interface.

After a preemptible instance is created, it can be used in the same way as a Pay-As-You-Go instance. You can also use it with other cloud products, such as cloud disks or EIP addresses.

## Stop a preemptible instance {#section_qdc_jt5_ydb .section}

You can stop a preemptible instance in the [ECS console](../../../../../reseller.en-US/User Guide/Instances/Start or stop an instance.md#) or by using the [StopInstance](../../../../../reseller.en-US/API Reference/Instances/StopInstance.md#) interface. VPC preemptible instances support the [No fees for stopped VPC instances](../../../../../reseller.en-US/Pricing/No fees for stopped VPC instances.md#) feature.

The network type and the bidding mode of a preemptible instance determine whether it can start after it is stopped, as shown in the following table.

|Network type + bidding mode|Stop instance|Restart instance|
|:--------------------------|:------------|:---------------|
|VPC + SpotWithPriceLimit|Select two options: Stop and Keep Stopped Instances and Continue Billing|During the guaranteed duration, the instance can be restarted successfully. After the guaranteed duration:-   If your bid is not lower than the market price and the resource stock is sufficient, the instance can be restarted successfully.
-   If your bid is lower than the market price or the resource stock is insufficient, the instance cannot be restarted.

|
|Classic network + SpotWithPriceLimit|N/A|
|VPC + SpotAsPriceGo|Select two options: Stop and Keep Stopped Instances and Continue Billing|During the guaranteed duration, the instance can be restarted successfully. After the guaranteed duration:-   If the resource stock is sufficient, the instance can be restarted successfully.
-   If the resource stock is insufficient, the instance cannot be restarted.

|
|Classic network + SpotAsPriceGo|N/A|
|VPC + SpotWithPriceLimit|Select one option only: Stop|During the guaranteed duration, the instance can be restarted successfully only if the resource stock is sufficient. After the guaranteed duration:-   If your bid is not lower than the market price and the resource stock is sufficient, the instance can be restarted successfully.
-   If your bid is lower than the market price or the resource stock is insufficient, the instance cannot be restarted successfully.

|
|VPC + SpotAsPriceGo|Select one option only: Stop|During the guaranteed duration, the instance can be restarted successfully only if the resource stock is sufficient. After the guaranteed duration:-   If the resource stock is sufficient, the instance can be restarted successfully.
-   If the resource stock is insufficient, the instance cannot be restarted.

|

## Release a preemptible instance {#section_xdc_jt5_ydb .section}

When the guaranteed period ends, the instance is automatically released according to market price changes or if there is insufficient stock. Additionally, you can independently [release the instance](../../../../../reseller.en-US/User Guide/Instances/Release an instance.md#).

When a preemptible instance is released because of market price changes or insufficient stock, the instance enters the **Pending Release** status. Then, the instance is released in about five minutes. You can use [instance metadata](../../../../../reseller.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#) or the `OperationLocks` information returned by calling the [DescribeInstances](../../../../../reseller.en-US/API Reference/Instances/DescribeInstances.md#)interface to check if an instance is in the **Pending Release** status.

**Note:** Although you can check if a preemptible instance is in the **Pending Release** status by using the API and save a small amount of data while the instance is in this status, we recommend that you design your applications in such a way that your services can continue even if the preemptible instance is immediately released. You can release a preemptible instance manually so as to test whether your applications run normally if an instance is automatically released.

Generally, preemptible instances are released in the order of bidding price, from low to high. If multiple preemptible instances have the same bidding price, they are randomly released.

## Best practices {#section_zdc_jt5_ydb .section}

When using a preemptible instance, consider the following:

-   Set a proper bidding price. That is, we recommend that you evaluate and submit a competitive price and take into account the estimated market price fluctuations. By doing so, your request can be accepted and your created preemptible instances will not be released easily due to price fluctuations. Additionally, we recommend that you take into account your pricing expectations based on your own business assessment.

-   The image must have all the software configurations that your applications need, making sure that you can run your business immediately after the instance is created. Additionally, you can use [User data](../../../../../reseller.en-US/User Guide/Instances/User-defined data and metadata/User data.md#) to run commands upon startup.

-   Store your business data on storage products that are independent from preemptible instances, such as cloud disks that are not set to release together with instances, OSS, or RDS.

-   Split your tasks by using grids, Hadoop, queue-based architecture, or check points, thus making it easy to store computing results frequently.

-   Use release notifications to monitor the status of a preemptible instance. You can use [instance metadata](../../../../../reseller.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#) to check the instance status every minute. The metadata of a preemptible instance is updated five minutes before it is released automatically.

-   Test your applications to make sure that they can handle the accidental release of instances. You can test your applications as follows: run the applications on a Pay-As-You-Go instance, release the instance, and then check how the applications handle the release.


For more information, see [FAQ about preemptible instances](https://partners-intl.aliyun.com/help/faq-detail/48269.htm).

For more information about using APIs to create preemptible instances, see [Use APIs to manage preemptible instances](https://partners-intl.aliyun.com/help/doc-detail/61259.htm).

