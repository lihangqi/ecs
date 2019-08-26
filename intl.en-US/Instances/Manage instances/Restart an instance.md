# Restart an instance {#concept_yxw_dwm_xdb .concept}

This topic describes how to restart an instance through the ECS console. You can also choose to call the RebootInstance API action.

## Limits {#section_vbt_v42_wfb .section}

-   Only instances in the **Running** state can be restarted.
-   When you restart an instance, the instance is stopped. As a result, services provided by the instance are disrupted.

## Procedure {#section_mwh_gxm_xdb .section}

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select the target region.
4.  Find the target instance, and then choose **More** \> **Instance Status** \> **Restart** in the **Actions** column.

    To restart multiple instances, select all required instances and then click **Restart** at the bottom of the instance list.

5.  In the displayed **Restart Instance** dialog box, select a **Restart Mode**, and then click **OK**.

Related API: [RebootInstance](../../../../reseller.en-US/API Reference/Instances/RebootInstance.md#)

