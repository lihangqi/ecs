# Create a preemptible instance {#concept_mv5_xxz_xdb .concept}

This topic describes how to create a preemptible instance and view its bills in the ECS console.

## Prerequisites {#section_qcd_rum_izp .section}

The following requirements must be met before you create a preemptible instance:

-   An appropriate bid has been made for the preemptible instance you want to purchase. For more information about an appropriate bid, see [Preemptible instances](reseller.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#).
-   The image used for creating a preemptible instance must contain the configuration of all the required software. You can also use user data to run commands at instance startup. For more information, see [User data](reseller.en-US/Instances/Manage instances/User-defined data/User data.md#).
-   Applications that can withstand accidental instance release are set up.

    **Note:** You can run your applications on a Pay-As-You-Go instance and release the instance to verify whether your applications can properly handle automatic instance release.


## Precautions {#section_car_0gp_woe .section}

We recommend that you perform the following actions before you create a preemptible instance:

-   To prevent any data loss caused by instance release, save important data in storage media such as separately created cloud disks, OSS, or RDS.
-   Break down your jobs into small tasks by using grids, Hadoop, queue-based architecture, or checkpoints to save calculation results on demand.
-   You can monitor the status of a preemptible instance by checking the instance release notifications issued by Alibaba Cloud ECS.

    **Note:** Alibaba Cloud ECS updates the instance metadata five minutes before releasing a preemptible instance. You can obtain the status of a preemptible instance every minute by checking the [instance metadata](reseller.en-US/Instances/Manage instances/User-defined data and metadata/Metadata.md#).


## Create a preemptible instance {#section_rt1_5yy_pfb .section}

1.  On the Instances page, click **Create Instance**.
2.  Set **Billing Method** to **Preemptible Instance**.
3.  In the **Maximum Price for Instance Type Per Instance** area, type your bid in the text box.

    **Note:** 

    -   You can create a preemptible instance only if your bid is higher than the market price and the resource stock is sufficient.
    -   You can bid for a preemptible instance only once.
    -   The following two bidding modes are supported:
        -   **Use Automatic Bid**: The real-time market price is used as the bidding price.
        -   **Set Custom Maximum Price \(Per Instance/Hour\)**: The highest price you are willing to pay for a specified instance type.
    In the displayed price range, the highest price is the price for the Pay-As-You-Go instance of the same configuration. Your bid must be based on the displayed price range, your service needs, and the estimated future price fluctuation. If your bid takes into account the estimated future price fluctuation, you can hold the instance even after the one-hour guaranteed duration. Otherwise, your instance will be automatically released at any time after that duration.

4.  Select or enter the quantity of instances you want to purchase.
5.  Complete other settings.

    For the description of other parameters, see [Create an instance by using the wizard](reseller.en-US/Instances/Create an instance/Create an instance by using the wizard.md#).

6.  After the order is confirmed, click **Create Instance**.

After a preemptible instance is created, you can view its information in the instance list. A preemptible instance is marked as a **Pay-As-You-Go-Preemptible Instance**. On the **Instance Details** page, you can view the bidding policy configured during instance creation in the **Payment Information** area.

You can also create a preemptible instance by calling the [RunInstances](../reseller.en-US/API Reference/Instances/RunInstances.md#) API action through Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK.

**Note:** If you select the **Use Automatic Bid** bidding mode, set the SpotStrategy parameter in this API to SpotAsPriceGo. If you select the **Set Custom Maximum Price \(Per Instance/Hour\)** bidding mode, set this parameter to SpotWithPriceLimit.

## View bills of a preemptible instance {#section_pkj_3qt_qgb .section}

Unlike Pay-As-You-Go instances, the price of a preemptible instance is the concluded price.

To view the bills of a preemptible instance on the **Instance Details** page, following these steps:

1.  On the Instances page, click the ID of the target preemptible instance or click **Manage** in the **Actions** column.
2.  On the Instance Details page, choose **More** \> **View Fees** in the **Payment Information** area.
3.  On the Bills page, click **Detail** in the **Action** column.

To view the bills of a preemptible instance on the **Billing Management** page, following these steps:

1.  Choose **Billing Management** \> **Billing Management**.
2.  On the Billing Management page, choose **Spending Summary** \> **Instance Spending Details**.
3.  On the Instance Spending Details page, find the target preemptible instance and click **Detail** in the **Action** column.

    **Note:** You can filter instances by billing cycle, product name, and status.


