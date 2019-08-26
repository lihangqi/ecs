# AuthorizeSecurityGroup {#doc_api_1031569 .reference}

Sets an inbound rule for a security group. This operation permits or declines the inbound traffic from other devices to instances in the security group.

## Description {#description .section}

Inbound traffic describes the traffic received at the destination security group sent from some other source security group.

When you call this operation, note that:

-   A maximum of 100 inbound rules can be configured for one security group.
-   You can set the security group rule to either accept or drop.
-   The priority of a security group rule ranges from 1 to 100. A smaller value indicates a higher priority.
-   When two or more security group rules have the same priority, drop rules will take precedence over accept rules.
-   The source device can belong to a specified range of IP addresses \(SourceCidrIp\) or another security group \(SourceGroupId\).
-   You can determine an inbound rule by specifying one of the following sets of parameters. You cannot determine a security group rule by specifying only one parameter. The AuthorizeSecurityGroup operation fails if the rule being created matches an existing rule.
    -   Grant access permissions to a specified range of IP addresses For a security group of the classic network type, you can set the NicType parameter to Internet or intranet. For a security group of the VPC type, you can only set the NicType parameter to intranet. You can specify the following set of parameters: IpProtocol, PortRange, SourcePortRange \(optional\), NicType, Policy, DestCidrIp, and SourceCidrIp \(optional\).

        ``` {#codeblock_1re_y8p_wc8}
        https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
        &SecurityGroupId=sg-F876FF7BA
        &SourceCidrIp=0.0.0.0/0
        &IpProtocol=tcp
        &PortRange=1/65535
        &NicType=intranet
        &Policy=allow
        &<Common request parameters>
        ```

        -   Grants access permissions to other security groups within the same region. In this case, you must set the NicType parameter to intranet. For mutual access between security groups of the classic network type, you can set the permission for another security group in the same region to access your security group. The security group granted access can belong to your own Alibaba Cloud account, or can belong to another Alibaba Cloud account specified by the SourceGroupOwnerAccount parameter. For mutual access between security groups of the VPC type, you can set the permission for another security group in the same VPC to access your security group. You can specify the following set of parameters: IpProtocol, PortRange, SourcePortRange \(optional\), NicType, Policy, DestCidrIp \(optional\), SourceGroupOwnerAccount, and SourceGroupId.

            ``` {#codeblock_hzj_jkx_ynp}
            https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
            &SecurityGroupId=sg-F876FF7BA
            &SourceGroupId=sg-1651FBB64
            &SourceGroupOwnerAccount=test@aliyun.com
            &IpProtocol=tcp
            &PortRange=1/65535
            &NicType=intranet
            &Policy=Drop
            &<Common request parameters>
            ```

-   For more information about how to set a security group rule, see [Scenarios](~~25475~~), [Typical use cases](~~58746~~), and [Quintet rules](~~97439~~).

## Debugging {#apiExplorer .section}

