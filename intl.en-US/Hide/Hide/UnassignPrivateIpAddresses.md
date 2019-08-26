# UnassignPrivateIpAddresses {#reference_lnv_bdd_n2b .reference}

Deletes one or more secondary private IP addresses from an ENI.

## Description {#section_phk_ddd_n2b .section}

-   This operation only supports ENIs in the ****`Available` or ****`InUse` status.
-   When operating on a primary ENI, the attached instance must be in the ****`Running` or ****`Stopped` status.

## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The operation that you want to perform. Value: UnassignPrivateIpAddresses.|
|NetworkInterfaceId|String|Yes|ENI ID.|
|PrivateIpAddress.N|Array|Yes|One or more secondary private IP addresses to delete from an ENI. Value range of `N`:-   ENI is in the ****`Available` status: \[1, 10\].
-   ENI is in the ****`InUse` status: Subject to instance type restrictions.

|

## Response parameters {#ResponseParameter .section}

## Examples { .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=UnassignPrivateIpAddresses
&NetworkInterfaceId=eni-m5e709m1ytxc4wx7wXXX
&PrivateIpAddress. 1=192.168.0.1
&PrivateIpAddress. 2=192.168.10.1
&<Common Request Parameters>
```

**Response example** 

**XML format**

```
<UnassignPrivateIpAddressesResponse>
    <RequestId>04F0F334-1335-436C-A1D7-6C044FE70008</RequestId>
</UnassignPrivateIpAddressesResponse>
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

