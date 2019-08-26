# ECS API快速入门 {#EcsApiGettingStarted .concept}

本文以CreateSnapshot为例，为您演示如何通过阿里云CLI、OpenAPI Explorer和阿里云SDK等开发者工具调用ECS API。

## 使用阿里云CLI调用API示例 {#section_rn1_hys_lgb .section}

**前提条件**

本文调用API的工具为阿里云CLI，请确保您已[安装](https://www.alibabacloud.com/help/doc-detail/90765.htm)和[配置](https://www.alibabacloud.com/help/doc-detail/90766.htm)了阿里云CLI。

**操作步骤**

本示例通过阿里云CLI调用API，完成创建快照（[CreateSnapshot](intl.zh-CN/API参考/快照/CreateSnapshot.md#)）的任务。调用API前，请根据API文档了解使用说明，并查询必需的请求参数。调用API报错时，您可以在相应API文档中获取排查建议。

1.  获取实例ID。
    -   如果您已远程连接到ECS实例，可以通过[实例元数据](../../../../../intl.zh-CN/用户指南/实例/实例自定义数据和元数据/实例元数据.md#)获取实例ID：

        ```
        curl http://100.100.100.200/2016-01-01/meta-data/instance-id
        ```

    -   在本地计算机中，您可以通过[DescribeInstances](intl.zh-CN/API参考/实例/DescribeInstances.md#)获取实例ID：

        ```
        aliyun ecs DescribeInstances --output cols=InstanceId,InstanceName
        ```

2.  使用[DescribeDisks](intl.zh-CN/API参考/磁盘/DescribeDisks.md#)筛选磁盘ID：

    ```
    aliyun ecs DescribeDisks --RegionId cn-hangzhou --InstanceId i-bp1afnc98r8k69XXXXXX --output cols=DiskId
    ```

3.  使用[CreateSnapshot](intl.zh-CN/API参考/快照/CreateSnapshot.md#)根据磁盘ID创建快照：

    ```
    aliyun ecs CreateSnapshot --DiskId d-bp19pjyf12hebpXXXXXX
    ```

    返回以下信息时，表示已成功发起创建任务：

    ```
    {"RequestId":"16B856F6-EFFB-4397-8A8A-CB73FAXXXXXX","SnapshotId":"s-bp1afnc98r8kjhXXXXXX"}
    ```

4.  使用[DescribeSnapshots](intl.zh-CN/API参考/快照/DescribeSnapshots.md#)查询快照创建状态。当`"SnapshotId"="s-bp1afnc98r8kjhXXXXXX"`和`"Status":"accomplished"`同时出现，表示快照已成功创建：

    ```
    aliyun ecs DescribeSnapshots --RegionId cn-hangzhou --InstanceId i-bp1afnc98r8k69XXXXXX --output cols=SnapshotId,Status
    ```


## 使用OpenAPI Explorer调用API示例 {#section_lt3_s4g_mgb .section}

本示例通过[阿里云OpenAPI Explorer](https://api.aliyun.com/new#/?product=Ecs)，完成创建快照（[CreateSnapshot](intl.zh-CN/API参考/快照/CreateSnapshot.md#)）的任务。更多有关OpenAPI Explorer的详情，请参见[什么是OpenAPI Explorer](https://www.alibabacloud.com/help/doc-detail/74407.htm)。调用[CreateSnapshot](intl.zh-CN/API参考/快照/CreateSnapshot.md#)前，请根据API文档了解使用说明，并查询必需的请求参数。

1.  通过[DescribeInstances](https://api.aliyun.com/new#/?product=Ecs&api=DescribeInstances)获取实例ID和磁盘ID。
2.  通过[CreateSnapshot](https://api.aliyun.com/new#/?product=Ecs&api=CreateSnapshot)根据磁盘ID创建快照。
3.  使用[DescribeSnapshots](https://api.aliyun.com/new#/?product=Ecs&api=DescribeSnapshots)查询快照创建状态。当`"SnapshotId"="s-bp1afnc98r8kjhXXXXXX"`和`"Status":"accomplished"`同时出现，表示快照已成功创建。

## 使用Java SDK调用API示例 {#section_s1c_2qg_mgb .section}

本示例通过[Java SDK](https://github.com/aliyun)，完成创建快照（[CreateSnapshot](intl.zh-CN/API参考/快照/CreateSnapshot.md#)）的任务。关于如何配置ECS SDK，请参见[安装新版Java SDK](../../../../../intl.zh-CN/SDK 参考/安装新版 Java SDK.md#)。

**说明：** 以下SDK示例中的`<AccessKey>`（您的AccessKeyId）、`<AccessSecret>`（您的AccessKeySecret）、`<RegionId>`（实例所在的地域ID）和`<DiskId>`（磁盘ID）需要根据实际情况自行填写。更多详情，请参见[创建AccessKey](../../../../../intl.zh-CN/通用参考/创建AccessKey.md#)和[地域与可用区](../../../../../intl.zh-CN/通用参考/地域和可用区.md#)。

```
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
     * 地域
     */
    private String regionId = "<RegionId>";

    /**
     * 磁盘id
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

