# Use APIs to manage preemptible instances {#concept_cqh_xtk_kfb .concept}

This topic describes how to use Alibaba Cloud ECS SDKs to quickly create and manage preemptible instances.

## Preparation {#section_esp_ytk_kfb .section}

Before you begin, make sure that:

-   You know which instance types and regions meet your business requirements.
-   You have a basic understanding of Alibaba Cloud ECS SDKs and calling methods. For more information, [see SDK documentation](../../../../reseller.en-US/Java SDK/Getting started.md#).
-   The ECS SDK version for preemptible instances is 4.2.0 and later. Here is an example of how to change the pom dependency.

    ```
    <dependency>
      <groupId>com.aliyun</groupId>
      <artifactId>aliyun-java-sdk-core</artifactId>
      <version>3.2.8</version>
    </dependency>
    <dependency>
      <groupId>com.aliyun</groupId>
      <artifactId>aliyun-java-sdk-ecs</artifactId>
      <version>4.2.0</version>
    </dependency>
    ```


## Query regions and available instance types {#section_j4y_c5k_kfb .section}

Use the [DescribeZones](../../../../reseller.en-US/API Reference/Regions/DescribeZones.md#) interface to query the regions where you can create preemptible instances and the available instance types. The sample code is as follows:

-   OpenApiCaller.java

    ```
    public class OpenApiCaller {
      IClientProfile profile;
      IAcsClient client;
      public OpenApiCaller() {
          profile = DefaultProfile.getProfile("cn-hangzhou", AKSUtil.accessKeyId, AKSUtil.accessKeySecret);
          client = new DefaultAcsClient(profile);
      }
      public  <T extends AcsResponse> T doAction(AcsRequest<T> var1) {
          try {
              return  client.getAcsResponse(var1);
          } catch (Throwable e) {
              e.printStackTrace();
              return null;
          }
      }
    ｝
    ```

-   DescribeZonesSample.java

    ```
    public class DescribeZonesSample {
      public static void main(String[] args) {
          OpenApiCaller caller = new OpenApiCaller();
          DescribeZonesRequest request = new DescribeZonesRequest();
          request.setRegionId("cn-zhangjiakou");//You can use DescribeRegionsRequest to get the RegionId of each region
          request.setSpotStrategy("SpotWithPriceLimit");//This field must be entered to query the availability of instance types
          request.setInstanceChargeType("PostPaid");//Post-paid mode, preemptible instances must be post-paid
          DescribeZonesResponse response = caller.doAction(request);
          System.out.println(JSON.toJSONString(response));
      }
    }
    ```


In the following output result, you can see the instance types, disk types, and network types available in each region.

```
{
  "requestId": "388D6321-E587-470C-8CFA-8985E2963DAE",
  "zones": [
      {
          "localName": "China North 3 Zone A",
          "zoneId": "cn-zhangjiakou-a",
          "availableDiskCategories": [
              "cloud_ssd",
              "cloud_efficiency"
          ],
          "availableInstanceTypes": [
              "ecs.e4.large",
              "ecs.n4.4xlarge",
              "ecs.sn2.medium",
              "ecs.i1.2xlarge",
              "ecs.se1.2xlarge",
              "ecs.n4.xlarge",
              "ecs.se1ne. 2xlarge",
              "ecs.se1.large",
              "ecs.sn2.xlarge",
              "ecs.se1ne.xlarge",
              "ecs.xn4.small",
              "ecs.sn2ne. 4xlarge",
              "ecs.se1ne. 4xlarge",
              "ecs.sn1.medium",
              "ecs.n4.8xlarge",
              "ecs.mn4.large",
              "ecs.e4.2xlarge",
              "ecs.mn4.2xlarge",
              "ecs.mn4.8xlarge",
              "ecs.n4.2xlarge",
              "ecs.e4.xlarge",
              "ecs.sn2ne.large",
              "ecs.sn2ne.xlarge",
              "ecs.sn1ne.large",
              "ecs.n4.large",
              "ecs.sn1.3xlarge",
              "ecs.e4.4xlarge",
              "ecs.sn1ne. 2xlarge",
              "ecs.e4.small",
              "ecs.i1.4xlarge",
              "ecs.se1.4xlarge",
              "ecs.sn2ne. 2xlarge",
              "ecs.sn2.3xlarge",
              "ecs.i1.xlarge",
              "ecs.n4.small",
              "ecs.sn1ne. 4xlarge",
              "ecs.mn4.4xlarge",
              "ecs.sn1ne.xlarge",
              "ecs.se1ne.large",
              "ecs.sn2.large",
              "ecs.i1-c5d1.4xlarge",
              "ecs.sn1.xlarge",
              "ecs.sn1.large",
              "ecs.mn4.small",
              "ecs.mn4.xlarge",
              "ecs.se1.xlarge"
          ],
          "availableResourceCreation": [
              "VSwitch",
              "IoOptimized",
              "Instance",
              "Disk"
          ],
          "availableResources": [
              {
                  "dataDiskCategories": [
                      "cloud_ssd",
                      "cloud_efficiency"
                  ],
                  "instanceGenerations": [
                      "ecs-3",
                      "ecs-2"
                  ],
                  "instanceTypeFamilies": [
                      "ecs.mn4",
                      "ecs.sn1",
                      "ecs.sn2",
                      "ecs.sn1ne",
                      "ecs.xn4",
                      "ecs.i1",
                      "ecs.se1",
                      "ecs.e4",
                      "ecs.n4",
                      "ecs.se1ne",
                      "ecs.sn2ne"
                  ],
                  "instanceTypes": [
                      "ecs.n4.4xlarge",
                      "ecs.sn2.medium",
                      "ecs.i1.2xlarge",
                      "ecs.se1.2xlarge",
                      "ecs.n4.xlarge",
                      "ecs.se1ne. 2xlarge",
                      "ecs.se1.large",
                      "ecs.sn2.xlarge",
                      "ecs.se1ne.xlarge",
                      "ecs.xn4.small",
                      "ecs.sn2ne. 4xlarge",
                      "ecs.se1ne. 4xlarge",
                      "ecs.sn1.medium",
                      "ecs.n4.8xlarge",
                      "ecs.mn4.large",
                      "ecs.mn4.2xlarge",
                      "ecs.mn4.8xlarge",
                      "ecs.n4.2xlarge",
                      "ecs.sn2ne.large",
                      "ecs.sn2ne.xlarge",
                      "ecs.sn1ne.large",
                      "ecs.n4.large",
                      "ecs.sn1.3xlarge",
                      "ecs.sn1ne. 2xlarge",
                      "ecs.e4.small",
                      "ecs.i1.4xlarge",
                      "ecs.se1.4xlarge",
                      "ecs.sn2ne. 2xlarge",
                      "ecs.sn2.3xlarge",
                      "ecs.i1.xlarge",
                      "ecs.n4.small",
                      "ecs.sn1ne. 4xlarge",
                      "ecs.mn4.4xlarge",
                      "ecs.sn1ne.xlarge",
                      "ecs.se1ne.large",
                      "ecs.sn2.large",
                      "ecs.i1-c5d1.4xlarge",
                      "ecs.sn1.xlarge",
                      "ecs.sn1.large",
                      "ecs.mn4.small",
                      "ecs.mn4.xlarge",
                      "ecs.se1.xlarge"
                  ],
                  "ioOptimized": true,
                  "networkTypes": [
                      "vpc"
                  ],
                  "systemDiskCategories": [
                      "cloud_ssd",
                      "cloud_efficiency"
                  ]
              }
          ],
          "availableVolumeCategories": [
              "san_ssd",
              "san_efficiency"
          ]
      }
  ]
}
```

## Query preemptible instance price history {#section_pgr_35k_kfb .section}

Use the [DescribeSpotPriceHistory](../../../../reseller.en-US/API Reference/Instances/DescribeSpotPriceHistory.md#) interface to query the price changes of a preemptible instance type over the last 30 days, so you can find the most cost efficient regions and instance types. The sample code \(DescribeSpotPriceHistorySample.java\) is as follows.

```
public class DescribeSpotPriceHistorySample {
    public static void main(String[] args) {
        OpenApiCaller caller = new OpenApiCaller();
        List<DescribeSpotPriceHistoryResponse.SpotPriceType> result = new ArrayList<DescribeSpotPriceHistoryResponse.SpotPriceType>();
        int offset = 0;
        while (true) {
            DescribeSpotPriceHistoryRequest request = new DescribeSpotPriceHistoryRequest();
            request.setRegionId("cn-hangzhou");//You can use DescribeRegionsRequest to get the RegionId of each region where preemptible instances are available
            request.setZoneId("cn-hangzhou-b");//You must enter the zone
            request.setInstanceType("ecs.sn2.medium");//See the instance types returned by DescribeZones, this field is mandatory
            request.setNetworkType("vpc");//See the network types returned by DescribeZones, this field is mandatory
//            request.setIoOptimized("optimized");//Determines if the instance is I/O optimized, see IoOptimized returned by DescribeZones, this field is optional
//            request.setStartTime("2017-09-20T08:45:08Z");//The price start time, optional, default value: within 3 days
//            request.setEndTime("2017-09-28T08:45:08Z");//Price end time, optional
            request.setOffset(offset);
            DescribeSpotPriceHistoryResponse response = caller.doAction(request);
            if (response ! = null && response.getSpotPrices() ! = null) {
                result.addAll(response.getSpotPrices());
            }
            if (response.getNextOffset() == null || response.getNextOffset() == 0) {
                break;
            } else {
                offset = response.getNextOffset();
            }
        }
        if (! result.isEmpty()) {
            for (DescribeSpotPriceHistoryResponse.SpotPriceType spotPriceType : result) {
                System.out.println(spotPriceType.getTimestamp() + "--->spotPrice:" + spotPriceType.getSpotPrice() + "---->originPrice:" + spotPriceType.getOriginPrice());
            }
            System.out.println(result.size());
        } else {
        }
    }
}
```

Returned results sample.

```
2017-09-26T06:28:55Z--->spotPrice:0.24---->originPrice:1.2
2017-09-26T14:00:00Z--->spotPrice:0.36---->originPrice:1.2
2017-09-26T15:00:00Z--->spotPrice:0.24---->originPrice:1.2
2017-09-27T14:00:00Z--->spotPrice:0.36---->originPrice:1.2
2017-09-27T15:00:00Z--->spotPrice:0.24---->originPrice:1.2
2017-09-28T14:00:00Z--->spotPrice:0.36---->originPrice:1.2
2017-09-28T15:00:00Z--->spotPrice:0.24---->originPrice:1.2
2017-09-29T06:28:55Z--->spotPrice:0.24---->originPrice:1.2
```

Repeat this process to find the price trends and recent prices of the instance type in each zones.

**Note:** You can use average price or maximum price to determine if you can afford this preemptible instance. You can also use more rational data models to analyze historical price data and adjust your instance types and zones at will for maximum cost effectiveness.

## Create a preemptible instance {#section_ryl_n5k_kfb .section}

You must complete the following work before creating a preemptible instance:

-   To use a custom image to create a preemptible instance, you must have already [CreateImage](../../../../reseller.en-US/API Reference/Images/CreateImage.md#).
-   [Create a security group](../../../../reseller.en-US/User Guide/Security groups/Create a security group.md#) in the console or use the [CreateSecurityGroup](../../../../reseller.en-US/API Reference/Security groups/CreateSecurityGroup.md#) to create a security group. Then, retrieve the security group ID \(SecurityGroupId\).
-   In the console, create [a VPC and VSwitch](../../../../reseller.en-US/User Guide/Manage a VPC.md#), or use the [CreateVpc](../../../../reseller.en-US/API reference/Virtual Private Cloud (VPC)/CreateVpc.md#) and [CreateVSwitch](../../../../reseller.en-US/API reference/VSwitch/CreateVSwitch.md#) interfaces to do so. Then, retrieve the VSwitch ID \(VSwitchId\).

Use the [CreateInstance](../../../../reseller.en-US/API Reference/Instances/CreateInstance.md#) to create a preemptible instance. The sample code \(CreateInstaneSample.java\) is as follows.

```
public class CreateInstaneSample {
    public static void main(String[] args) {
        OpenApiCaller caller = new OpenApiCaller();
        CreateInstanceRequest request = new CreateInstanceRequest();
        request.setRegionId("cn-hangzhou");//The region ID
        request.setZoneId("cn-hangzhou-b"); //The zone ID
        request.setSecurityGroupId("sg-bp11nhf94ivkdxwb2gd4");//The ID of the security group
        request.setImageId("centos_7_03_64_20G_alibase_20170818.vhd");//We recommend that you select a custom image you have prepared in this region
        request.setVSwitchId("vsw-bp164cyonthfudn9kj5br");//For VPC, the VSwitch ID is required
        request.setInstanceType("ecs.sn2.medium"); //Enter the instance type you want to purchase
        request.setIoOptimized("optimized");//See the parameters returned by DescirbeZones
        request.setSystemDiskCategory("cloud_ssd");//See the parameters returned by DescirbeZones, select one: cloud_ssd, cloud_efficiency, or cloud
        request.setSystemDiskSize(40);
        request.setInstanceChargeType("PostPaid");//Post-paid is required for preemptible instances
        request.setSpotStrategy("SpotWithPriceLimit");//SpotWithPriceLimit: bid mode, SpotAsPriceGo: no bids, the maximum Pay-As-You-Go price
        request.setSpotPriceLimit(0.25F);//This applies only to SpotWithPriceLimit. Set the maximum price you are willing to pay, units: USD/hour. An instance is created when this price is higher than the current market price
        CreateInstanceResponse response = caller.doAction(request);
        System.out.println(response.getInstanceId());
    }
}
```

## Recover a preemptible instance {#section_urn_p5k_kfb .section}

Mandatory recovery can be imposed on preemptible instances due to changes in price or supply and demand. At such a time, the operation of the preemptible instance is suspended. Before being released, the preemptible instance enters the locked status and a prompt notifies you that the instance will be automatically recovered. You can design a withdrawal logic to automatically process instances in the recovery status.

Now, you can use the following methods to determine the suspension and lock statuses of preemptible instances:

-   Obtain this information from the [instance metadata](../../../../reseller.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#). Run the following command.

    ```
    curl 'http://100.100.100.200/latest/meta-data/instance/spot/termination-time'
    ```

    If the returned result is blank, this indicates the instance can continue to be used. If no result is returned, it indicates the instance can continue to be used. If the returned result contains UTC time stamp information in the format of YYYY-MM-DDTHH:mm:ssZ \(for example `2015-01-05T18:02:00Z`\), it indicates the instance will be released at the specified time.

-   You can use the OperationLocks information returned by the [DescribeInstances](../../../../reseller.en-US/API Reference/Instances/DescribeInstances.md#) to see if an instance is in the Awaiting Recovery status. The sample code \(DescribeInstancesSample.java\) is as follows.

    ```
    public class DescribeInstancesSample {
      public static void main(String[] args) throws InterruptedException {
          OpenApiCaller caller = new OpenApiCaller();
          JSONArray allInstances = new JSONArray();
          allInstances.addAll(Arrays.asList("i-bp18hgfai8ekoqwo0y2n", "i-bp1ecbyds24ij63w146c"));
          while (! allInstances.isEmpty()) {
              DescribeInstancesRequest request = new DescribeInstancesRequest();
              request.setRegionId("cn-hangzhou");
              request.setInstanceIds(allInstances.toJSONString());//Specify the instance ID, maximum efficiency
              DescribeInstancesResponse response = caller.doAction(request);
              List<DescribeInstancesResponse.Instance> instanceList = response.getInstances();
              if (instanceList ! = null && ! instanceList.isEmpty()) {
                  for (DescribeInstancesResponse.Instance instance : instanceList) {
                      System.out.println("result:instance:" + instance.getInstanceId() + ",az:" + instance.getZoneId());
                      if (instance.getOperationLocks() ! = null) {
                          for (DescribeInstancesResponse.Instance.LockReason lockReason : instance.getOperationLocks()) {
                              System.out.println("instance:" + instance.getInstanceId() + "-->lockReason:" + lockReason.getLockReason() + ",vmStatus:" + instance.getStatus());
                              if ("Recycling".equals(lockReason.getLockReason())) {
                                  //do your action
                                  System.out.println("spot instance will be recycled immediately, instance id:" + instance.getInstanceId());
                                  allInstances.remove(instance.getInstanceId());
                              }
                          }
                      }
                  }
                  System.out.print("try describeInstances again later ...") ;
                  Thread.sleep(2 * 60 * 1000);
              } else {
                  break;
              }
          }
      }
    }
    ```


The output result when recovery is triggered is as follows.

```
instance:i-bp1ecbyds24ij63w146c-->lockReason:Recycling,vmStatus:Stopped
spot instance will be recycled immediately, instance id:i-bp1ecbyds24ij63w146c
```

## Other operations {#section_bzw_v5k_kfb .section}

You can start, stop, and release preemptible instances. These operations are the same as Pay-As-You-Go instances. For more information, see:

-   Start an instance: [StartInstance](../../../../reseller.en-US/API Reference/Instances/StartInstance.md#)
-   Stop an instance: [StopInstance](../../../../reseller.en-US/API Reference/Instances/StopInstance.md#)
-   Release an instance: [DeleteInstance](../../../../reseller.en-US/API Reference/Instances/DeleteInstance.md#)

