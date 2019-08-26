# Quick start for ECS APIs {#EcsApiGettingStarted .concept}

This topic describes how to call ECS APIs by using different developer tools, such as the Alibaba Cloud CLI, OpenAPI Explorer, and the Alibaba Cloud Java SDK. The topic takes CreateSnapshot as the example API to call.

## Use the Alibaba Cloud CLI {#section_rn1_hys_lgb .section}

This example shows how to create a snapshot by calling the API \([CreateSnapshot](reseller.en-US/API Reference/Snapshots/CreateSnapshot.md#)\) through Alibaba Cloud CLI. Before calling the API, please read the API documentation to understand its usage and learn about the required request parameters. If errors are reported when you call the API, you can check the corresponding API documentation for troubleshooting.

1.  Get the instance ID.
    -   If you have connected to the ECS instance, you can use [metadata](../../../../../reseller.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#) to get the instance ID. For example, Linux instance can run the following commands:

        ```
        curl http://100.100.100.200/2016-01-01/meta-data/instance-id
        ```

    -   On your local computer, you can call [DescribeInstances](reseller.en-US/API Reference/Instances/DescribeInstances.md#) to get the instance ID:

        ```
        aliyun ecs DescribeInstances --output cols=InstanceId,InstanceName
        ```

2.  Use [DescribeInstances](reseller.en-US/API Reference/Instances/DescribeInstances.md#) to filter for the target disk ID:

    ```
    aliyun ecs DescribeInstances --RegionId cn-hangzhou --InstanceId i-bp1afnc98r8k69XXXXXX --output cols=DiskId
    ```

3.  Use [CreateSnapshot](reseller.en-US/API Reference/Snapshots/CreateSnapshot.md#) to create a snapshot based on the disk ID:

    ```
    aliyun ecs CreateSnapshot --DiskId d-bp19pjyf12hebpXXXXXX
    ```

    If the following information is returned, the snapshot creation task has been successfully initiated:

    ```
    {"RequestId":"16B856F6-EFFB-4397-8A8A-CB73FAXXXXXX","SnapshotId":"s-bp1afnc98r8kjhXXXXXX"}
    ```

4.  Use [DescribeSnapshots](reseller.en-US/API Reference/Snapshots/DescribeSnapshots.md#) to query the snapshot creation status. If `"SnapshotId"="s-bp1afnc98r8kjhXXXXXX"` and `"Status":"accomplished"` are shown at the same time, it indicates that the snapshot has been successfully created.

    ```
    aliyun ecs DescribeSnapshots --RegionId cn-hangzhou --InstanceId i-bp1afnc98r8k69XXXXXX --output cols=SnapshotId,Status
    ```


## Use the Java SDK {#section_s1c_2qg_mgb .section}

This example shows how to create a snapshot \([CreateSnapshot](reseller.en-US/API Reference/Snapshots/CreateSnapshot.md#)\) through [Java SDK](https://github.com/aliyun). For how to configure ECS SDK, see [Install the new Java SDK](../../../../../reseller.en-US/SDK Reference/Download and install Java SDKs.md#).

**Note:** For the `<AccessKey>` \(your AccessKeyId\), `<AccessSecret>` \(your AccessKeySecret\), `<RegionId>` \(the ID of the region to which the instance belongs\), and `<DiskId>` \(disk ID\), you need to enter them according to your actual scenario. For more information, see [Create an accesskey](../../../../../reseller.en-US/General Reference/Create an AccessKey.md#) and [Regions and zones](../../../../../reseller.en-US/General Reference/Regions and zones.md#).

```language-java
import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.IAcsClient;
import com.aliyuncs.ecs.model.v20140526.CreateSnapshotRequest;
import com.aliyuncs.ecs.model.v20140526.CreateSnapshotResponse;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.exceptions.ServerException;
import com.aliyuncs.profile.DefaultProfile;

/* pom.xml
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-core</artifactId>
    <version>3.0.9</version>
</dependency>
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-java-sdk-ecs</artifactId>
    <version>4.10.1</version>
</dependency>
*/  

public class CreateSnapshotExample {

    private String accessKeyId = "<AccessKey>";
    private String accessSecret = "<AccessSecret>";

    /**
     * Region
     */
    private String regionId = "<RegionId>";

    /**
     * DiskId
     */
    private String diskId = "<DiskId>";

    public void createSnapshot() {
        DefaultProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessSecret);
        IAcsClient client = new DefaultAcsClient(profile);

        CreateSnapshotRequest request = new CreateSnapshotRequest();
        request.setRegionId(regionId);
        request.setDiskId(diskId);
        try {
            CreateSnapshotResponse response = client.getAcsResponse(request);
            logInfo(response.getSnapshotId());
        } catch (ServerException e) {
            logInfo(String.format("Fail. Something with your connection with Aliyun go incorrect. ErrorCode: %s",
                e.getErrCode()));
        } catch (ClientException e) {
            logInfo(String.format("Fail. Business error. ErrorCode: %s, RequestId: %s",
                e.getErrCode(), e.getRequestId()));
        }
    }

    private static void logInfo(String message) {
        System.out.println(message);
    }

    public static void main(String[] args) {
        new CreateSnapshotExample().createSnapshot();
    }
}
```

