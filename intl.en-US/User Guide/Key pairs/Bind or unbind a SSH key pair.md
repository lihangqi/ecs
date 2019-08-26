# Bind or unbind an SSH key pair {#concept_zzt_nl1_ydb .concept}

## Limits {#section_f2n_pl1_ydb .section}

-   An ECS instance can bind only one SSH key pair.
-   Except for the non-I/O-optimized instances of Generation I, all the Linux instances listed in the [instance type families](../../../../reseller.en-US/Product Introduction/Instance type families.md#) support the authentication method of SSH key pair.
-   When your ECS instance is in the **Running** status, [restart it](reseller.en-US/User Guide/Instances/Restart an instance.md#) after you bind an SSH key pair to the instance.
-   If the ECS instance has already bound an SSH key pair, after the new key pair is bound, the new key automatically replaces the original key.
-   If you use password-based authentication for Linux logon, the password authentication feature is automatically disabled after the key pair is bound.
-   After an SSH key pair is unbound, you must [reset the instance password](reseller.en-US/User Guide/Instances/Reset an instance password.md#) for successful connection.

## Bind an SSH key pair {#section_d4l_ql1_ydb .section}

To bind an SSH key pair to an ECS instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Networks and Security** \> **SSH Key Pair**.
3.  Select a region.
4.  Select a key pair, and then click **Bind** in the **Actions** column.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9730/153950469211242_en-US.png)

5.  In the Bind dialog box, select one or more instances from the **Select Instance** box, and then click the icon **\>** to move them to the **Selected** column.

    **Note:** In the **Select Instance** box, the instances with gray names are either Windows instances or non-I/O-optimized instances of Generation I, for which SSH key pairs are not supported.

6.  Click **OK**.

## Unbind an SSH key pair {#section_lqq_yp1_ydb .section}

To unbind an SSH key pair from an ECS instance, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  Select a region.
3.  In the left-side navigation pane, click **Networks and Security** \> **SSH Key Pair**.
4.  Select an SSH key pair, and then in the **Actions** column, click **Unbind**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9730/153950469211245_en-US.png)

5.  In the Unbind dialog, select one or more instances from the **Select Instance** box, and then click the icon **\>** to move them to the **Selected** column.
6.  Click **OK**.

