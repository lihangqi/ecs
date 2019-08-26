# Convert public IP address to EIP address {#concept_l2l_jgn_xdb .concept}

This topic describes how to convert the assigned public IP address of an ECS instance in a VPC network \(hereinafter referred to as VPC instance\) to an elastic public IP \(EIP\) address. After conversion, you can retain the public IP address and bind it to another ECS instance.

## Limits {#section_asc_kgn_xdb .section}

To convert a public IP address to an EIP address, consider the following limits:

-   You cannot undo this action. Exercise caution when converting an assigned public IP address to an EIP address.

-   Only a VPC instance assigned a public IP address is supported.

-   Only a VPC instance in the **Stopped** or **Running** state is supported.

-   Only a VPC instance that does not have any inactivated specification changes is supported.

-   Only a VPC instance that is not within the last 24 hours of its life cycle is supported.


**Note:** 

-   The conversion has no effect on the Internet access of the VPC instance. It does not cause transient traffic interruption.

-   The billing method of the public traffic remains unchanged.

-   After conversion, the EIP address is charged separately. For more information about billing of EIP addresses, see [EIP billing](https://partners-intl.aliyun.com/help/doc-detail/27767.htm). You can go to the [Usage Records](https://partners-intl.console.aliyun.com/#/ecs) page in the **Billing Management** to download the **Elastic Public IP** usage record.


## Procedure {#section_fsc_kgn_xdb .section}

To convert a public IP address to an elastic public IP \(EIP\) address, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  Find the target **VPC instance** to convert the public IP address, and then choose **More** \> **Network and Security Group** \> **Convert to EIP** from the **Actions** column.
4.  In the Convert to EIP dialog box, read the note and click **OK**.
5.  Refresh the instance list.

After the public IP address is converted to an EIP address, the IP address is followed by **\(Elastic IP Address\)**.

You can click the IP address to go to the [EIP console](https://partners-intl.console.aliyun.com/?spm=a2c6n.7954052.697958.7.50951cbbma1T7R#/vpc) to manage the EIP address.

## What to do next {#section_947_bzj_grm .section}

After the public IP address is converted to an EIP address, you can unbind the EIP address from the instance and bind it to another instance, or release the EIP address. For more information, see [Disassociate an EIP from a cloud instance](../../../../../reseller.en-US/User Guide/Disassociate an EIP from a cloud instance.md#).

## Related API {#section_lsc_kgn_xdb .section}

You can call [ConvertNatPublicIpToEip](../reseller.en-US/API Reference/Networks/ConvertNatPublicIpToEip.md#) to convert a public IP address to an EIP address. Currently, only SDK 4.3.0 or a later version supports this API action.

[Download](https://partners-intl.aliyun.com/help/doc-detail/25699.htm) the latest SDK.

