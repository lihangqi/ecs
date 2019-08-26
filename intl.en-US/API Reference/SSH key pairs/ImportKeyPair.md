# ImportKeyPair {#doc_api_1006131 .reference}

Imports the public key of an RSA-encrypted key pair that was created by other key pair generators. After the public key is imported, you must store the private key on your own and ensure its confidentiality.

## Description {#description .section}

When you call this operation, note that you can only import a maximum of 500 key pairs in each region.

You can use any of the following encryption methods for your key pair:

-   `RSA`
-   `DSA`
-   `SSH-RSA`
-   `SSH-DSS`
-   `ECDSA`
-   `ssh-rsa-cert-v00@openssh.com`
-   `ssh-dss-cert-v00@openssh.com`
-   `ssh-rsa-cert-v01@openssh.com`
-   `ssh-dss-cert-v01@openssh.com`
-   `ecdsa-sha2-nistp256-cert-v01@openssh.com`
-   `ecdsa-sha2-nistp384-cert-v01@openssh.com`
-   `ecdsa-sha2-nistp521-cert-v01@openssh.com`

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=ImportKeyPair) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|KeyPairName|String|Yes|FinanceJoshuaV24| The name of the key pair. The name must be globally unique. It must be 2 to 128 characters in length. It must start with a letter and cannot start with http:// or https://. It can contain letters, digits, colons \(:\), underscores \(\_\), and hyphens \(-\).

 |
|PublicKeyBody|String|Yes|xxxxxxxxxxxxxx| The public key of the key pair.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region where the key pair resides. You can call [DescribeRegions](~~25609~~) to view the latest list of Alibaba Cloud regions.

 |
|Action|String|No|ImportKeyPair| The operation that you want to perform. Set the value to ImportKeyPair.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|KeyPairFingerPrint|String|89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:d7| The fingerprint of the key pair. MD5 is used based on the public key fingerprint format defined in RFC 4716. For more information, see RFC 4716.

 |
|KeyPairName|String|FinanceJoshauV24| The name of the key pair.

 |
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=ImportKeyPair
&RegionId=cn-qingdao
&PublicKeyBody=xxxxxxxxxxxxxx
&KeyPairName=test
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<ImportKeyPairResponse>
  <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
  <KeyPairName>test</KeyPairName>
  <KeyPairFingerPrint> 89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:d7</KeyPairFingerPrint>
</ImportKeyPairResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E",
	"KeyPairFingerPrint":"89:f0:ba:62:ac:b8:aa:e1:61:5e:fd:81:69:86:6d:6b:f0:c0:5a:d7",
	"KeyPairName":"test"
}
```

## Error codes {#section_bbc_0ph_guw .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|403|QuotaExceed.KeyPair|The key pair quota exceeds.|The error message returned when the number of key pairs reaches the upper limit.|
|400|InvalidPublicKeyBody.Malformed|The PublicKeyBody format is not supported.|The error message returned when the public key format is not supported.|
|400|MissingParameter|The input parameter "PublicKeyBody" that is mandatory for processing this request is not supplied.|The error message returned when the required PublicKeyBody parameter is not specified.|
|400|KeyPair.AlreadyExist|The key pair already exist.|The error message returned when a key pair already exists. Duplicate key pairs cannot be added.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

