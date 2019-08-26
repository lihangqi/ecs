# ReactivateInstances {#ReactivateInstances .reference}

Reactivates a Pay-As-You-Go ECS instance that is suspended because of overdue payments and in the Stopped status.

## Description {#section_gvn_mmx_rfb .section}

When you call this interface, consider the following:

-   The instance must be in the **Expired** \(`Stopped`\) or **Overdue and Being Recycled** \(`Stopped`\) status.

-   You must pay the bills and reactivate the instance within 15 days after the instance is suspended because of overdue payments. Otherwise, the instance is released and the data cannot be restored. If you cannot reactivate a VPC-connected instance, try again later or open a ticket to contact Alibaba Cloud.

-   For more information about the service restrictions, see [Reactivate instances](../reseller.en-US/User Guide/Instances/Reactivate an instance.md#) in the User Guide manual.

-   If the operation is successful, the status of the instance becomes **Starting** \(`Starting`\).

-   The `OperationLocks` of the [locked](../reseller.en-US/API Reference/Appendix/API behavior when an instance is locked for security reasons.md#) instance cannot be `"LockReason" : "security"`.


## Request parameters {#RequestParameter .section}

|Name|Type|Required|Description|
|:---|:---|:-------|:----------|
|Action|String|Yes|The name of this interface. Value: ReactivateInstances.|
|InstanceId|String|Yes|The ID of the instance that you want to reactivate.|

## Response parameters {#ResponseParameter .section}

All are common response parameters. See [Common response parameters](../reseller.en-US/API Reference/Getting started/Common parameters.md#commonResponseParameters).

## Examples {#Samples .section}

**Request example** 

```
https://ecs.aliyuncs.com/?Action=ReactivateInstances
&InstanceId=i-instance1
&<Common Request Parameters>
```

**Response examples**

**XML format**

```
<ReactivateInstancesResponse>
    <RequestId>51AB7717-6E1A-4D1D-A44D-54CBxxxxxxxx</RequestId>
</ReactivateInstancesResponse>
```

**JSON format**

```
{
	"RequestId": "51AB7717-6E1A-4D1D-A44D-54CBxxxxxxxx"
}
```

## Error codes {#ErrorCode .section}

|Error code|Error message|HTTP status code|Description|
|:---------|:------------|:---------------|:----------|
|IncorrectInstanceStatus|The current status of the resource does not support this operation.|403|The operation is not supported when the instance is in its current status.|
|InstanceLockedForSecurity|The specified operation is denied as your instance is locked for security reasons.|403|The request is denied because this resource is locked for safety concerns.|
|InsufficientBalance|Your account does not have enough balance.|403|Your account has unpaid bills. Pay all the bills and try again.|
|ReactivateInstances.InstanceStatusNotValid|Instance status is not Expired, ImageExpired or EcsAndImageExpired.|403|The Pay-As-You-Go instance is not in the **Expired** or **Overdue and Being Recycled** status.|
|InvalidInstanceId.NotFound|The specified InstanceId does not exist.|404|The specified InstanceId does not exist.|
|InvalidPayType.NotSupport|The specified pre pay instance not support.|404|This operation is supported only for Pay-As-You-Go instances.|
|InternalError|The request processing has failed due to some unknown error.|500|The error message returned when an internal error occurs. Please try again later.|

