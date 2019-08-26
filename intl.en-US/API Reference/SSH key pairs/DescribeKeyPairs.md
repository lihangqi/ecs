# DescribeKeyPairs {#doc_api_1006038 .reference}

Queries one or more key pairs.

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=DescribeKeyPairs) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|RegionId|String|Yes|cn-hangzhou| The ID of the region where a key pair resides. You can call [DescribeRegions](~~25609~~) to view the latest list of Alibaba Cloud regions.

 |
|Action|String|No|DescribeKeyPairs| The operation that you want to perform. Set the value to DescribeKeyPairs.

 |
|KeyPairFingerPrint|String|No|XXXXXXXXXX| The fingerprint of the key pair. The message-digest algorithm 5 \(MD5\) is used based on the public key fingerprint format defined in RFC 4716. For more information, see [RFC 4716](https://tools.ietf.org/html/rfc4716).

 |
|KeyPairName|String|No|\*Finance\*| The name of the key pair. The asterisk \(\*\) symbol can be used as a wild card in regular expressions to query key pairs by fuzzy match. Sample patterns:

 -   `` \*SshKey: queries key pair names ending with SshKey, including SshKey.
-   ``SshKey \*: queries key pair names starting with SshKey, including SshKey.
-   ``\* SshKey \*: queries key pair names that contain SshKey.
-   ``SshKey: queries SshKey by exact match.

 |
|PageNumber|Integer|No|1| The page number to be queried in the SSH key pair list. Starting value: 1.

 Default value: 1.

 |
|PageSize|Integer|No|10| The number of entries per page. Maximum Value: 50

 Default value: 10

 |
|ResourceGroupId|String|No|rg-resourcegroupid1| The ID of the resource group that hosts the key pair.

 |
|Tag.N.Key|String|No|FinanceDept| The tag key of the key pair. Valid values of N: 1 to 20. It cannot be an empty string. It must be no more than 64 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.Value|String|No|FinanceDept.Joshua| The tag value of the key pair. Valid values of N: 1 to 20. It can be an empty string. It can be a maximum of 64 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|KeyPairs| | | A set of key pairs.

 |
|└KeyPairFingerPrint|String|xxxxxxxxxx| The fingerprint of the key pair.

 |
|└KeyPairName|String|FinanceJoshuaV27| The name of the key pair.

 |
|└ResourceGroupId|String|rg-resourcegroupid1| The ID of the resource group.

 |
|└Tags| | | The tags of the key pair.

 |
|└TagKey|String|FinanceDept| The tag key of the key pair.

 |
|└TagValue|String|FinanceDept.Joshua| The tag value of the key pair.

 |
|PageNumber|Integer|1| The current page number.

 |
|PageSize|Integer|10| The number of entries per page.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request. This parameter is returned regardless of whether the operation is successful.

 |
|TotalCount|Integer|1| The total number of key pairs.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=DescribeKeyPairs
&RegionId=cn-qingdao
&KeyPairFingerPrint=xxxxxxxxxx
&KeyPairName=test
&PageNumber=1
&PageSize=20
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<DescribeKeyPairsResponse>
  <PageNumber>1</PageNumber>
  <PageSize>2</PageSize>
  <TotalCount>1</TotalCount>
  <KeyPairs>
    <KeyPair>
      <KeyPairName>test</KeyPairName>
      <KeyPairFingerPrint>xxxxxxxxxx</KeyPairFingerPrint>
    </KeyPair>
  </KeyPairs>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DescribeKeyPairsResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"PageNumber":1,
	"TotalCount":1,
	"KeyPairs": {
		"KeyPair":{
			{
				"KeyPairFingerPrint": "xxxxxxxxxx",
				"KeyPairName": "test"
			}
		]
	},
	"PageSize":2,
	"RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#section_4wu_aa8_gxi .section}

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

