# CreateKeyPair {#doc_api_999670 .reference}

Creates an SSH key pair. The system stores the public key and returns the unencrypted private key. The private key is encoded by using PEM and is in the PKCS\#8 format. You must store the private key on your own and ensure its confidentiality.

## Description {#description .section}

In addition to calling CreateKeyPair, you can create a key pair through other key pair generators and call [ImportKeyPair](~~25542~~) to upload the key pair to a region.

You can have up to 500 key pairs in each Alibaba Cloud region. For more information, see [SSH key pair](~~51792~~).

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=CreateKeyPair) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|KeyPairName|String|Yes|FinanceJoshuaV23| The name of the key pair. It must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\). The name must be globally unique and supports all character set encoding formats.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the key pair resides. You can call [DescribeRegions](~~25609~~) to view the latest list of Alibaba Cloud regions.

 |
|Action|String|No|CreateKeyPair| The operation that you want to perform. Set the value to CreateKeyPair.

 |
|ResourceGroupId|String|No|rg-resourcegroupid1| The ID of the resource group to which the tag belongs.

 |
|Tag.N.Key|String|No|FinanceDept| The tag key of the key pair. Valid values of N: 1 to 20. It cannot be an empty string. It can be a maximum of 64 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |
|Tag.N.Value|String|No|FinanceDept.Joshua| The tag value of the key pair. Valid values of N: 1 to 20. It can be an empty string. It can be a maximum of 128 characters in length. It cannot start with aliyun or acs:. It cannot contain http:// or https://.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|KeyPairFingerPrint|String|89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:d7| The fingerprint of the key pair. MD5 is used based on the public key fingerprint format defined in RFC 4716. For more information, see [RFC 4716](https://tools.ietf.org/html/rfc4716).

 |
|KeyPairName|String|FinanceJoshuaV23| The name of the key pair.

 |
|PrivateKeyBody|String|xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx| The private key of the key pair. The private key is encoded by using PEM and is in PKCS\#8 format. For more details, see OpenSSL PKCS \#8.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=CreateKeyPair
&RegionId=cn-qingdao
&KeyPairName=test
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<CreateKeyPairResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
  <KeyPairName>test</KeyPairName>
  <KeyPairFingerPrint>89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:d7</KeyPairFingerPrint>
  <PrivateKeyBody>xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</PrivateKeyBody>
</CreateKeyPairResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"PrivateKeyBody":"xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
	"KeyPairFingerPrint":"89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:d7",
	"KeyPairName":"test"
}
```

## Error codes {#section_ysp_8j5_lu7 .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|QuotaExceed.KeyPair|The key pair quota exceeds.|The error message returned when the number of key pairs reaches the upper limit.|
|400|KeyPair.AlreadyExist|The key pair already exist.|The error message returned when a key pair already exists. Duplicate key pairs cannot be added.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

