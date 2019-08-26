# Console output and screenshot {#UserGuideLogScreenshot .concept}

ECS instances are virtualized cloud-based services that cannot be connected to any display devices and prohibit mobile snapshots. However, the console output of instances are cached at the time of the last startup, restart, or shutdown event. Moreover, you can obtain instance screenshots in real time. We recommend that you use these features to analyze and troubleshoot instance faults, such as operating system exception diagnosis, abnormal reboots, or unable to connect to instances.

## Limits {#Limits .section}

-   Instances running Windows Server image do not allow you to obtain console ouput.
-   [Phased-out instance types](https://partners-intl.aliyun.com/help/faq-detail/55263.htm) do not allow you to obtain instance console ouput or screenshots.
-   You cannot obtain console ouput or screenshots for instances created before January 1, 2018.

## Prerequisite {#Prerequisite .section}

The instance must be in the **Running** status. For more information, see [overview](reseller.en-US/User Guide/Connect to instances/Overview.md#).

## Procedure {#Operation .section}

You can view instance console output and screenshot from the Instance Details page, the Instances list page, or by calling API.

**Operation in Instance Details page**

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  Select and click the instance to troubleshoot and go to the **Instance Details** page.
5.  Click **More** \> **Get Instance Screenshot** to view the screenshot. Alternatively, click **More** \> **Get Instance Console Output** to monitor the root console.
6.  Check the instance screenshot or console output.
    -   Windows instance screenshot sample:

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15530/15433973457126_en-US.png)

    -   Linux instance screenshot sample:

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15530/15433973457127_en-US.png)

    -   Linux instance console output sample:

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15530/15433973457128_en-US.png)


**Operation in Instances list page**

1.  Log on to the [ECS console](https://partners-intl.console.aliyun.com/#/ecs).
2.  In the left-side navigation pane, click **Instances**.
3.  Select a region.
4.  Locate the instance to troubleshoot.
5.  In the **Actions** column, click **More** \> **Operations and Troubleshooting** \> **Get Instance Screenshot** to view the screenshot. Alternatively, click **More** \> **Operations and Troubleshooting** \> **Get Instance Console Output** to monitor the root console.
6.  Check the instance screenshot or console output.

**API operations**

-   Instance screenshots: [GetInstanceScreenshot](../../../../reseller.en-US/API Reference/Operations and monitoring/GetInstanceScreenshot.md#)
-   Instance console output: [GetInstanceConsoleOutput](../../../../reseller.en-US/API Reference/Operations and monitoring/GetInstanceConsoleOutput.md#)

## What to do next {#section_lhx_5dk_l2b .section}

For other troubleshooting instructions, see [link testing tool for ping packet loss or ping failure](https://partners-intl.aliyun.com/help/doc-detail/40573.htm).

