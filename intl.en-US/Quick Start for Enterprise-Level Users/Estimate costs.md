# Estimate costs {#concept_hwc_yqv_wdb .concept}

As an enterprise-level user, once you select the instance type and have completed the network planning, you can estimate the costs based on the following factors: billing methods, regions, images, networks, and quantity.

## Billing methods {#billing .section}

Now, the following billing methods are available to an enterprise-level user, including [Subscription, Pay-As-You-Go](../../../../intl.en-US/Pricing/Billing method comparison.md#), and [preemptible instances](../../../../intl.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#).

-   Subscription: Subscription is a type of prepayment whereby instances can be used only after you make the payment. Instances are charged on a monthly basis, and the unit is **USD/month**. This billing method is applicable to fixed 24/7 services, such as the Web service.
-   Pay-As-You-Go: Pay-As-You-Go is a type of post payment whereby payment can be made after you use the resources. Instances are billed by second and settled by hour. The unit is **USD/hour** . This billing method is applicable to scenarios with traffic volume spikes, such as temporary scaling, interim testing, and scientific computing.

-   Preemptible instance: To reduce the ECS computing cost, you can select a **preemptible instance**. As an instance on demand, you must set the maximum hourly rate you want to pay for your expected instance type. When your bid is higher than the current market price, your instance runs. The final price you pay for the instance type is based on the current market price. For more information, see [preemptible instances](../../../../intl.en-US/Instances/Instance purchasing options/Preemptible instances/Preemptible instances.md#).


Advantages of each billing method vary according to the instance type. For more information, see [ECS product pricing](https://www.alibabacloud.com/product/ecs).

## Regions {#regions .section}

When selecting a region, you must consider the following factors:

-   Region of the instance and the geographical location of your target users
-   Relationship between ECS and other Alibaba Cloud products
-   Resource price
-   Special requirements of some regions. For example, to use an ECS instance as a Web server in mainland China, your business license must be filed for record.

**Note:** The price for the same instance type may vary according to the region. For more information about the specific prices, see [ECS product pricing](https://www.alibabacloud.com/product/ecs).

## Images {#images .section}

The price varies according to the image type:

-   Public images: The price varies with the region.
-   Shared images: The price of the custom image shared with you by other accounts is based on the source image.
-   Custom images: The price is based on the source image.

## Networks {#networks .section}

After completing network planning of the general solution, you must select a specified VPC and switch.

**Note:** Before purchasing an instance, you must create a VPC and a switch in advance.

When selecting a specific network, the selected VPC and switch are free of charge.

-   If you want to **allocate a public IP address**, you can set the **peak bandwidth** . Different fees are charged based on the selected bandwidth. If the selected public bandwidth is 0 Mbit/s, no public IP address is allocated by default.

    **Note:** The allocated public IP addresses cannot be unbound from their ECS instances.

-   If you choose not to allocate public IP addresses and you need a static public IP address solution with greater flexibility, we recommend that you do not allocate a public IP address. Then, configure and bind an EIP address. For more information about the fees if you choose to configure an EIP, see EIP billing.


## Quantity {#quantity .section}

If you purchase more ECS instances, the cost rises.

