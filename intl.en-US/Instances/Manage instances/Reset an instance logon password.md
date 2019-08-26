# Reset an instance logon password {#concept_qct_gfl_xdb .concept}

This topic describes how to reset the logon password of one or more instances.

## Limits {#section_vkr_t12_qgb .section}

-   After you reset the logon password of a running instance, you must restart the instance so that the new password can take effect. Restarting the instance may impact your services. We recommend that you reset the logon password and restart your instance during off-peak business hours to avoid service disruption.
-   If your instance uses a password for authentication, the password authentication automatically becomes invalid after you [attach a key pair](../../../../../reseller.en-US/Security/Key pairs/How do I use an SSH key pair?.md#section_d4l_ql1_ydb) to your instance. However, if you reset the password of your instance after you attach a key pair to the instance, you can log on to the instance by using the password or the key pair.

## Prerequisite {#section_mg1_3fl_xdb .section}

The instance must be in a stable status, such as **Stopped** and **Running**. For more information, see [ECS instance life cycle](../../../../../reseller.en-US/Instances/ECS instance life cycle.md#).

## Procedure {#section_ng1_3fl_xdb .section}

To reset the password of one or multiple ECS instances, follow these steps:

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Select one or more target instances as follows:
    -   To reset the password of one instance, locate the target instance, and then choose **More** \> **Password/Key Pair** \> **Reset Password** in the **Actions** column.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9647/155486239832543_en-US.png)

    -   To reset the password of multiple instances, select the target instances, and then click **Reset Password** under the instance list.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9647/15548623985442_en-US.png)

5.  Specify a new valid password, and then click **Submit**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9647/15548623985443_en-US.png)

6.  Perform the following operations as needed:
    -   For a **Running** instance, [restart the instance](reseller.en-US/Instances/Manage instances/Restart an instance.md#) to make the new password take effect.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9647/155486239832546_en-US.png)

    -   For a **Stopped** instance, [start the instance](../../../../../reseller.en-US/Instances/Manage instances/Start or stop an instance.md#) to make the new password take effect.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9647/155486239832547_en-US.png)


You can also use Alibaba Cloud CLI, OpenAPI Explorer, or Alibaba Cloud SDK to call the [ModifyInstanceAttribute](../../../../../reseller.en-US/API Reference/Instances/ModifyInstanceAttribute.md#) API action to reset the logon password.

## What to do next {#section_sg1_3fl_xdb .section}

You can [change the password of an ECS instance](reseller.en-US/Instances/Manage instances/Change the password of an ECS instance.md#) and then [restart the instance](reseller.en-US/Instances/Manage instances/Restart an instance.md#) in the ECS console to make the new password take effect.

