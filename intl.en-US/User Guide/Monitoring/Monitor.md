# Monitor {#concept_fft_3xz_xdb .concept}

You can monitor the operating statuses of instances to ensure optimal performance.

You can monitor the status of instances using the following two portals:

-   Instance Details page
-   CloudMonitor

## Monitor the status of an instance by using Instance Details page {#section_o2c_nxz_xdb .section}

1.  [Log on to the ECS console](https://ecs.console.aliyun.com/?spm=a2c4g.11186623.2.9.FNEORG#/home).
2.  In the left-side navigation pane, click **Instances**. Select a region.
3.  Click an instance to go to the Instance Details page.
4.  On the Instance Details  page, you can view the monitoring information, including CPU utilization and outbound/inbound network traffic information.

-   Information about CPU monitoring: For Linux instances, use the top command to view CPU usage details. Log on to the instance and run the top command in the command line. 
    -   Then, pressShift+P key to list programs by CPU utilization to view which processes are using the most CPU resources.
    -   For Windows instances,  use the Task Manager on an instance to  view the CPU utilization to view which programs are using the CPU resources of the server.
-   The displayed monitoring data shows the Internet traffic of the instance in Kbps \(1 Mbps = 1,024 Kbps\).  The monitoring data shows inbound and outbound instance traffic.  For 1 Mbps of bandwidth,  the bandwidth is working at full capacity if the outbound network traffic reaches 1,024 Kbps.

## CloudMonitor {#section_ozt_sxz_xdb .section}

1.  To install a CloudMonitor, follow these steps:**In the Alibaba Cloud Console, choose Products and Services \> ** \> **CloudMonitor**.
2.  In the left-side navigation pane, click Host Monitoring, and then select the name of the instance you want to monitor.
3.   Click Install to monitor the operating system of the instance. Click Batch Install to monitor the instance OS, click Monitoring Chart to view basic parameters, and click Alarm Rules to set alarm rules.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9747/15349236263939_en-US.png)


For more information about CloudMonitor, see CloudMonitor Product Documentation.

