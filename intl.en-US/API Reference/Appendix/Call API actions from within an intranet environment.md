# Call API actions from within an intranet environment {#concept_226934 .concept}

This topic describes how to configure PrivateZone so that you can call API actions for ECS instances in a VPC through the provided domain name system \(DNS\) service of PrivateZone.

## Background information {#Context .section}

The endpoints provided by Alibaba Cloud ECS can be used to send API calls over the Internet. However, if your ECS instance is not assigned an Internet bandwidth package or a public IP address, the instance cannot initiate an API action request by using the Alibaba Cloud CLI or corresponding SDK. To ensure that your instance can send API requests from Alibaba Cloud intranet, Alibaba Cloud provides the PrivateZone solution. You can use PrivateZone to associate the VPC with the region to which your ECS instance belongs.

## Limits {#section_b26_sgt_s1a .section}

-   You can configure PrivateZone only for the region where your VPC-connected ECS instances are located. You cannot configure PrivateZone across multiple regions.
-   We recommend that you create instances by using custom images that have been deployed with Alibaba Cloud CLI or SDK. This allows your ECS instances to load relevant dependencies even when they have no access to the Internet.
-   Currently, only the following ECS endpoints support PrivateZone.

    |Alibaba Cloud region|Region ID|CNAME record value|Internet endpoint|
    |--------------------|---------|------------------|-----------------|
    |China \(Beijing\)|cn-beijing|popunify-vpc.cn-beijing.aliyuncs.com|ecs.cn-beijing.aliyuncs.com|
    |China \(Hangzhou\)|cn-hangzhou|popunify-vpc.cn-hangzhou.aliyuncs.com|ecs.cn-hangzhou.aliyuncs.com|
    |China \(Shanghai\)|cn-shanghai|popunify-vpc.cn-shanghai.aliyuncs.com|ecs.cn-shanghai.aliyuncs.com|
    |China \(Shenzhen\)|cn-shenzhen|popunify-vpc.cn-shenzhen.aliyuncs.com|ecs.cn-shenzhen.aliyuncs.com|
    |China \(Hohhot\)|cn-huhehaote|popunify-vpc.cn-huhehaote.aliyuncs.com|ecs.cn-huhehaote.aliyuncs.com|
    |China \(Zhangjiakou-Beijing Winter Olympics\)|cn-zhangjiakou|popunify-vpc.cn-zhangjiakou.aliyuncs.com|ecs.cn-zhangjiakou.aliyuncs.com|
    |China \(Hong Kong\)|cn-hongkong|popunify-vpc.cn-hongkong.aliyuncs.com|ecs.cn-hongkong.aliyuncs.com|
    |Singapore|ap-southeast-1|popunify-vpc.ap-southeast-1.aliyuncs.com|ecs.ap-southeast-1.aliyuncs.com|
    |Germany \(Frankfurt\)|eu-central-1|popunify-vpc.eu-central-1.aliyuncs.com|ecs.eu-central-1.aliyuncs.com|


## Procedure {#section_2ju_5zf_3md .section}

1.  Log on to the [Alibaba Cloud DNS console](https://partners-intl.console.aliyun.com/#/dns/domainList).
2.  In the left-side navigation pane, click **PrivateZone**.
3.  Click **Add Zone**.
4.  In the displayed dialog box, set the parameters as needed, and then click **OK**.

    -   **Zone Name**: Set an ECS endpoint that supports PrivateZone. In this example, set the zone name to ecs.cn-hangzhou.aliyuncs.com.
    -   **Subdomain recursive resolution proxy**: If you select this option, the name resolved on the Internet is used when DNS detects a domain name with the suffix Zone that is not included in the Zone file.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190084/156618484546151_en-US.png)

5.  Locate the created PrivateZone, and then click **Configure** in the **Actions** column.
6.  On the displayed **Resolution Settings** page, click **Add Record**.
7.  In the displayed dialog box, set the parameters as needed, and then click **OK**.

    -   **Record Type**: Select **CNAME**.
    -   **Resource Records**: Enter @ to resolve the @.example.com domain name.
    -   **Record Value**: Set it to the CNAME record value of the corresponding region. For more information, see [Limits](#section_b26_sgt_s1a).
    -   **TTL Value**: The time to live value. In this example, select **1 minute\(s\)**.
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190084/156618484546154_en-US.png)

8.  Go back to the **PrivateZone** page, locate the created PrivateZone, and then click **Bind VPC** in the **Actions** column.
9.  In the displayed dialog box, select the region where the PrivateZone is located, select one or more VPCs to which your ECS instance belongs, and then click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190084/156618484646161_en-US.png)


## What to do next {#section_mzc_end_wml .section}

After you associate a VPC with your PrivateZone, you can log on to your ECS instance to check whether the instance can access the endpoint of the corresponding region. For more information, see [Connect to an instance by using the Management Terminal](../../../../reseller.en-US/Instances/Connect to instances/Connect to Linux instances/Connect to an instance by using the Management Terminal.md#). For example, if the zone name is ecs.cn-hangzhou.aliyuncs.com, you can:

-   Conduct a ping test to check whether data packets can be properly transmitted and received.

    ``` {#codeblock_744_z6z_zhk}
    ping ecs.cn-hangzhou.aliyuncs.com
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190084/156618484646338_en-US.png)

-   Use Alibaba Cloud CLI to call [DescribeRegions](reseller.en-US/API Reference/Regions/DescribeRegions.md#), and change the endpoint in the --endpoint field.

    ``` {#codeblock_g7i_i2p_t0q}
    aliyun ecs DescribeRegions --endpoint ecs.cn-hangzhou.aliyuncs.com
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/190084/156618484646404_en-US.png)


