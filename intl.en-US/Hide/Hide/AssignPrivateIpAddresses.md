# AssignPrivateIpAddresses {#reference_hlp_yrc_n2b .reference}

Allocates one or more secondary private IP addresses to an ENI. Particularly, you can specify the CIDR private IP addresses that are available in the VSwitch. Alternatively, set the number of private IP addresses you want to allocate, and ECS automatically allocates the IP addresses for you.

## Description {#section_eq4_qvc_n2b .section}

-   This operation only supports ENIs in the **Available**`Available` or **InUse**`InUse` status.
-   When operating on a primary ENI, the attached instance must be in the **Running**`Running` or **Stopped**`Stopped` status.
-   When the ENI is **Available**`Available`, you can allocate up to 10 secondary private IP addresses to the ENI. However, once the ENI is used and attached an instance, the maximum number of private IP addresses is subject to the instance type limits. For more information, see [instance type families](../reseller.en-US/Product Introduction/Instance type families.md#).

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Value: AssignPrivateIpAddresses.|
|NetworkInterfaceId|String|Yes|ENI ID.|
|PrivateIpAddress.N|Array|No|Select one or more secondary private IP addresses from the CIDR block of the VSwitch. Value range of `N`:-   When ENI is in the **Available**`Available` status: \[1, 10\].
-   When ENI is in the **InUse**`InUse` status: Subject to instance type restrictions. For more information, see [instance type families](../reseller.en-US/Product Introduction/Instance type families.md#).

You cannot specify the parameters `PrivateIpAddress.N` and `SecondaryPrivateIpAddressCount` at the same time.|
|SecondaryPrivateIpAddressCount|Integer|No|ECS can automatically create IP addresses for you. You must specify the number of private IP addresses you want to create.|

## Response parameters {#ResponseParameter .section}

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=AssignPrivateIpAddresses
&NetworkInterfaceId=eni-m5e709m1ytxc4wx7wXXX
&PrivateIpAddress. 1=192.168.0.1
&PrivateIpAddress. 2=192.168.10.1
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<AssignPrivateIpAddressesResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE70008</RequestId>
</AssignPrivateIpAddressesResponse>
```

**JSON format** 

```
{
    "RequestId": "04F0F334-1335-436C-A1D7-6C044FE70008"
}
```

## Error codes {#ErrorCode .section}

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|InValidParameter|the parameter\(s\) “\{0\}” provided is\(are\) invalid.|400|The specified parameter is invalid.|
|MissingParameter|The input parameter “\{0\}” that is mandatory for processing this request is not supplied.|400|You must specify this required parameters.|
|InvalidOperation.InvalidEniState|The operation is not allowed in the current ENI state. Expecting status is “\{0\}” while current status is “\{1\}”.|400|This operation only supports ENIs in the ****`Available` or ****`InUse` status.|
|InvalidIp.IpUnassigned|The specified IP “\{0\}” is not assigned on this ENI.|403|The specified secondary private IP address was not assigned to this ENI.|
|InvalidVSwitchId.IpInvalid|The specified IpAddress “\{0\}” is not valid in VSwitch CIDR block “\{1\}”.|403|You must select secondary IP addresses from the VSwitch's CIDR block.|
|Operation.Conflict|ecs task is conflicted.|403|The specified ENI is processing another task. Please try again later.|
|InvalidEniId.NotFound|The specified EniId “\{0\}” is not found.|404|The specified `NetworkInterfaceId` does not exist.|
|InvalidVSwitchId.NotFound|The specified VSwitchId “\{0\}” is not found.|404|The specified VSwitch does not exist.|

