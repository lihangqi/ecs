# ModifyInstanceAttribute {#ModifyInstanceAttribute .reference}

Modifies the information such as the name, password, host name, and description of an instance.

## Description {#section_ufy_4pt_xdb .section}

When you call this interface, consider the following:

-   You cannot reset the password for an instance when it is in the `Starting` status.
-   If the specified instance is [locked](reseller.en-US/API Reference/Appendix/API behavior when an instance is locked for security reasons.md#), and the `OperationLocks` of the instance indicates `"LockReason" : "security"`, you cannot reset its password.
-   The new password takes effect only after the instance is [restarted](../reseller.en-US/Instances/Manage instances/Restart an instance.md#) in the console or by calling the interface [RebootInstance](reseller.en-US/API Reference/Instances/RebootInstance.md#). 
-   When an instance is in the **Stopped** status and is not limited to pass a [user data](../reseller.en-US/Instances/Manage instances/User-defined data/User data.md) script, you can modify its user data.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: ModifyInstanceAttribute.|
|InstanceId|String|Yes|The specified instance ID.|
|InstanceName|String|No|The name of the instance.The name is a string of 2 to 128 characters. It must begin with an English or a Chinese character. It can contain A-Z, a-z, Chinese characters, numbers, periods \(.\), colons \(:\), underscores \(\_\), and hyphens \(-\).|
|Description|String|No|The description of the instance is null by default. It cannot begin with http:// or https://.|
|Password|String|No|Resets the administrative password of the instance. The password can be \[8, 30\] characters in length. It must contain uppercase letters, lowercase letters, and numbers. The following special characters are allowed: \(\)\`~! @\#$%^&amp;\*-+=|\{\}\[\]:;‘&lt;\>,.? /. A slash \(/\) cannot be the first character of Windows instances administrative password.|
|HostName|String|No|Host name of the instance.-   It cannot start or end with a period \(.\) or a hyphen \(-\) and it cannot have two or more consecutive periods \(.\) or hyphens \(-\).
-   For Windows: The host name can be \[2, 15\] characters in length. It can contain A-Z, a-z, numbers, periods \(.\), and hyphens \(-\). It cannot only contain numbers.
-   For other operating systems: The host name can be \[2, 64\] characters in length. It can be segments separated by periods \(.\). It can contain A-Z, a-z, numbers, and hyphens \(-\).

|
|UserData|String|No|The user-defined data of your ECS instance. The size of your UserData must be less than 16 KB before the Base64 encodement. Refrain from entering confidential information, such as SSH key pair and AccessKey, in your request. If you do so, make sure the confidential information is encrypted before Base64 encoding. Also, do not forget to decrypt the information after it passes into your ECS instance.|
|CreditSpecification|String|No| Modifies the running mode of an unlimited credit enabled t5 instance. Optional values:

 -   Standard: The standard running mode. For more information, see [t5 standard instances](../reseller.en-US/Instances/Instance type families/Burstable performance instances/t5 standard instances.md#).
-   Unlimited: The unlimited running mode. For more information, see [t5 unlimited instances](../reseller.en-US/Instances/Instance type families/Burstable performance instances/t5 unlimited instances.md#).

 Default value: null.

 |
|DeletionProtection|Boolean|No|Whether an instance can be released manually through the console or API \([DeleteInstance](reseller.en-US/API Reference/Instances/DeleteInstance.md#)\).-   true: Enable deletion protection.
-   false: Disable deletion protection.

**Note:** This attribute applies to the Pay-As-You-Go instances. However, it can only restrict the manual release operation, not the release operation by Alibaba Cloud.

|

## Response parameters {#ResponseParameter .section}

All are common response parameters. For more information, see [Common parameters](reseller.en-US/API Reference/Getting started/Common parameters.md#commonResponseParameters).

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=ModifyInstanceAttribute
&InstanceId=i-instance1
&Password=pwd
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<ModifyInstanceAttributeResponse>
    <RequestId>473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E</RequestId>
</ModifyInstanceAttributeResponse>
```

 **JSON format** 

```
{
    "RequestId": "473469C7-AA6F-4DC5-B3DB-A3DC0DE3C83E"
}
```

## Error codes {#ErrorCode .section}

All are common error codes. For more information, see [Common error codes](../reseller.en-US/API Reference/Getting started/Response results.md#commonErrorCodes).

|Error code|Error message|HTTP status code|Meaning|
|:---------|:------------|:---------------|:------|
|InvalidDescription.Malformed|The specified parameter “Description” is not valid.|400|The specified `Description` is invalid.|
|InvalidDescription.Malformed|The specified destination image description is wrongly formed.|400|The specified `Description` is invalid.|
|InvalidHostPassword.Malformed|The specified parameter “Password” is not valid.|400|The specified `Password` is invalid.|
|InvalidInstanceName.Malformed|The specified parameter “InstanceName” is not valid.|400|The specified `InstanceName` is invalid.|
|InvalidHostName.Malformed|The specified parameter “HostName” is not valid.|400|The specified `HostName` is invalid.|
|InvalidPassword.Malformed|The specified parameter “Password” is not valid.|400|The specified `Password` is invalid.|
|InvalidUserData.SizeExceeded|The specified parameter “UserData” exceeds the size.|400|The size of your `UserData` must be less than 16 KB.|
|InvalidUserData.NotSupported|The specified parameter “UserData” only support the vpc and IoOptimized Instance.|400|You can only specify `UserData` for a VPC instance or an I/O optimized instance.|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|You cannot reset the password for an instance when it is in Deleted or Starting status.|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|Your instance has been locked.|
|OperationDenied|The Specified operation is denied as your instance is locked for security reasons.|403|Your instance has been locked.|
|OperationDenied|The current status of the resource does not support this operation.|403|You cannot reset the password for an instance when it is in Deleted or Starting status.|
|HOSTNAME\_ILLEGAL|hostname is not valid.|404|The specified `HostName` is invalid.|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|The specified `InstanceId` does not exist.|
|InvalidSecurityGroupId.NotFound|The specified SecurityGroupId does not exist.|404|The specified `SecurityGroupId` does not exist.|

