# DescribeKeyPairs {#DescribeKeyPairs .reference}

查询一个或多个密钥对。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeKeyPairs|
|RegionId|String|是|密钥对所在的地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|KeyPairFingerPrint|String|否|密钥对的指纹。根据RFC4716定义的公钥指纹格式，采用MD5信息摘要算法。更多详情，请参阅[RFC4716](http://tools.ietf.org/html/rfc4716)。|
|KeyPairName|String|否|密钥对名称。支持正则表达式模糊搜索，使用`*`匹配子表达式，示例：-   `*SshKey`：查询以*SshKey*结尾的密钥对名称，包括*SshKey*。
-   `SshKey*`：查询以*SshKey*开头的密钥对名称，包括*SshKey*。
-   `*SshKey*`：查询名称中间有*SshKey*的密钥对，包括*SshKey*。
-   `SshKey`：精确匹配*SshKey*。

|
|PageNumber|Integer|否|密钥对列表的页码。起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数。最大值：50默认值：10

|
|Tag.n.Key|String|否|密钥对的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|密钥对的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|密钥对的总数。|
|PageNumber|Integer|当前页码。|
|PageSize|Integer|每页行数。|
|RegionId|String|密钥对所属地域ID。|
|KeyPairs|[KeyPairItemType](intl.zh-CN/API 参考/数据类型/KeyPairItemType.md#)|密钥对信息集合。|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=DescribeKeyPairs
&RegionId=cn-qingdao
&KeyPairFingerPrint=xxxxxxxxxx
&KeyPairName=test
&PageNumber=1
&PageSize=20
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<DescribeKeyPairsResponse>
    <PageNumber>1</PageNumber>
    <PageSize>2</PageSize>
    <TotalCount>1</TotalCount>
    <KeyPairs>
        <KeyPair>
            <KeyPairName>test</KeyPairName >
            <KeyPairFingerPrint>xxxxxxxxxx</KeyPairFingerPrint>
        </KeyPair>
    </KeyPairs>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</DescribeKeyPairsResponse>
```

**JSON格式**

```
{
    "PageNumber": 1,
    "PageSize": 2,
    "TotalCount": 1,
    "KeyPairs": {
        "KeyPair":[{
            "KeyPairName": "test",
            "KeyPairFingerPrint": "xxxxxxxxxx"
        }]
    }
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP状态码|说明|
|:---|:---|:------|:-|
|MissingParameter|The input parameter “RegionId” that is mandatory for processing this request is not supplied.|400|您必须指定`RegionId`参数。|
|InvalidParameter|The specified parameter “PageNumber” is not valid.|400|指定的参数`PageNumber`不合法。|
|InvalidParameter|The specified parameter “PageSize” is not valid.|400|指定的参数`PageSize`不合法。|

