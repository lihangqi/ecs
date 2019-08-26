# Change public IP address {#concept_emj_v2n_xdb .concept}

If your instance is assigned a public IP address, you can change the address within six hours after the instance is created regardless of whether the instance is in a classic network or in a VPC network.

## Limits {#section_pv5_w2n_xdb .section}

-   The instance must be assigned a public IP address. To verify the public IP address, view the public IP address in the **IP Address** column from the **Instance List** in the ECS console, as displayed in the following figure. 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9656/15432125695458_en-US.png)

    **Note:** 

    -   If the public network IP address is not assigned at the time of creation of the instance, after the instance is created successfully, you can assign the public IP address by upgrading or downgrading the network bandwidth configuration. For more information, see [overview of configuration changes](reseller.en-US/User Guide/Instances/Change configurations/Overview of configuration changes.md#).
    -   If the public network IP address is not assigned during the creation of a Pay-As-You-Go instance, after the instance is created successfully, public IP address cannot be assigned. You can only [bind an elastic IP \(EIP\) address](https://partners-intl.aliyun.com/help/doc-detail/27714.htm).
-   The instance must be in the **Stopped** status.

-   The instance has existed for less than six hours.

    **Note:** After six hours, for a VPC instance in a VPC network, you can [convert public IP address to EIP address](reseller.en-US/User Guide/Instances/Change IP addresses/Convert public IP address to EIP address.md#). Instances in the classic network cannot have their public IP address converted.

-   You can change the public IP address of an instance a maximum of three times.


## Prerequisite {#section_tv5_w2n_xdb .section}

The instance must be in the **Stopped** status.

## Procedure {#section_uv5_w2n_xdb .section}

To change the public IP address, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the target instance to change the public IP address and then, in the **Actions** column, select **More** \> **Network and Security Group** \> **Change Public IP**.

    **Note:** If the instance has existed for more than six hours, the **Change Public IP** option in the **More** drop-down menu is not available.

5.  Click **Start Now**.

    A new public IP address is displayed as shown in the following figure.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9656/15432125695460_en-US.png)

6.  Click **OK**.

## Related operation {#section_yv5_w2n_xdb .section}

You can [change the private IP of an ECS instance](reseller.en-US/User Guide/Instances/Change IP addresses/Change the private IP of an ECS instance.md#).

