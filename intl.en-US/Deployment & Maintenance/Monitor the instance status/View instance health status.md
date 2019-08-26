# View instance health status {#concept_gc3_psr_pgb .concept}

Alibaba Cloud Elastic Computing Service \(ECS\) can perform periodic checks on each instance to identify system issues. This topic describes how to view detected issues and check the instance health status on the ECS console or through API calls.

## Benefits {#section_n23_qsw_pgb .section}

The instance health status is different from the life cycle status of your instance \(such as `pending`, `running`, or `stopped`\), instead it focuses on abnormal activities of network configuration, software crashes, and hardware usage. By monitoring the instance status, you can record network, software, or hardware issues in time to keep your applications running continuously in Alibaba Cloud ECS.

Meanwhile, by using the metric monitoring features of [CloudMonitor](../../../../../reseller.en-US/Product Introduction/Overview.md#), you can have systematic overview of computing resource maintenance.

## Health status {#section_grl_cvw_pgb .section}

The health status is returned for each instance query performed. If the health check is passed, the health status is **Normal**. When the health check fails, the health status returns other metrics. See the following tables for the list of health status codes:

|Console UI|API values|Description|Highlight color|
|:---------|:---------|:----------|:--------------|
|Normal|OK|The health status check is passed.|Green|
|Impaired|Impaired|The instance performance is impaired.|Red|
|Warning|The instance performance may have degraded because of maintenance or technical issues.|Red|
|Maintaining|The instance is under maintenance.|Red|
|Initializing|The instance is being initialized.|Red|
|InsufficientData|The health status cannot be determined because of insufficient data.|Red|
|NotApplicable|The instance health status is not applicable.|Red|

## View the health status by using the console {#section_bfz_kzw_pgb .section}

1.  Find the ECS instance whose health status you want to view, and click the instance.
2.  View the health status of the instance in the upper-right corner of the **Instance Details** page.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/122606/156533712638356_en-US.png)


## View the health status by calling APIs {#section_efm_s2x_pgb .section}

This section uses the Alibaba Cloud CLI to demonstrate the API procedure. For other developer tool instructions, see [Quick start for ECS APIs](../reseller.en-US/API Reference/Quick start for ECS APIs.md#).

-   Run the following commands to view the health status of a specific instance by calling [DescribeInstances](../reseller.en-US/API Reference/Instances/DescribeInstances.md#) and [DescribeInstancesFullStatus](../reseller.en-US/API Reference/System event/DescribeInstancesFullStatus.md#):

``` {#codeblock_mcj_652_xl2}
aliyun ecs DescribeInstances --RegionId cn-hangzhou --output cols=InstanceId,InstanceName
aliyun ecs DescribeInstancesFullStatus --RegionId cn-hangzhou --InstanceId.1 i-bp1afnc98r8k69XXXXXX --output cols=HealthStatus
```

-   Execute the following command to view the health status of instances located in a specific region by calling [DescribeInstancesFullStatus](../reseller.en-US/API Reference/System event/DescribeInstancesFullStatus.md#):

``` {#codeblock_2bu_9oc_de0}
aliyun ecs DescribeInstancesFullStatus --RegionId cn-hangzhou --output cols=HealthStatus
```


