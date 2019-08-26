# Authentication rules {#EcsApiAuthorizationRules .reference}

This topic describes how to use Alibaba Cloud Resource Names \(ARN\) in ECS to authenticate users or user groups, grant RAM user accounts access to resources, and implement access authorization across cloud services.

## Background information {#section_hvf_sxj_dhb .section}

**Note:** If you can access resources without authorization, skip this topic.

You can use your Alibaba Cloud account or RAM user account to perform operations on ECS resources through the ECS API by default. Operation permissions are required when:

-   A RAM user account that you created has no permissions to perform operations on the ECS resources under your Alibaba Cloud account.
-   You want to access ECS resources from other Alibaba Cloud services, or access other Alibaba Cloud services from ECS.
-   You want to perform operations on ECS resources that require operation permissions to be granted by the resource owners.

When an account requests access to ECS resources under your Alibaba Cloud account by calling ECS API operations, Alibaba Cloud ECS instructs RAM to perform a permission check to ensure that the required permissions have been granted to the account that sends the request. Depending on the requested resources and API operation syntaxes, ECS determines which resources require a permission check. For more information about authorization policies and permission control, see [What is RAM?](../../../../intl.en-US/Product Introduction/What is RAM?.md#) and [API overview](../../../../intl.en-US/API Reference/API overview.md#) in the RAM documentation.

## Use ARN values in policies {#section_i54_4fv_fgb .section}

The following section describes how to use an ARN value in a custom policy in the RAM console. You can also call the [CreatePolicy](../../../../intl.en-US/API Reference/Policy management APIs/CreatePolicy.md#) operation to do so.

1.  Log on to the [RAM console](https://ram.console.aliyun.com/policies/new).
2.  In the left-side navigation pane, choose **Permissions** \> **Policies**.
3.  On the Policies page, click **Create Policy**.
4.  On the Create Custom Policy page, set **Policy Name** and **Note**.
5.  Select **Script** for Configuration Mode.

    **Note:** You can also select **Visualized** for Configuration Mode to complete the policy settings without referring to following ARN values section.

6.  Set the parameters in the **Policy Document** section based on the JSON template. Set the Resource parameter to one of the ARN values in the ARN values table. For the settings of other parameters, *see* [Policy elements](../../../../intl.en-US/User Guide/Policies/Policy language/Policy elements.md#) in the RAM documentation.

    ``` {#codeblock_k1y_z8z_xa6}
    {
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "",
                "Resource": ""
            }
        ],
        "Version": "1"
    }
    ```

7.  Click **OK**.

## ARN values {#section_yln_xgy_g2b .section}

The following table lists the ARN values that correspond to some ECS API operations. For information about the ARN format, *see* [Terms](../../../../intl.en-US/Product Introduction/Terms.md#) in the RAM documentation.

|Action|ARN value|
|:-----|:--------|
|AddTags|acs:ecs:$regionid:$accountid:$resourceType/$resourceId|
|AllocatePublicIpAddress|acs:ecs:$regionid:$accountid:instance/$instanceId|
|ApplyAutoSnapshotPolicy|acs:ecs:\*:$accountid:snapshot/\*|
|AttachClassicLinkVpc|acs:ecs:$regionid:$accountid:instance/$instanceId|
|AttachDisk| -   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:instance/$diskId

 |
|AttachKeyPair| -   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:keypair/$keypairName

 |
|AuthorizeSecurityGroup|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|
|AuthorizeSecurityGroupEgress|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|
|CancelAutoSnapshotPolicy|acs:ecs:\*:$accountid:snapshot/\*|
|CancelCopyImage|acs:ecs:$regionid:$accountid:image/$imageNo|
|CopyImage| -   acs:ecs:$fromRegionid:$accountid:image/$imageNo
-   acs:ecs:$toRegionid:$accountid:image/\*

 |
|ConvertNatPublicIpToEip|acs:ecs:$regionid:$accountid:instance/$instanceId|
|CreateAutoSnapshotPolicy|acs:ecs:\*:$accountid:snapshot/\*|
|CreateDisk| -   acs:ecs:$regionid:$accountid:disk/\*
-   acs:ecs:$regionid:$accountid:snapshot/$snapshotId

 |
|CreateImage| -   acs:ecs:$regionid:$accountid:image/\*
-   acs:ecs:$regionid:$accountid:snapshot/$snapshotId
-   acs:ecs:$regionid:$accountid:instance/$instanceId

 |
|CreateInstance| -   acs:ecs:$regionid:$accountid:instance/\*
-   acs:ecs:$regionid:$accountid:image/$imageNo
-   acs:ecs:$regionid:$accountid:securitygroup/$groupNo
-   acs:ecs:$regionid:$accountid:snapshot/$snapshotId
-   \(Optional\) acs:ecs:$regionid:$accountid:keypair/$keyPairName
-   acs:vpc:$regionid:$accountid:vswitch/$vswitchId
-   acs:vpc:$regionid:$accountid:vpc/$vpcId

 |
|CreateKeyPair|acs:ecs:$regionid:$accountid:keypair/\*|
|CreateSecurityGroup|acs:ecs:$regionid:$accountid:securitygroup/\*|
|CreateSnapshot| -   acs:ecs:$regionid:$accountid:snapshot/\*
-   acs:ecs:$regionid:$accountid:disk/$diskId
-   acs:ecs:$regionid:$accountid:volume/$volumeId

 |
|DeleteAutoSnapshotPolicy|acs:ecs:\*:$accountid:snapshot/\*|
|DeleteDisk|acs:ecs:$regionid:$accountid:disk/$diskId|
|DeleteImage|acs:ecs:$regionid:$accountid:image/$imageNo|
|DeleteInstance|acs:ecs:$regionid:$accountid:instance/$instanceId|
|DeleteKeyPairs|acs:ecs:$regionid:$accountid:keypair/$keyPairName|
|DeleteSecurityGroup|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|
|DeleteSnapshot|acs:ecs:$regionid:$accountid:snapshot/$snapshotId|
|DescribeClassicLinkInstances|acs:ecs:$regionid:$accountid:instance/\*|
|DescribeDiskMonitorData|acs:ecs:$regionid:$accountid:disk/$diskId|
|DescribeDisks| -   acs:ecs:$regionid:$accountid:disk/$diskId
-   acs:ecs:$regionid:$accountid:disk/\*

 |
|DescribeImages| -   acs:ecs:$regionid:$accountid:image/$imageNo
-   acs:ecs:$regionid:$accountid:image/\*

 |
|DescribeInstanceMonitorData|acs:ecs:$regionid:$accountid:instance/$instanceId|
|DescribeInstances| -   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:instance/\*

 |
|DescribeInstanceStatus|acs:ecs:$regionid:$accountid:instance/\*|
|DescribeInstanceVncPasswd|acs:ecs:$regionid:$accountid:instance/$instanceId|
|DescribeInstanceVncUrl|acs:ecs:$regionid:$accountid:instance/$instanceId|
|DescribeKeyPairs| -   acs:ecs:$regionid:$accountid:keypair/$keyPairName
-   acs:ecs:$regionid:$accountid:keypair/\*

 |
|DescribePrice|acs:ecs:\*:$accountid:\*|
|DescribeRenewalPrice|acs:ecs:$regionid:$accountid:instance/$instanceId|
|DescribeSecurityGroupAttribute|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|
|DescribeSecurityGroups| -   acs:ecs:$regionid:$accountid:securitygroup/$groupNo
-   acs:ecs:$regionid:$accountid:securitygroup/\*

 |
|DescribeSnapshotAttribute|acs:ecs:$regionid:$accountid:snapshot/$snapshotId|
|DescribeSnapshotLinks| -   acs:ecs:$regionid:$accountid:disk/$diskId
-   acs:ecs:$regionid:$accountid:disk/\*

 |
|DescribeSnapshotMonitorData|acs:ecs:\*:$accountid:snapshot/\*|
|DescribeSnapshots| -   acs:ecs:$regionid:$accountid:snapshot/$snapshotId
-   acs:ecs:$regionid:$accountid:snapshot/\*

 |
|DescribeTags|acs:ecs:$regionid:$accountid:$resourceType/$resourceId|
|DetachClassicLinkVpc|acs:ecs:$regionid:$accountid:instance/$instanceId|
|DetachDisk| -   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:disk/$diskId

 |
|DetachKeyPair| -   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:keypair/$keypairName

 |
|ExportImage|acs:ecs:$regionid:$accountid:image/$imageNo|
|ImportImage|acs:ecs:$regionid:$accountid:image/\*|
|ImportKeyPair|acs:ecs:$regionid:$accountid:keypair/\*|
|JoinSecurityGroup| -   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:securitygroup/$groupNo

 |
|LeaveSecurityGroup| -   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:securitygroup/$groupNo

 |
|ModifyAutoSnapshotPolicy|acs:ecs:\*:$accountid:snapshot/\*|
|ModifyDiskAttribute|acs:ecs:$regionid:$accountid:disk/$diskId|
|ModifyImageAttribute|acs:ecs:$regionid:$accountid:image/$imageNo|
|ModifyInstanceAttribute|acs:ecs:$regionid:$accountid:instance/$instanceId|
|ModifyInstanceAutoReleaseTime|acs:ecs:$regionid:$accountid:instance/$instanceId|
|ModifyInstanceChargeType|acs:ecs:$regionid:$accountid:instance/$instanceId|
|ModifyInstanceNetworkSpec|acs:ecs:$regionid:$accountid:instance/$instanceId|
|ModifyInstanceVncPasswd|acs:ecs:$regionid:$accountid:instance/$instanceId|
|ModifyInstanceVpcAttribute| -   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:vswitch/$vSwitchId

 |
|ModifySecurityGroupAttribute|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|
|ModifySecurityGroupEgressRule|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|
|ModifySecurityGroupRule|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|
|ModifyPrepayInstanceSpec|acs:ecs:$regionid:$accountid:|
|ModifySnapshotAttribute|acs:ecs:$regionid:$accountid:snapshot/$snapshotId|
|RebootInstance|acs:ecs:$regionid:$accountid:instance/$instanceId|
|ReInitDisk|acs:ecs:$regionid:$accountid:disk/$diskId|
|ReleasePublicIpAddress|acs:ecs:$regionid:$accountid:instance/$instanceId|
|RemoveTags|acs:ecs:$regionid:$accountid:$resourceType/$resourceId|
|RenewInstance|acs:ecs:$regionid:$accountid:instance/$instanceId|
|ReplaceSystemDisk| -   acs:ecs:$regionid:$accountid:instance/$instanceId
-   acs:ecs:$regionid:$accountid:image/$imageNo

 |
|ResetDisk|acs:ecs:$regionid:$accountid:disk/$diskId|
|ResizeDisk|acs:ecs:$regionid:$accountid:disk/$diskId|
|RevokeSecurityGroup|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|
|RevokeSecurityGroupEgress|acs:ecs:$regionid:$accountid:securitygroup/$groupNo|
|RunInstances| -   acs:ecs:$regionid:$accountid:instance/\*
-   acs:ecs:$regionid:$accountid:image/$imageNo
-   acs:ecs:$regionid:$accountid:securitygroup/$groupNo
-   acs:ecs:$regionid:$accountid:snapshot/$snapshotId
-   acs:ecs:$regionid:$accountid:keypair/$keyPairName

 |
|StartInstance|acs:ecs:$regionid:$accountid:instance/$instanceId|
|StopInstance|acs:ecs:$regionid:$accountid:instance/$instanceId|

