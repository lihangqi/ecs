# Preemptible instance {#concept_t3p_gv2_5db .concept}

Preemptible instances are a type of on-demand instances. They are designed to reduce your ECS costs in some cases. When you create a preemptible instance, you can set a maximum rate per hour for bidding a specified instance type. When your bid is higher than or equal to the current market price, your instance runs. You can hold a preemptible instance without interruption for at least one hour.  When the market price exceeds your bid or the resource stock is insufficient, the instance is automatically released. The following figure shows the life cycle of a preemptible instance.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9552/5106_en-US.png)

## Scenarios {#section_fdc_jt5_ydb .section}

Preemptible instances are ideal for stateless applications, such as scalable Web services and applications for rendering figures, big data analysis, and massively parallel computing. Applications requiring higher level of distribution, scalability, and fault tolerance capability benefit from preemptible instances with respect to costs and throughput.

You can deploy the following businesses on preemptible instances:

-   Real-time analysis
-   Big data
-   Geological survey
-   Image coding and media coding
-   Scientific computing
-   Scalable Web sites and Web crawlers
-   Image and media coding
-   Testing

Preemptible instances are not suitable for stateful applications, such as databases, because it is difficult to store application states if the instance is released because of a failed bid or some other reasons.

## Bidding modes {#section_hdc_jt5_ydb .section}

You can bid for a preemptible instance only one time in either of the following bidding modes:

