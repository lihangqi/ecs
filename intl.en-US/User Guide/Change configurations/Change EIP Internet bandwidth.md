# Change EIP Internet bandwidth {#concept_eqg_jbf_5db .concept}

If you are using a VPC-Connected ECS instance, and [an Elastic IP \(EIP\) address is bound to it](https://partners-intl.aliyun.com/help/doc-detail/27714.htm), you can use the **Change Bandwidth** feature to change the Internet bandwidth as needed, regardless of your billing method.

## Restrictions {#section_jzn_d3z_xdb .section}

The **Change Bandwidth** feature only applies to VPC-Connected instances, that are bound with an Elastic IP \(EIP\) address.

## Change bandwidth {#section_hdd_j3z_xdb .section}

To change the Internet bandwidth of an EIP address, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  Find an instance to which an EIP address is bound, and in the **Actions** column, click **Change Configuration**.
5.  In the Change Configurations dialog box, select change bandwidth, and click **Continue**.
6.  On the Confirm Order page, set the new peak bandwidth.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9646/15407912815429_en-US.png)

7.  Click **Activate** and follow the instructions to complete the configuraiton.

## Related operations {#section_wtj_j3z_xdb .section}

For Subscription instances of the classic network type or VPC-Connected ECS instances to which no EIP addresses are bound, you can use the following features to change the Internet bandwidth:

-   Use the [Upgrade Configuration](reseller.en-US/User Guide/Instances/Change configurations/Upgrade configurations of Subscription instances.md#) feature to change the Internet bandwidth immediately.

-   Use the [Renew for Configuration Downgrade](../../../../reseller.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#) feature to change the Internet bandwidth for the next billing cycle.


