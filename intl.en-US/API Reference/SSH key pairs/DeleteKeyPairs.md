# DeleteKeyPairs {#doc_api_999672 .reference}

Deletes one or multiple SSH key pairs. The entry of a deleted SSH key pair is removed from the database. However, the instances bound with the SSH key pair can still use it.

## Description {#description .section}

When you call this operation, note that:

-   After you delete an SSH key pair, this pair cannot be returned in response to [DescribeKeyPairs](~~51773~~).
-   When you call [DescribeInstances](~~25506~~) to query instance information, the SSH key pair name \(KeyPairNames\) is still returned, but without any other information.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DeleteKeyPairs) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|KeyPairNames|String|Yes|\["key-xxxxxxxxx", "key-yyyyyyyyy", … "key-zzzzzzzzz"\]| The SSH key pair names. The value can be a JSON array consisting of up to 100 SSH key pairs. Multiple key pairs must be separated by commas \(,\).

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where a SSH key pair resides. You can call [DescribeRegions](~~25609~~) to view the latest list of Alibaba Cloud regions.

 |
|Action|String|No|DeleteKeyPairs| The operation that you want to perform. Set the value to DeleteKeyPairs.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DeleteKeyPairs
&RegionId=cn-qingdao
&KeyPairNames=test
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DeleteKeyPairsResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DeleteKeyPairsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_5mk_8w7_63w .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|MissingParameter|The input parameter "KeyPairNames" that is mandatory for processing this request is not supplied.|The error message returned when the required KeyPairNames parameter is not specified.|
|400|InvalidKeyPairNames. ValueNotSupported|The specified parameter "KeyPairNames" is not valid.|The error message returned when the KeyPairNames parameter is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

