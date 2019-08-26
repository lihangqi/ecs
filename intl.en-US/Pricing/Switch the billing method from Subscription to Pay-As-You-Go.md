# Switch the billing method from Subscription to Pay-As-You-Go {#concept_hzg_ggr_l2b .concept}

This topic describes how to switch the billing method from Subscription to Pay-As-You-Go. After you create a Subscription instance, you can convert its billing method to Pay-As-You-Go if you want to pay only for the actual usage of your resources.

Before converting the billing method, note the following:

-   The billing method conversion applies to the system disk and the data disks of the instance, regardless of whether the data disks are created along with the instance.
-   The billing method of Internet bandwidth is unchanged.

After the conversion, make sure your account has sufficient funds to pay the bill. Otherwise, overdue payment will affect the running of your services. If you no longer require the instance, you can set it to auto release or release it manually. For more information, see [Release an instance](../reseller.en-US/Instances/Manage instances/Release an instance.md#).

## Conversion notes {#section_ytk_23r_l2b .section}

-   Whether you can convert the billing method is determined by your ECS instance resource usage.
-   Each account is limited by a maximum monthly **refund amount**. For more information, see the conversion page. You cannot claim additional refunds once the monthly limit is reached. The remaining amount will be cleared automatically on the 1st day of the next month.

    To calculate the refund amount resulting from a billing method conversion, the calculation uses the number of vCPUs and the remaining hours in the current billing cycle. For example, 1 refund unit = `1 vCPU × 1 hour`.

    In this example, assume you have purchased a Subscription instance with four vCPUs for six months. Four months later, you convert the billing method to Pay-As-You-Go. In this case, the refund amount for this instance is `4 (vCPUs) × 60 (remaining days) × 24 (hours/day) = 5760 (refund amount)`.

-   If the instance involves renewal or upgrade orders that have not taken effect, a full refund will be made. For orders that have already taken effect, only a partial refund will be made.
-   After the billing method is converted, the duration of usage given for reasons such as ICP filing, failure, or IDC migration is automatically invalidated.

## Prerequisites {#section_dpm_k3r_l2b .section}

-   The relevant ECS instance and cloud disks must use the Subscription billing method.
-   The relevant ECS instance is in the **Running** or **Stopped** state.

## Procedure {#section_t4h_l3r_l2b .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, choose **Instances & Images** \> **Instances**.
3.  Select the relevant instance. In the **Actions** column, choose **More** \> **Configuration Change** \> **Switch to Pay-As-You-Go**.
4.  On the conversion page, read the notes and confirm you agree to the *ECS Service Terms* .
5.  Click **Confirm Conversion**.

    After the billing method is converted successfully, you can see that the **Billing Method** of the instance is changed to **Pay-As-You-Go** in the ECS console. Alternatively, click the instance ID to enter the Instance Details page. In the left-side navigation pane, click **Disks**. You can see that the **Billing Method** of the system disk and data disks \(if any\) of the instance have changed to **Pay-As-You-Go**.


## FAQ {#section_fzl_5jr_l2b .section}

 **What can I do if the conversion fails?** 

Conversion failure may be due to:

-   The current instance status does not support conversion.
-   Conversion is not allowed because the instance has expired.
-   Conversion is not allowed because instance information has changed.

If any of the preceding error messages appears, adjust the instance accordingly. If the problem persists, open a ticket.

