# Convert billing methods of cloud disks {#concept_zpt_5g3_ydb .concept}

The billing method of a cloud disk depends on how it is created:

-   For cloud disks created with Subscription instances, prepayment of the service fee is required for it to be available for use. For more information, see [Subscription](../../../../intl.en-US/Pricing/Subscription.md#).
-   For cloud disks created jointly with Pay-As-You-Go instances, or created separately the billing is on a Pay-As-You-Go basis. For more information, see [Pay-As-You-Go](../../../../intl.en-US/Pricing/Pay-As-You-Go.md#).

You can change the billing method of a cloud disk, as shown in the following table.

|Conversion of billing methods|Conversion method|Suitable for|Effective date|
|:----------------------------|:----------------|:-----------|:-------------|
|Subscription —\> Pay-As-You-Go|[Renew for configuration downgrade](../../../../intl.en-US/Pricing/Renew instances/Renew for configuration downgrade.md#)|Subscription cloud disks attached to Subscription instances. The billing method of the system disk cannot be changed.|Effective from the next billing cycle|
|Pay-As-You-Go —\> Subscription|[Upgrade configurations](intl.en-US/User Guide/Instances/Change configurations/Upgrade configurations of Subscription instances.md#)|Pay-As-You-Go data disks attached to Subscription instances. The billing method of the system disk cannot be changed.|Effective immediately|
|[Switch from Pay-As-You-Go to subscription](../../../../intl.en-US/Pricing/Limits.md#)|The system disks and data disks attached to the Pay-As-You-Go instances.|

