# Use the instance RAM role by calling APIs {#concept_jwk_pd5_xdb .concept}

## Limits {#section_f2w_td5_xdb .section}

Instance RAM roles have the following limits:

-   Instance RAM roles are only applicable to VPC-Connected instances.
-   An ECS instance can only be authorized to one RAM role at a time.
-   After an instance RAM role is attached to an ECS instance, if you want to access other cloud services \(such as OSS, SLB, or ApsaraDB for RDS\) from applications within the ECS instance, you must obtain the authorization credential of the instance RAM role by using [Metadata](reseller.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#). For more information, see [obtain the on-demand authorization credential](#).
-   If you are using an instance RAM role through a RAM user account, you must use a primary account to [authorize a RAM user to use the instance RAM role](#).

## Prerequisite {#section_h2w_td5_xdb .section}

If you are using a RAM user account, it must be authorized to use the instance RAM role. See [activation method](../../../../reseller.en-US/Pricing/Activation method.md#) to activate the RAM service.

## 1. Create an instance RAM role {#step3 .section}

1.  Call the CreateRole [CreateRole](../../../../reseller.en-US/API reference/API Reference (RAM)/Role Management Interface/CreateRole.md#) to create an instance RAM role.
2.  Set a parameter RoleName, for example, EcsRamRoleDocumentTesting.
3.  Set the AssumeRolePolicyDocumentas follows:

    ```
    "Statement": [
    
    "Action": "sts:AssumeRole",
    "Effect": "Allow",
    "Principal": {
    "Service": [
    "ecs.aliyuncs.com"
    
    }
    
    
    "Version": "1"
    ```


## 2. Authorize the instance RAM role {#section_jhn_g25_xdb .section}

1.  Call the CreatePolicy to [CreatePolicy](../../../../reseller.en-US/API reference/API Reference (RAM)/Authorization policy management interface/CreatePolicy.md#) create an authorization policy.
2.  Set a parameter RoleName, for example, set it to EcsRamRoleDocumentTestingPolicy.
3.  Set the PolicyDocumentas follows.

    ```
    "Statement": [
    
    "Action": [
    "oss:Get*",
    "oss:List*"
    
    "Effect": "Allow",
    "Resource": "*"
    
    
    "Version": "1"
    ```

4.  Call the [AttachPolicyToRole](../../../../reseller.en-US/API reference/API Reference (RAM)/Authorization policy management interface/AttachPolicyToRole.md#) to authorize the role policy.
5.  Set PolicyType to Custom.
6.  Set a parameterPolicyName, for example, EcsRamRoleDocumentTestingPolicy.
7.  Set a parameter RoleName, for example, EcsRamRoleDocumentTesting.

## Attach the instance RAM role {#section_pmw_bf5_xdb .section}

1.  Call the [AttachInstanceRamRole ](../../../../reseller.en-US/API Reference/Instances/AttachInstanceRamRole.md#) to attach an instance RAM role to an ECS instance.
2.  Set the parameters RegionId  and InstanceIds to specify an ECS  instance.
3.  Set a parameter RamRoleName, for example, EcsRamRoleDocumentTesting.

## 4. \(Optional\). Detach an instance RAM role {#section_k4m_2f5_xdb .section}

1.  Call the [DetachInstanceRamRole](../../../../reseller.en-US/API Reference/Instances/DetachInstanceRamRole.md#)  to detach an instance RAM role.
2.  Set the parametersRegionId and InstanceIds to specify an ECS  instance.
3.  Set a parameter RamRoleName, for example, EcsRamRoleDocumentTesting.

## 5. \(Optional\). Obtain the on-demand authorization credential {#Token .section}

For the internal application of an ECS instance, you can obtain the STS credential of the instance RAM role, which is a metadata of an instance, to access the role-authorized permissions and resources.  The credential is updated periodically. Example:

1.  Obtain the STS credential of the instance RAM role, for example, EcsRamRoleDocumentTesting:
    -   Linux instance: run `curl http://100.100.100.200/latest/meta-data/Ram/security-credentials/EcsRamRoleDocumentTesting` .
    -   Windows instance: see [Metadata](reseller.en-US/User Guide/Instances/User-defined data and metadata/Metadata.md#).
2.  Get the credential Token. Return example:

    ```
    "AccessKeyId" : "XXXXXXXXX",
    "AccessKeySecret" : "XXXXXXXXX",
    "Expiration" : "2017-11-01T05:20:01Z",
    "SecurityToken" : "XXXXXXXXX",
    "LastUpdated" : "2017-10-31T23:20:01Z",
    "Code" : "Success"
    
    ```


## 6. \(Optional\). Authorize a RAM user to use the instance RAM role {#Authorize .section}

**Note:** You must grant the RAM user with the PassRole permission to use the instance RAM role feature.

Log on to the RAM console and follow the steps to [authorize RAM users](../../../../reseller.en-US/Quick Start/Authorize RAM users.md#). Then, authorize the RAM user to complete the authorization, see the following code snippet as an authorization policy example:

```
"Version": "2016-10-17",
"Statement": [

"Effect": "Allow",
"Action": [
"ecs: [ECS RAM Action]",
"ecs: CreateInstance",
"ecs: AttachInstanceRamRole",
"ecs: DetachInstanceRAMRole"

"Resource": "*"


"Effect": "Allow",
"Action": "ram:PassRole",
"Resource": "*"

```

The parameter \[ECS RAM Action\] indicates that a RAM user is authorized for certain actions. See [authorization rules](../../../../reseller.en-US/API Reference/Authorization rules.md#).

## References {#section_bgl_kf5_xdb .section}

-   Click the following link to see how to [use the instance RAM role in the console](reseller.en-US/User Guide/Instances/Instance RAM roles/Use the instance RAM role in the console.md#).
-   For instruction on how to access other cloud services, see [access other Cloud Product APIs by the Instance RAM Role](../../../../reseller.en-US/Best Practices/Access other Cloud Product APIs by the Instance RAM Role.md#).
-   APIs related to the instance RAM role include:
    -   [CreateRole](../../../../reseller.en-US/API reference/API Reference (RAM)/Role Management Interface/CreateRole.md#): Create an instance RAM role
    -   [ListRoles](../../../../reseller.en-US/API reference/API Reference (RAM)/Role Management Interface/ListRoles.md#): Query the list of instance RAM roles
    -   [CreatePolicy](../../../../reseller.en-US/API reference/API Reference (RAM)/Authorization policy management interface/CreatePolicy.md#): Create an instance RAM role policy
    -   [AttachPolicyToRole](../../../../reseller.en-US/API reference/API Reference (RAM)/Authorization policy management interface/AttachPolicyToRole.md#): Authorize an instance RAM role policy
    -   [AttachInstanceRamRole](../../../../reseller.en-US/API Reference/Instances/AttachInstanceRamRole.md#): Attach an instance RAM role
    -   [DetachInstanceRamRole](../../../../reseller.en-US/API Reference/Instances/DetachInstanceRamRole.md#): Detach an instance RAM role
    -   [DescribeInstanceRamRole](../../../../reseller.en-US/API Reference/Instances/DescribeInstanceRamRole.md#): Query an instance RAM role

