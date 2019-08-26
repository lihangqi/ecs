# API Billing {#ApiBilling .reference}

## Billing {#Billing .section}

We recommend that you maintain a sufficient balance in the linked credit card or PayPal account to complete the payment or preauthorization. For more information, see [Pricing overview](../../../../reseller.en-US/Pricing/Pricing overview.md#).

By default, the system uses the latest billing method to automatically charge fees. Make sure that your account balance is sufficient. Otherwise, the system regards your order as an exception, and you have to cancel this order. If your account balance is insufficient, set `AutoPay` to `false`. The system then generates a normal unpaid order for the outstanding payment. You can log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs) to pay for this order.

After you enable the No Termination Fees option for stopped VPC-Connected instances, you can set StoppedMode=KeepCharging to disable the feature, you are billed after the ECS instances are stopped, but their resources and Internet IP addresses are reserved. For more information, see [StopInstance](reseller.en-US/API Reference/Instances/StopInstance.md#).

