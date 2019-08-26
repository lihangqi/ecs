# Change the public IP address of an ECS instance {#concept_emj_v2n_xdb .concept}

If your ECS instance is assigned a public IP address, you can change the IP address within six hours after the instance is created regardless of whether the instance is in a classic network or in a VPC network.

## Limits {#section_t0q_uk2_52z .section}

-   You can change the public IP address of an instance a maximum of three times.
-   Changes to a public IP address must be made within six hours after the corresponding instance is created.

## Prerequisites {#section_0ig_7sl_6yt .section}

-   The instance must be in the **Stopped** state. For information about how to start or stop an instance, see [Start or stop an instance](../reseller.en-US/Instances/Manage instances/Start or stop an instance.md#).
-   The instance must be assigned a public IP address. You can view the IP address in the **IP Address** column of the **Instance List** in the ECS console.

## Procedure {#section_iqm_61r_0nn .section}

To change the public IP address, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  Find the target instance and then choose **More** \> **Network and Security Group** \> **Change Public IP Address** in the **Actions** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9656/156216062444661_en-US.jpg)

4.  Click **Start Now**.

    A new public IP address is displayed.

5.  Click **OK**.

## FAQ {#section_mgi_mwy_asx .section}

-   Can I change the public IP address of an instance if it was created more than six hours ago?
    -   For instances in a VPC network, the public IP address can be converted into an Elastic IP Address \(EIP\). For information about how to convert the IP address, see [Convert public IP address to EIP address](reseller.en-US/Network/Change IPv4 addresses/Convert public IP address to EIP address.md#).
    -   For instances in a classic network, the public IP address cannot be changed if an instance has been created for more than six hours.
-   Why is the **Change Public IP Address** option under **Network and Security Group** not displayed?
    -   By default, the **Change Public IP Address** option is not displayed for instances that were created more than six hours ago.
    -   If you enable the [no fees for stopped VPC instances](../DNA0011810291/EN-US_TP_9595.dita#concept_js1_1fd_5db) feature for an instance, make sure that this feature is disabled when you stop the instance. Otherwise, the instance will be temporarily released and the **Change Public IP Address** option is not displayed. You can disable this feature by selecting the **Keep Stopped Instances and Continue Billing** check box in the Stop dialog box.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9656/156216062444752_en-US.jpg)

-   Can I change the private IP address of an instance?
    -   This operation is allowed for instances in a VPC network. For information about how to change the private IP address, see [EN-US\_TP\_9658.md\#](reseller.en-US/Network/Change IPv4 addresses/Change the private IP of an ECS instance.md#).
    -   This operation is not allowed for instances in a classic network.
-   How do I obtain the public IP address of a created instance if the IP address is not assigned during instance creation?
    -   For a Subscription instance, you can obtain the public IP address by upgrading or downgrading the network bandwidth configuration. For more information, see [Overview of configuration changes](../reseller.en-US/Instances/Change configurations/Overview of configuration changes.md#).
    -   For a Pay-As-You-Go instance, you cannot obtain the public IP address after the instance is created. You can only [bind an EIP address](https://partners-intl.aliyun.com/help/doc-detail/27714.htm).

