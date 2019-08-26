# Monitoring {#concept_fft_3xz_xdb .concept}

This topic describes how to monitor an ECS instance. Monitoring the status of your ECS instances helps you guarantee its normal running of your services. Alibaba Cloud provides features such as data monitoring, visualization of monitoring data, and real-time alerts to make sure that your ECS instances are running without interruption.

## Details {#section_thh_2xr_w2b .section}

You can monitor your ECS instances by using the ECS monitoring service or CloudMonitor. ECS provides CPU utilization, network traffic, and disk I/O monitoring for a specified instance. In CloudMonitor, you can monitor the instances by using a wider range of metrics with finer granularity. For more information about CloudMonitor, see [Host monitoring metrics](../../../../../reseller.en-US/User Guide/Host monitoring/Metrics.md#). Some of the metrics provided by the ECS monitoring service are described as follows.

-   CPU utilization: The percentage of allocated ECS compute units that are currently in use on the instance. A higher percentage indicates a higher CPU load on the instance. You can view the CPU utilization in the ECS console or in the CloudMonitor console. You can also obtain the data by calling the ECS API operations or after connecting to the specified instance through [remote connection](reseller.en-US/Instances/Connect to instances/Overview.md#). The following shows how to view the CPU utilization of different ECS instances after you connect the instance.
    -   Windows instance: View the CPU utilization in the Task Manager. You can then sort the tasks by CPU utilization to find the process that is consuming an abnormal amount of CPU resources in the specified ECS instance.
    -   Linux instance: Run the top command to view the CPU utilization. To locate the process that is consuming an abnormal amount of CPU resources in the specified ECS instance, press **Shift** + **P** to sort the tasks by CPU utilization.
-   Network traffic: The bandwidth usage for the inbound and outbound traffic of the ECS instance in kbps. ECS provides data connection monitoring, while CloudMonitor can monitor Internet and internal network traffic. If the outbound traffic reaches 1,024 kbps and the outbound bandwidth limit is 1 Mbps, the outbound bandwidth for the specified ECS instance is fully utilized.

## ECS monitoring service {#section_o2c_nxz_xdb .section}

To view the monitoring data in the ECS console, follow these steps.

1.  Find the target instance and click the instance ID.
2.  On the Instance Details page, you can view the **Monitoring Information** including CPU utilization and network traffic.

    1.  Click ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9747/15662692959889_en-US.png) to specify the **Start Time** and **End Time**.

        **Note:** The **Start Time** and **End Time** you specify affect the granularity of the data display. Smaller sampling intervals result in finer granularity of data displayed. For example, the average values shown will be different when you select a sampling interval of 5 and 15 minutes.

    2.  \(Optional\) Click **Set Alert Rule** and you will be directed to the CloudMonitor console. You can specify the CPU utilization and network traffic alarm rules. For more information about the metrics, see [Overview of alarm services](../../../../../reseller.en-US/User Guide/Alarm service/Alarm service overview.md#).
    3.  \(Optional\) Click **More Metrics** and you can view more monitoring data in the CloudMonitor console. Updates to the monitoring data may take a few minutes to display.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9747/15662692969888_en-US.png)


You can also call the ECS API operations [DescribeInstanceMonitorData](../reseller.en-US/API Reference/Operations and monitoring/DescribeInstanceMonitorData.md#), [DescribeDiskMonitorData](../reseller.en-US/API Reference/Operations and monitoring/DescribeDiskMonitorData.md#), and [DescribeEniMonitorData](../reseller.en-US/API Reference/Operations and monitoring/DescribeEniMonitorData.md#) to obtain the monitoring data.

The monitoring metrics in ECS are listed as follows. The sampling interval for each metric is 1 minute.

|Metric|Description|
|:-----|:----------|
|Instance|The instance ID.|
|CPU Usage|The percentage of allocated ECS compute units that are currently in use on the instance.|
|Intranet inbound traffic|The internal network traffic to your instance. Unit: kbit/s.|
|Intranet outbound traffic|The internal network traffic from your instance. Unit: kbit/s.|
|Intranet bandwidth|The internal network traffic of the instance per unit time. Unit: kbit/s.|
|Public network inbound traffic|The Internet traffic to the instance. Unit: kbit/s.|
|Public network outbound traffic|The Internet traffic from the instance. Unit: kbit/s.|
|Public network bandwidth|The internet traffic of the instance per unit time. Unit: kbit/s.|
|Disk read IOPS|The number of disk read operations per second.|
|Disk write IOPS|The number of disk write operations per second.|
|Disk read BPS|The number of bytes read from disk per second. Unit: Byte/s.|
|Disk write BPS|The number of bytes written to disk per second. Unit: Byte/s.|

## CloudMonitor {#section_ozt_sxz_xdb .section}

Alibaba Cloud CloudMonitor is a one-stop monitoring solution that provides monitoring for IT facilities and network quality, and service monitoring based on events, custom metrics, and logs. For more information about CloudMonitor, see [Host monitoring](../../../../../reseller.en-US/User Guide/Host monitoring/Host monitoring overview.md#). To view the monitoring data of your ECS instance in the CloudMonitor console, follow these steps.

1.  Log on to the [CloudMonitor console](https://partners-intl.console.aliyun.com/?spm=a2c63.p38356.a3.3.4e2b3770MrqQ1v#/cms).
2.  In the left-side navigation pane, click **Host Monitoring**.
3.  Select your target instance.
4.  \(Optional\) If your instance has not been installed with the CloudMonitor agent, click **Click to install**.
5.  -   To obtain the monitoring data, click **Monitoring Charts** in the **Actions** column.
-   To set alarm rules, click **Alarm Rules** in the **Actions** column.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/9747/15662692963939_en-US.png)


## About bandwidth units {#section_szt_sxz_xdb .section}

**Differences between Kb and KB**

-   A bit \(b\) is the smallest unit of data in a computer. A bit has a single binary value, either 0 or 1. Eight bits forms a Byte. For example, 0101 0010. 1 Byte = 8 bits \(1B = 8b\).
-   If K or k indicates kilo, one Kb equals one thousand bits, while a kilobyte \(KB\) equals 1,024 bytes.

In the ECS monitoring service, network traffic is measured in kbps, which is kilobit per second. Kbps indicates network speed, which is the number of kilobits transmitted per second. The unit bps is usually omitted when bandwidth is described. For example, the full form of 4M in the bandwidth scenario is 4 Mbps.

**Relations between bandwidth and download speed**

-   Common misunderstanding: Bandwidth is equivalent to download speed.
-   In theory, if a network bandwidth is 1 Mbps, the download speed can reach 125 KB/s. Download unit conversions are as follows: 1 KB = 8 Kb, 1 Mbps = 125 KB/s, 1 kbps= 1,000 bps.

    However, some applications running on the instance consume a small amount of bandwidth, such as remote desktop programs. Therefore, the actual download speed is usually between 100-110 KB/s.