You can use [API Explorer](https://api.aliyun.com/#product=Ecs&api=AuthorizeSecurityGroup) to perform debugging. API Explorer allows you to perform various operations to simplify API usage. For example, you can retrieve APIs, call APIs, and dynamically generate SDK example code.

## Request parameters {#parameters .section}

|Name|Type|Required|Example|Description|
|----|----|--------|-------|-----------|
|IpProtocol|String|Yes|all| The transport layer protocol. This parameter is case-sensitive. Valid values:

 -   tcp
-   udp
-   icmp
-   gre
-   all: All protocols are supported.

 |
|PortRange|String|Yes|1/200| The range of destination port numbers relevant to the transport layer protocol. Valid values:

 -   When IpProtocol is set to tcp or udp, the port number range is 1 to 65535. Separate the starting port and the ending port with a forward slash \(/\). Correct example: 1/200. Incorrect example: 200/1.
-   When IpProtocol is set to icmp, the port number range is -1/-1, indicating that all values are valid.
-   When IpProtocol is set to gre, the port number range is -1/-1, indicating that all values are valid.
-   When IpProtocol is set to all, the port number range is -1/-1, indicating that all values are valid.

 |
|RegionId|String|Yes|cn-hangzhou| The ID of the region to which the source security group belongs. You can call [DescribeRegions](~~25609~~) to view the latest regions of Alibaba Cloud.

 |
|SecurityGroupId|String|Yes|sg-securitygroupid1| The ID of the destination security group.

 |
|Action|String|No|AuthorizeSecurityGroup| The operation that you want to perform. Set the value to AuthorizeSecurityGroup.

 |
|ClientToken|String|No|123e4567-e89b-12d3-a456-426655440000| A client token. It is used to ensure the idempotency of requests. The value of this parameter is generated by the client and is unique among different requests. The **ClientToken** parameter must be no more than 64 ASCII characters in length. For more information, see [How to ensure idempotency](~~25693~~).

 |
|Description|String|No|FinanceJoshua| The description of the security group rule. The description can be up to 1 to 512 characters in length.

 |
|DestCidrIp|String|No|0.0.0.0/0| The destination CIDR block or IPv4 address. Default value: null.

 |
|Ipv6DestCidrIp|String|No|2001:db8:1234:1a00::XXX| The destination CIDR block or IPv6 address.

 **Note:** Only IP addresses of the VPC type can be specified.

 Default value: null.

 |
|Ipv6SourceCidrIp|String|No|2001:db8:1234:1a00::XXX| The source CIDR block or IPv6 address.

 **Note:** Only IP addresses of the VPC type can be specified.

 Default value: null.

 |
|NicType|String|No|intranet| The NIC type. Valid values:

 -   internet: Internet NIC
-   intranet: intranet NIC

 This parameter must be set to intranet for mutual security group access where the SourceGroupId parameter is specified and the SourceCidrIp parameter is not. Default value: internet.

 |
|Policy|String|No|accept| The access control policy. Valid values:

 -   accept \(default\): grants access.
-   drop: denies access without returning a rejection response.

 |
|Priority|String|No|1| The priority of the security group rule. Valid values: 1 to 100. Default value: 1.

 |
|SourceCidrIp|String|No|0.0.0.0/0| The source CIDR block or IPv4 address. Default value: null.

 |
|SourceGroupId|String|No|sg-securitygroupid2| The ID of the source security group for which you want to set access permissions. Either the SourceGroupId parameter or the SourceCidrIp parameter must be specified.

 If the SourceGroupId parameter is specified, but the SourceCidrIp parameter is not, the NicType parameter must be set to intranet.

 If both the SourceGroupId and SourceCidrIp parameters are set, the SourceCidrIp parameter will take precedence.

 |
|SourceGroupOwnerAccount|String|No|test@aliyun.com| The Alibaba Cloud account of the source security group when you set security group rules for different accounts.

 -   If neither the SourceGroupOwnerAccount parameter nor the SourceGroupOwnerId parameter is specified, the access permissions are granted to other security groups.
-   If the SourceCidrIp parameter is specified, the SourceGroupOwnerAccount parameter will be ignored.

 |
|SourceGroupOwnerId|Long|No|155780923770| The ID of the Alibaba account that owns the source security group. This parameter is used to grant access for the current security group to receive traffic from other Alibaba Cloud accounts.

 -   If neither the SourceGroupOwnerId parameter nor the SourceGroupOwnerAccount parameter is specified, the access permissions are granted to other security groups.
-   If the SourceCidrIp parameter is specified, the SourceGroupOwnerId parameter will be ignored.

 |
|SourcePortRange|String|No|1/200| The range of source port numbers relevant to the transport layer protocol. Valid values:

 -   When IpProtocol is set to tcp or udp, the port number range is 1 to 65535. Separate the starting port and the ending port with a forward slash \(/\). Correct example: 1/200. Incorrect example: 200/1.
-   When IpProtocol is set to icmp, the port number range is -1/-1, indicating that all values are valid.
-   When IpProtocol is set to gre, the port number range is -1/-1, indicating that all values are valid.
-   When IpProtocol is set to all, the port number range is -1/-1, indicating that all values are valid.

 |

## Response parameters {#resultMapping .section}

|Name|Type|Example|Description|
|----|----|-------|-----------|
|RequestId|String|473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E| The ID of the request.

 |

## Examples {#demo .section}

Sample requests

``` {#request_demo}
https://ecs.aliyuncs.com/?Action=AuthorizeSecurityGroup
&SecurityGroupId=sg-F876FF7BA
&SourceCidrIp=0.0.0.0/0
&IpProtocol=tcp
&PortRange=1/65535
&NicType=intranet
&Policy=accept
&<Common request parameters>
```

Successful response examples

`XML` format

``` {#xml_return_success_demo}
<AuthorizeSecurityGroupResponse>
  <RequestId>CEF72CEB-54B6-4AE8-B225-F876FF7BA984</RequestId> 
</AuthorizeSecurityGroupResponse>
```

`JSON` format

``` {#json_return_success_demo}
{
	"RequestId":"CEF72CEB-54B6-4AE8-B225-F876FF7BA984"
}
```

## Error codes {#section_vot_fuo_ktp .section}

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|The error message returned when the specified security group does not exist under this account. Check whether the security group ID is correct.|
|400|OperationDenied|The specified IpProtocol does not exist or IpProtocol and PortRange do not match.|The error message returned when the specified IP protocol does not exist or does not match the port range.|
|400|InvalidIpProtocol.Malformed|The specified parameter PortRange is not valid.|The error message returned when the specified value of the IpProtocol parameter is invalid.|
|403|MissingParameter|The input parameter SourceGroupId or SourceCidrIp cannot be both blank.|The error message returned when neither the SourceGroupId parameter nor the SourceCidrIp parameter is specified.|
|400|InvalidPolicy.Malformed|The specified parameter Policy is not valid.|The error message returned when the specified value of the Policy parameter is invalid.|
|400|InvalidNicType.Mismatch|Specified nic type conflicts with the authorization record.|The error message returned when the specified NIC type does not exist.|
|403|InvalidParamter.Conflict|The specified SecurityGroupId should be different from the SourceGroupId.|The error message returned when the specified security group is the same as the source security group.|
|400|InvalidPriority.Malformed|The parameter Priority is invalid.|The error message returned when the specified value of the Priority parameter is invalid.|
|400|InvalidPriority.ValueNotSupported|The parameter Priority is invalid.|The error message returned when the specified value of the Priority parameter is invalid.|
|403|InvalidNetworkType.Conflict|The specified SecurityGroup network type should be same with SourceGroup network type \(vpc or classic\).|The error message returned when the network type of the specified security group is different from that of the source group.|
|400|InvalidSecurityGroupDiscription.Malformed|The specified security group rule description is not valid.|The error message returned when the description of the specified security group is invalid.|
|400|InvalidSecurityGroup.InvalidNetworkType|The specified security group network type is not support this operation, please check the security group network types. For VPC security groups, ClassicLink must be enabled.|The error message returned when the network types of the source security group and the destination security group are different.|
|400|MissingParameter.Source|Either SourceCidrIp or SourceGroupId must be specified.|The error message returned when neither the SourceGroupId parameter nor the SourceCidrIp parameter is specified.|
|400|InvalidParam.PortRange|Please specify the PortRange or SourcePortRange in integer, less than 65535, and separate the range with ? /?.|The error message returned when the specified value of the PortRange or SourcePortRange parameter is invalid.|
|400|InvalidIpProtocol.ValueNotSupported|The parameter IpProtocol must be specified with case insensitive TCP, UDP, ICMP, GRE or All.|The error message returned when the IpProtocol parameter is not set to tcp, udp, icmp, gre, or all.|
|400|InvalidParam.SourceIp|%s|The error message returned when the specified source IP address is invalid.|
|400|InvalidParam.DestIp|%s|The error message returned when the specified destination IP address is invalid.|
|400|InvalidParam.Ipv6DestCidrIp|%s|The error message returned when the destination IPv6 address is invalid.|
|400|InvalidParam.Ipv6SourceCidrIp|%s|The error message returned when the source IPv6 address is invalid.|
|400|InvalidParam.Ipv4ProtocolConflictWithIpv6Address|%s|The error message returned when IPv4 addresses conflict with IPv6 addresses.|
|400|InvalidParam.Ipv6ProtocolConflictWithIpv4Address|%s|The error message returned when IPv6 addresses conflict with IPv4 addresses.|
|400|ILLEGAL\_IPV6\_CIDR|%s|The error message returned when the specified IPv6 CIDR block is invalid.|

[View error codes](https://error-center.aliyun.com/status/product/Ecs)

