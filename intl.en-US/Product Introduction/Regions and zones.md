# Regions and zones {#concept_h4v_j5k_xdb .concept}

This topic provides a complete list of Alibaba Cloud regions and zones.

Regions in Alibaba Cloud are independent. Zones in Alibaba Cloud are completely isolated. However, zones in the same region are connected through links with low latency. The following figure shows the relationship between regions and zones in Alibaba Cloud.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/13778/156618320744660_en-US.jpg)

## Regions {#section_ug5_k5k_xdb .section}

Alibaba Cloud regions are physical locations \(data centers\) that spread all over the world to reduce the network latency. The region cannot be changed once a resource is created in it. The following table lists all Alibaba Cloud regions, corresponding cities, and Region IDs.

**Note:** The available regions vary according to the product. To view the list of regions available for each product, see [Alibaba Cloud Global Infrastructure](https://www.alibabacloud.com/global-locations).

-   Regions in Mainland China

    |Region name|City|Region ID|Number of zones|
    |-----------|----|---------|---------------|
    |China North 1|Qingdao|cn-qingdao|2|
    |China North 2|Beijing|cn-beijing|8|
    |China North 3|Zhangjiakou|cn-zhangjiakou|2|
    |China North 5|Hohhot|cn-huhehaote|2|
    |China East 1|Hangzhou|cn-hangzhou|8|
    |China East 2|Shanghai|cn-shanghai|6|
    |China South 1|Shenzhen|cn-shenzhen|5|
    |China SW 1|Chengdu|cn-chengdu|1|

-   International regions

    |Region name|City|Region ID|Number of zones|
    |-----------|----|---------|---------------|
    |China \(Hong Kong\)|Hong Kong|cn-hongkong|2|
    |Asia Pacific SE 1|Singapore|ap-southeast-1|3|
    |Asia Pacific SE 2|Sydney|ap-southeast-2|2|
    |Asia Pacific SE 3|Kuala Lumpur|ap-southeast-3|2|
    |Asia Pacific SE 5|Jakarta|ap-southeast-5|2|
    |Asia Pacific SOU 1|Mumbai|ap-south-1|2|
    |Asia Pacific NE 1|Tokyo|ap-northeast-1|2|
    |US West 1|Silicon Valley|us-west-1|2|
    |US East 1|Virginia|us-east-1|2|
    |EU Central 1|Frankfurt|eu-central-1|2|
    |UK \(London\)|London|eu-west-1|2|
    |Middle East 1|Dubai|me-east-1|1|


When choosing a region, consider the following factors:

-   Geographic location

    Choose a region based on the geographic locations of you and your target users.

    -   Regions in mainland China

        In general, we recommend that you choose the data center closest to your target users so that they have fast access. Alibaba Cloud's data centers of the regions in mainland China are similar to each other in terms of infrastructure, BGP network quality, service quality, ECS operation and configuration. The regions offer BGP backbone network lines covering all provinces, autonomous regions, and municipalities to guarantee fast, stable access within mainland China.

    -   International regions

        Alibaba Cloud’s international regions are data centers outside mainland China. They offer access at international bandwidth, targeting areas outside mainland China. Users in mainland China that access services deployed in these regions may experience high latency. Therefore, we do not recommend deploying services in international regions if users from mainland China require access.

        -   If you have business operations in China \(Hong Kong\) or Southeast Asia, choose the region China \(Hong Kong\), Asia Pacific SE 1, Asia Pacific SE 3, or Asia Pacific SE 5.
        -   If you have business operations in Japan and Korea, choose the Asia Pacific NE 1.
        -   If you have business operations in India, choose the region Asia Pacific SOU 1.
        -   If you have business operations in Australia, choose the region Asia Pacific SE 2.
        -   If you have business operations in America, choose the region US East 1 or US West 1.
        -   If you have business operations in Continental Europe, choose the region EU Central 1.
        -   If you have business operations in the Middle East, choose the Eastern Middle East 1 region.
-   Intranet communication between Alibaba Cloud products across regions

    Intranet communication between Alibaba Cloud products that are not in the same region is not supported, which means:

    -   ECS instances and other products, such as ApsaraDB for RDS and OSS instances, cannot communicate with one another over the intranet if they are in different regions.
    -   Server Load Balancer cannot be deployed for ECS instances in different regions.
-   Resource pricing

    The price of resources may vary according to the region. For details, see the [product pricing page](https://www.alibabacloud.com/pricing).

-   Business license filing

    When you choose a region, consider the special requirements of some areas. If you have purchased an ECS instance in mainland China and used it for a web server, complete business license filing first.

    To complete business license filing, pay attention to the following points:

    -   If your company is located in Beijing, choose the **China North 2** region for the ECS instance you have purchased.
    -   If your company is located in Guangdong, choose the **China South 1** region for the ECS instance you have purchased.
    **Note:** The communications administrations in different provinces, autonomous regions, and municipalities have different approval requirements for business license filing. In case of any change, the information published on the business license filing website of your local administration prevails.


## Zones {#section_gfh_z5k_xdb .section}

Zones are physical areas with independent power grids and networks within one region. The network latency for instances within the same zone is lower.

Intranet communication can take place between instances in different zones of the same region, and fault isolation can be achieved between zones. Whether or not instances can be deployed in the same zone depends on the requirements for disaster recovery and network latency.

-   If your applications require high disaster recovery capabilities, we recommend that you deploy your instances in different zones of the same region.
-   If your applications require low network latency between instances, we recommend that you create your instances in the same zone.

For more information about regions and zones, see the [Alibaba Cloud Global Infrastructure](https://www.alibabacloud.com/global-locations).

