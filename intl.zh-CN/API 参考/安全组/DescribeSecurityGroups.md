# DescribeSecurityGroups {#DescribeSecurityGroups .reference}

查询您创建的安全组的基本信息，例如安全组ID和安全组描述等。返回列表按照安全组ID降序排列。

## 请求参数 {#RequestParameter .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：DescribeSecurityGroups|
|RegionId|String|是|地域ID。您可以调用[DescribeRegions](../intl.zh-CN/API 参考/地域/DescribeRegions.md#)查看最新的阿里云地域列表。|
|VpcId|String|否|安全组所在的专有网络ID。|
|SecurityGroupIds|Array|否|安全组ID列表。一次最多支持100个安全组ID，ID之间用半角逗号（,）隔开，格式为JSON数组，示例\["sg-id1", "sg-id2", "sg-id2",....\]。|
|Tag.n.Key|String|否|安全组的标签键。n的取值范围：\[1, 20\]。一旦传入该值，则不允许为空字符串。最多支持64个字符，不能以aliyun、acs:、http://或者https://开头。|
|Tag.n.Value|String|否|安全组的标签值。n的取值范围：\[1, 20\]。一旦传入该值，可以为空字符串。最多支持128个字符，不能以aliyun、acs:、http://或者https://开头。|
|PageNumber|Integer|否|安全组列表的页码。起始值：1默认值：1

|
|PageSize|Integer|否|分页查询时设置的每页行数。最大值：50默认值：10

|
|DryRun|Boolean|否|是否只预检此次请求。-   true：发送检查请求，不会查询资源状况。检查项包括AccessKey是否有效、RAM用户的授权情况和是否填写了必需参数。如果检查不通过，则返回对应错误。如果检查通过，会返回错误码`DryRunOperation`。
-   false：发送正常请求，通过检查后返回2XX HTTP状态码并直接查询资源状况。

默认值：false

|

## 返回参数 {#ResponseParameter .section}

|名称|类型|描述|
|:-|:-|:-|
|TotalCount|Integer|安全组的总数|
|PageNumber|Integer|当前页码|
|PageSize|Integer|每页行数|
|RegionId|String|安全组所属地域ID|
|SecurityGroups|[SecurityGroupItemType](intl.zh-CN/API 参考/数据类型/SecurityGroupItemType.md#)|安全组信息集合|

## 示例 { .section}

**请求示例**

```
https://ecs.aliyuncs.com/?Action=DescribeSecurityGroups
&RegionId=cn-hangzhou
&<公共请求参数>
```

**返回示例**

**XML格式**

```
<DescribeSecurityGroupsResponse>
    <RequestId>94D38899-626D-434A-891F-7E1F77A81525</RequestId>
    <TotalCount>4</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <RegionId>cn-hangzhou</RegionId>
    <SecurityGroups>
        <SecurityGroup>
            <SecurityGroupId>sg-F876FF7BA</SecurityGroupId>
            <Description>Test</Description>
        </SecurityGroup>
        <SecurityGroup>
            <SecurityGroupId>sg-086FFC27A</SecurityGroupId>
            <Description>test00212</Description>
        </SecurityGroup>
        <SecurityGroup>
            <SecurityGroupId>sg-BA4B7975B</SecurityGroupId>
            <Description>cn-hangzhou test group</Description>
        </SecurityGroup>
        <SecurityGroup>
            <SecurityGroupId>sg-35F20777C</SecurityGroupId>
            <Description>cn-hangzhou test group</Description>
        </SecurityGroup>
    </SecurityGroups>
</DescribeSecurityGroupsResponse>
```

 **JSON格式**

```
{
    "RequestId": "94D38899-626D-434A-891F-7E1F77A81525",
    "TotalCount": 4,
    "PageSize": "10",
    "RegionId": "cn-hangzhou",
    "PageNumber": "1",
    "SecurityGroups": {
        "SecurityGroup": [{
            "SecurityGroupId": "sg-F876FF7BA",
            "Description": "TestByXcf"
        },
        {
            "SecurityGroupId": "sg-086FFC27A",
            "Description": "test00212"
        },
        {
            "SecurityGroupId": "sg-BA4B7975B",
            "Description": "cn-hangzhou test group"
        },
        {
            "SecurityGroupId": "sg-35F20777C",
            "Description": "cn-hangzhou test group"
        }]
    }
}
```

## 错误码 {#ErrorCode .section}

全是公共错误码。更多错误码，请访问[API错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