-   [SpotWithPriceLimit](#SpotWithPriceLimit)
-   [SpotAsPriceGo](#SpotAsPriceGo)

**SpotWithPriceLimit**

In this mode, you must set the highest price you want to pay for a specified instance type. When creating a preemptible instance by using [RunInstances](../../../../intl.en-US/API Reference/Instances/RunInstances.md#), you can bid in this mode.

Currently, the maximum bid of a preemptible instance is the price of a Pay-As-You-Go instance of the same configuration. When creating a preemptible instance, you can set a price according to the market price history, business features, and the estimated future price fluctuation. When the market price is lower than or equal to your bid, and the resource stock is sufficient, the instance continues to run. If your estimated quote is accurate, you can hold the instance even after one hour [Guaranteed duration](#valid). Otherwise, your instance gets automatically released at any time.

**SpotAsPriceGo**

When creating a preemptible instance by using [RunInstances](../../../../intl.en-US/API Reference/Instances/RunInstances.md#), you can create a preemptible instance with the SpotAsPriceGo bidding mode by setting `SpotStrategy` to `SpotAsPriceGo`, which means you always set the real-time market price as the bidding price until the instance is released because of stock shortage.

## Guaranteed duration {#valid .section}

Once a preemptible instance is created, it has a guaranteed duration of one hour, namely, the first hour after it is created. During this period, we do not release your instance because of stock shortage, and you can run services on the instance as usual. Beyond the guaranteed duration, we check the market price and stock every five minutes. If the market price at any given point of time is higher than your bid or the instance type stock is insufficient, we will release your preemptible instance.

## Price and billing {#section_mdc_jt5_ydb .section}

Preemptible instance price and billing considerations:

-   **Price** 

    The preemptible instance price applies to the instance type only, including vCPU and memory, but not to system disks, data disks, or network bandwidth. The prices for system disks, data disks, or network bandwidth are the same as for [Pay-As-You-Go](../../../../intl.en-US/Pricing/Pay-As-You-Go.md#) instances.

-   **Billing cycle** 

    Preemptible instances are billed on an hourly basis during their life cycles. You are billed for the entire hour even if your usage is less than an hour.

-   **Billing duration** 

    Instances are billed according to the actual period of use. The actual period of use is the duration from instance creation to instance release. After an instance is released, it is no longer billed. If you stop the instance by using [StopInstance](../../../../intl.en-US/API Reference/Instances/StopInstance.md#) or in the [ECS console](../../../../intl.en-US/User Guide/Instances/Start or stop an instance.md#), the instance continues to be billed.

-   **Market price** 

    During creation of a preemptible instance, it runs when your bid is higher than the current market price and the relevant demand and supply conditions are satisfied. The final price you pay for your instance type is based on the current market price.


The actual market price of a preemptible instance fluctuates according to the changes in the demand and supply of a given instance type. Therefore, you can take full advantage of the price fluctuations of preemptible instances. If you purchase preemptible instance types at the right time, the computing costs are reduced but your business throughput for this period is increased.

## Quota {#section_l24_3tk_zdb .section}

For more information about the preemptible instance quota, see [Limits](../../../../intl.en-US/User Guide/Limits.md#).

## Create a preemptible instance {#section_pdc_jt5_ydb .section}

You can purchase a preemptible instance by using the [RunInstances](../../../../intl.en-US/API Reference/Instances/RunInstances.md#) interface.

After a preemptible instance is created, it can be used exactly as a Pay-As-You-Go instance. You can also use it with other cloud products, such as cloud disks or EIP addresses.

## Stop a preemptible instance {#section_qdc_jt5_ydb .section}

You can stop a preemptible instance in the [ECS console](../../../../intl.en-US/User Guide/Instances/Start or stop an instance.md#) or by using the [StopInstance](../../../../intl.en-US/API Reference/Instances/StopInstance.md#) interface. The VPC-Connected preemptible instances support the feature.

The network type and the bidding mode of a preemptible instance determine whether it can start after it is stopped, as displayed in the following table.

|Network type + Bidding mode|Stop instance |Start instance|
|:--------------------------|:-------------|:-------------|
|VPC + SpotWithPriceLimit|Keep Instance, Fees Apply|During the guaranteed duration, the instance can be started successfully. After the guaranteed duration:-   If your bid is not lower than the market price and the resource stock is sufficient, the instance can be started successfully.
-   If your bid is lower than the market price or the resource stock is insufficient, the instance cannot be started successfully.

|
|Classic + SpotWithPriceLimit|N/A|
|VPC + SpotAsPriceGo|Keep Instance, Fees Apply|During the guaranteed duration, the instance can be started successfully. After the guaranteed duration:-   If the resource stock is sufficient, the instance can be started successfully.
-   If the resource stock is insufficient, the instance cannot be started.

|
|Classic + SpotAsPriceGo|N/A|
|VPC + SpotWithPriceLimit|Stop Instance, No Fees|During the guaranteed duration, the instance can be started successfully only if the resource stock is sufficient.  After the guaranteed duration:-   If your bid is not lower than the market price and the resource stock is sufficient, the instance can be started successfully.
-   If your bid is lower than the market price or the resource stock is insufficient, the instance cannot be started successfully.

|
|VPC + SpotAsPriceGo|Stop Instance, No Fees|During the guaranteed duration, the instance can be started successfully only if the resource stock is sufficient. After the guaranteed duration:-   If the resource stock is sufficient, the instance can be started successfully.
-   If the resource stock is insufficient, the instance cannot be started.

|

## Release a preemptible instance {#section_xdc_jt5_ydb .section}

When the guaranteed period ends, we automatically release your preemptible instance because of changes in the market price or short resource stock. Additionally, you can independently [release the instance](../../../../intl.en-US/User Guide/Instances/Release an instance.md#).

When a preemptible instance is released because of market price or changes in the demand and supply of resources, the instance enters the **Pending Release** status. Then, the instance is released in about five minutes. You can use [Metadata](../../../../intl.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#) or the `OperationLocks` information returned by calling the [DescribeInstances](../../../../intl.en-US/API Reference/Instances/DescribeInstances.md#) interface to check if an instance is in the **Pending** Release status.

**Note:** Although you can check if a preemptible instance is in the **Pending Release** status by using the API and save a small amount of data while the instance is in this status, we recommend that you design your applications so work can be properly resumed if the preemptible instance is immediately released. When you release the instance manually, you can test whether or not your application functions normally if a preemptible instance is immediately recovered.

Generally, we release preemptible instance in the order of bidding price, from low to high. If multiple preemptible instances have the same bidding price, they are randomly released.

## Best practices {#section_zdc_jt5_ydb .section}

When using a preemptible instance, consider the following:

-   Set a proper bidding price. In other words, you must quote a competitive price to meet your business budget and hedge against the future market price fluctuations. By using this price, your preemptible instance can be created. In addition, the price must meet your expectations based on your own business assessment.

-   The image must have all the software configurations that your applications need, assuring that you can run your business immediately after the instance is created. Additionally, you can use [User data](../../../../intl.en-US/User Guide/Instances/User-defined data and metadata/User data.md#) to run commands at startup.

-   Store your business data on storage products that are independent from preemptible instances, such as cloud disks that are not set to release together with instances, OSS, or RDS.

-   Split your tasks by using grids, Hadoop, queuing-based architecture, or check points, to facilitate store computing results frequently.

-   Use the release notification to monitor the status of a preemptible instance. You can use [Metadata](../../../../intl.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#) to check the instance status every minute. The metadata of an instance is updated five minutes before it is released automatically.

-   Test your applications in advance, to make sure that they can handle events such as accidental release of an instance. To test the applications: Run the applications on a Pay-As-You-Go instance, release the instance, and then check how the applications can handle the release.


For more information, see [FAQ about preemptible instances](https://www.alibabacloud.com/help/faq-detail/48269.htm).

For more information about using APIs to create preemptible instances, see [Using APIs to manage preemptible instances](https://www.alibabacloud.com/help/zh/doc-detail/61259.htm).

