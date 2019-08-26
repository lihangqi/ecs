# Manage Reserved Instances {#concept_kc4_cnr_dgb .concept}

This topic describes how to split, merge, and modify the scope of your Reserved Instances \(RIs\). Such actions allow you to benefit from billing discounts of more Pay-As-You-Go instance types.

## Prerequisites {#section_b5n_pnr_dgb .section}

**Note:** To make this topic easier to understand, RIs to be split, merged, or modified are hereinafter referred to as original RIs, while split, merged, or modified RIs are hereinafter referred to as target RIs.

Before you split, merge, or modify RIs, make sure that the following conditions are met:

-   You have successfully purchased original RIs and they are within a valid term.
-   There is no ongoing splitting, merging, or modification request.
-   The RI to be modified only requires its size to be adjusted. The instance type family of an RI cannot be modified.

After you submit a splitting, merging, or modification request:

-   The original RI changes to changing status, which will be automatically refreshed after the request is processed.
-   A request in progress cannot be changed or canceled. If you want to roll back your changes, you must submit another request.

After an RI is split, merged, or modified:

-   The target RI becomes valid on the hour. If it matches one or more new Pay-As-You-Go instances, the billing discount is applied within the same hour.
-   The original RI becomes invalid on the hour, and its price is updated to USD 0.
-   If the target RI is a zonal RI, the type of resource reservation is also updated automatically.

For example, you successfully split an ecs.g5.2xlarge zonal RI \(RI1\) into two ecs.g5.xlarge zonal RIs \(RI2 and RI3\) at 2019-02-26 13:45:00. In this case, RI1 becomes invalid at 2019-02-26 13:00:00, while RI2 and RI3 take effect also at 2019-02-26 13:00:00. Starting 2019-02-26 13:00:00, the reserved instance type eligible for billing discount is also changed from ecs.g5.2xlarge to ecs.g5.xlarge. If RI2 and RI3 match instances immediately after they take effect, the hourly bill discount for ecs.g5.xlarge instances is also applied starting 2019-02-26 13:00:00.

If the original RI fails to be split, merged, or modified, it will remain valid.

## Split an RI {#section_zcd_vnr_dgb .section}

You can split an RI into multiple RIs of less computing power. The smaller RIs can then match applicable Pay-As-You-Go instances to better distribute your service traffic.

1.  In the left-side navigation pane, choose **Instances & Images** \> **Reserved Instances**.
2.  On the Reserved Instances page, click **Split** in the **Actions** column of the original RI.
3.  On the Split Reserved Instance page, set the name, instance type, and instance quantity of the target RIs.

    **Note:** The total computing power of the target RIs must be equal to that of the original RI.

4.  Click **OK**.

## Merge RIs {#section_xsk_fpr_dgb .section}

If traffic to your instances increases, you can merge multiple RIs into one RI that has greater computing power to match larger Pay-As-You-Go instances.

**Note:** Before merging RIs, you must verify that the following conditions are met:

-   The expiration date of the original RIs must be the same.
-   The original RIs have been purchased using the same currency.
-   If the original RIs are regional RIs, they must be in the same region. If the original RIs are zonal RIs, they must be in the same zone.

1.  In the left-side navigation pane, choose **Instances & Images** \> **Reserved Instances**.
2.  On the Reserved Instances page, click **Merge** in the **Actions** column of the original RI.
3.  On the Merge Reserved Instances page, select the original RIs, and then set the name, instance type, and instance quantity of the target RI.

    **Note:** The computing power of the target RI must be equal to that of all selected original RIs, and the target RI must be of an existing instance type. For example, two ecs.g5.2xlarge RIs can be merged into one ecs.g5.4xlarge RI, but one ecs.g5.xlarge RI and two ecs.g5.2xlarge RIs cannot be merged into one ecs.g5.5xlarge RI.

4.  Click **OK**.

## Modify the scope of an RI {#section_rrd_ppr_dgb .section}

If your service requirements change, you can modify the scope of your RIs. Specifically, you can:

-   Modify a regional RI to a zonal RI.
-   Modify a zonal RI to a regional RI.
-   Modify the zone of an RI in the same region.

You cannot modify the scope of an RI across regions. For example, if you have a zonal RI in zone B of China \(Hangzhou\), you can modify it as a zonal RI in another zone of China \(Hangzhou\), or as a regional RI in China \(Hangzhou\). However, you cannot modify it as a regional or zonal RI in another region.

1.  In the left-side navigation pane, choose **Instances & Images** \> **Reserved Instances**.
2.  On the Reserved Instances page, click **Modify** in the **Actions** column of the original RI.
3.  On the Modify Reserved Instance Page, modify the parameters as needed.
4.  Click **OK**.

