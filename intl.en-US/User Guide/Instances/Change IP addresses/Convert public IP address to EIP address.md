# Convert public IP address to EIP address {#concept_l2l_jgn_xdb .concept}

This article describes how to convert the assigned public IP address of an ECS instance in a VPC network, \(referenced as VPC instance for short in this article\), to an elastic public IP \(EIP\) address. After conversion, you can retain the public IP address and bind it to another ECS instance.

## Limits {#section_asc_kgn_xdb .section}

To convert a public IP address to an EIP address, consider the following limits:

-   You cannot undo this action. Exercise caution when converting an assigned public IP address to an EIP address.

-   Only a VPC instance assigned a public IP address is supported.

-   Only a VPC instance in the **Stopped** or **Running** status is supported.

-   Only a VPC instance that does not have any inactivated specification changes is supported.

-   Only a VPC instance that is not within the last 24 hours of its life cycle is supported.


**Note:** 

-   The conversion has no effect on the Internet access of the VPC instance. It does not cause transient traffic interruption.

-   The billing method of the public traffic remains unchanged.

-   After conversion, the EIP address is charged separately. For more information about billing of EIP addresses, see [EIP billing](https://partners-intl.aliyun.com/help/doc-detail/27767.htm). You can go to the [Usage Records](https://partners-intl.console.aliyun.com/#/ecs) page in the **Billing Management** to download the **Elastic Public IP** usage record.


## Procedure {#section_fsc_kgn_xdb .section}

To convert a public IP address to an elastic public IP \(EIP\) address, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the region.
4.  Find the target **VPC instance** to convert the public IP address, in the **Actions** column, select **More** \> **Convert to EIP**.
5.  In the Convert to EIP dialog box, read the note and click **OK**.
6.  Refresh the instance list.

After the public IP address is converted to an EIP address, the IP address is followed by **\(Elastic IP Address\)**. 

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9657/15432129985473_en-US.png)

Click the IP address to go to the EIP console to manage the EIP address. 

## Follow-up operations {#section_jsc_kgn_xdb .section}

After the public IP address is converted to an EIP address, you can unbind the EIP address from the instance and bind it to another instance. You can also release the EIP address. For more information, see [unbind and release an EIP](../../../../reseller.en-US/User Guide/Unbind and release an EIP.md#).

## Related API {#section_lsc_kgn_xdb .section}

You can use the [ConvertNatPublicIpToEip](../../../../reseller.en-US/API Reference/Networks/ConvertNatPublicIpToEip.md#) interface to convert a public IP address to an EIP address. Currently, only SDK 4.3.0 or a later version supports this interface.

[Download](https://partners-intl.aliyun.com/help/doc-detail/25699.htm) the latest SDK.

