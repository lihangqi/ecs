# Downgrade bandwidth configurations of Subscription instances {#concept_vvc_kcb_1gb .concept}

You can downgrade Internet bandwidth configurations of Subscription instances and change the bandwidth billing method from Pay-By-Bandwidth to Pay-By-Traffic. The configurations take effect immediately without the need to restart instances.

You can use the bandwidth configuration downgrade function to perform the following operations:

-   If the current bandwidth billing method is **Pay-By-Bandwidth**, you can:

    -   Lower the fixed bandwidth.
    -   Change the billing method to **Pay-By-Traffic** and set the peak bandwidth.
-   If the current bandwidth billing method is **Pay-By-Traffic**, you can:

    Change the peak bandwidth. Note that you cannot change the billing method to **Pay-By-Bandwidth**.

    **Note:** If your instance uses a VPC, the process of detaching the Internet IP address will be triggered when the bandwidth is lowered to 0 Mbit/s.


## Limits {#section_olg_wp1_1gb .section}

-   Some accounts support this feature \(based on your ECS usage\).
-   You can downgrade bandwidth configurations of only one instance at a time.
-   You can only downgrade the bandwidth configurations of each instance a maximum of three times. Configuration downgrade operations include instance configuration downgrades, bandwidth configuration downgrades, and cloud disk billing method adjustments.
-   The time interval between two downgrade operations must be at least 5 minutes.
-   If the instance uses a VPC and has an elastic IP address, the bandwidth configurations of the instance cannot be downgraded.

## Prerequisites {#section_okd_yp1_1gb .section}

The configurations of an instance can be downgraded only if the instance meets the following conditions:

-   The billing method is Subscription.
-   The instance works properly. That is, the instance cannot be in an abnormal state, such as overdue, outdated, locked, or to be released.
-   The instance cannot have any ongoing configuration downgrade renewal process.

## Procedure {#section_htb_zp1_1gb .section}

1.  Log on to the ECS console.

2.  Find the target instance and click **Change Configuration** in the **Action** column.

3.  In the displayed dialog box, select **Configuration downgrade** and **Bandwidth Configuration**.

4.  Set the bandwidth and read and confirm that you agree with the *ECS Service Terms* .

5.  Click **Downgrade Now**.


